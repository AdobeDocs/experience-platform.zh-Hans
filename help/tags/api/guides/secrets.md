---
title: Reactor API中的秘密
description: 瞭解如何在Reactor API中設定用於事件轉送的秘密的基礎知識。
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 1%

---

# Reactor API中的秘密

在Reactor API中，秘密是代表驗證認證的資源。 在事件轉送中使用密碼來驗證其他系統的安全資料交換。 因此，只能在事件轉送屬性（具有以下特性的屬性）中建立秘密： `platform` 屬性已設定為 `edge`)。

目前有三個受支援的秘密型別，表示於 `type_of` 屬性：

| 密碼型別 | 描述 |
| --- | --- |
| `token` | 代表兩個系統已知且瞭解的驗證Token值的單一字元字串。 |
| `simple-http` | 包含使用者名稱和密碼的兩個字串屬性。 |
| `oauth2-client_credentials` | 包含數個屬性以支援 [OAuth](https://datatracker.ietf.org/doc/html/rfc6749) 驗證規格。 事件轉送會要求您提供必要資訊，然後以指定間隔為您處理這些權杖的續約。 |

{style="table-layout:auto"}

本指南提供如何設定用於事件轉送的密碼的整體概觀。 如需如何在Reactor API中管理秘密的詳細指引，包括秘密結構的JSON範例，請參閱 [秘密端點指南](../endpoints/secrets.md).

## 凭据

每個密碼都包含 `credentials` 儲存其個別認證值的屬性。 時間 [在API中建立秘密](../endpoints/secrets.md#create)，每種型別的密碼都有不同的必要屬性，如下節所示：

* [`令牌`](#token)
* [&#39;simple-http&#39;](#simple-http)
* [&#39;oauth2-client_credentials&#39;](#oauth2-client_credentials)
* [&#39;oauth2-google&#39;](#oauth2-google)

### `token` {#token}

含的秘密 `type_of` 值 `token` 僅需要下的單一屬性 `credentials`：

| 認證屬性 | 資料型別 | 描述 |
| --- | --- | --- |
| `token` | 字符串 | 目的地系統可理解的秘密Token。 |

{style="table-layout:auto"}

代號會儲存為靜態值，因此密碼的 `expires_at` 和 `refresh_at` 屬性已設定為 `null` 建立密碼時。

### `simple-http` {#simple-http}

含的秘密 `type_of` 值 `simple-http` 需要下列屬性，位於 `credentials`：

| 認證屬性 | 資料型別 | 描述 |
| --- | --- | --- |
| `username` | 字符串 | 使用者名稱。 |
| `password` | 字符串 | 密碼。 API回應中不包含此值。 |

{style="table-layout:auto"}

建立密碼時，兩個屬性會以BASE64編碼交換 `username:password`. 交換後，秘密的 `expires_at` 和 `refresh_at` 屬性已設定為 `null`.

### `oauth2-client_credentials` {#oauth2-client_credentials}

含的秘密 `type_of` 值 `oauth2-client_credentials` 需要下列屬性，位於 `credentials`：

| 認證屬性 | 資料型別 | 描述 |
| --- | --- | --- |
| `client_id` | 字符串 | Oauth整合的使用者端ID。 |
| `client_secret` | 字符串 | OAuth整合的使用者端密碼。 API回應中不包含此值。 |
| `token_url` | 字符串 | Oauth整合的授權URL。 |
| `refresh_offset` | 整数 | *（可選）* 重新整理作業偏移的值（以秒為單位）。 如果在建立密碼時省略了此屬性，則值將設為 `14400` （4小時）預設為關閉。 |
| `options` | 对象 | *（可選）* 指定OAuth整合的其他選項：<ul><li>`scope`：字串，代表 [OAuth 2.0範圍](https://oauth.net/2/scope/) 用於認證。</li><li>`audience`：字串，代表 [Auth0存取權杖](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

當 `oauth2-client_credentials` 密碼建立或更新後， `client_id` 和 `client_secret` (而且可能會 `options`)會在POST要求中交換至 `token_url`，根據OAuth通訊協定的使用者端憑證流程。

>[!NOTE]
>
>授權服務回應本文應與OAuth通訊協定相容。

如果授權服務回應 `200 OK` 和JSON回應內文，則會剖析內文及 `access_token` 會推送至邊緣環境，而且 `expires_in` 用於計算 `expires_at` 和 `refresh_at` 密碼的屬性。 如果密碼上沒有環境關聯， `access_token` 會捨棄。

在以下條件下，憑證交換被視為成功：

* `expires_in` 大於 `28800` （8小時）。
* `refresh_offset` 小於 `expires_in` 減號 `14400` （四個小時）。 例如，如果 `expires_in` 是 `36000` （十小時），以及 `refresh_offset` 是 `28800` （8小時），交換被視為失敗，因為 `28800` 大於 `36000` - `14400` (`21600`)。

如果交換成功，密碼的狀態屬性會設為 `succeeded` 和值 `expires_at` 和 `refresh_at` 已設定：

* `expires_at` 為目前的UTC時間加上 `expires_in`.
* `refresh_at` 為目前的UTC時間加上 `expires_in`，減去 `refresh_offset`. 例如，如果 `expires_in` 是 `43200` （12小時）和 `refresh_offset` 是 `14400` （四個小時）， `refresh_at` 屬性將設為 `28800` （8小時）後結束。

如果交換因任何原因而失敗， `status_details` 中的屬性 `meta` 物件會以相關資訊更新。

#### 重新整理 `oauth2-client_credentials` 密碼

如果 `oauth2-client_credentials` 密碼已指派給環境，其狀態為 `succeeded` （已成功交換認證），新交換會自動執行於 `refresh_at`.

如果交換成功， `refresh_status` 中的屬性 `meta` 物件已設定為 `succeeded` while `expires_at`， `refresh_at`、和 `activated_at` 將進行相應的更新。

如果交換失敗，則會再次嘗試操作3次，最後一次嘗試的時間不超過存取Token過期的兩小時。 如果所有嘗試都失敗， `refresh_status_details` 屬性來自 `meta` 物件會以相關詳細資料更新。

### `oauth2-google` {#oauth2-google}

含的秘密 `type_of` 值 `oauth2-google` 需要下列屬性，位於 `credentials`：

| 認證屬性 | 資料型別 | 描述 |
| --- | --- | --- |
| `scopes` | 陣列 | 列出用於驗證的Google產品範圍。 支援下列範圍：<ul><li>[Google Ads](https://developers.google.com/google-ads/api/docs/oauth/overview)： `https://www.googleapis.com/auth/adwords`</li><li>[Google Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)： `https://www.googleapis.com/auth/pubsub`</li></ul> |

建立之後 `oauth2-google` 密碼，回應包含 `meta.authorization_url` 屬性。 您必須複製此URL並貼到瀏覽器中，才能完成Google驗證流程。

#### 重新授權 `oauth2-google` 密碼

的授權URL `oauth2-google` 密碼在建立後一小時過期（如所示）。 `meta.authorization_url_expires_at`)。 在這之後，必須重新授權密碼才能更新驗證程式。

請參閱 [秘密端點指南](../endpoints/secrets.md#reauthorize) 以取得有關如何重新授權 `oauth2-google` 向Reactor API發出PATCH請求以保密。

## 環境關係

建立密碼時，您必須指定 [環境](../endpoints/environments.md) 將存在的位置。 秘密會立即部署到建立它們的環境。

密碼只能與一個環境相關聯。 一旦秘密和環境之間的關係建立，就不能從環境中清除秘密，而且秘密不能與不同的環境相關聯。

>[!NOTE]
>
>此規則的唯一例外是刪除相關環境時。 在這種情況下，關係會被清除，並且密碼可以指派給不同的環境。

成功交換密碼的認證後，為了將密碼與環境相關聯，交換成品(的權杖字串 `token`，的Base64編碼字串 `simple-http`，或的存取Token `oauth2-client_credentials`)會安全地儲存在環境中。

成功在環境中儲存Exchange成品後，密碼的 `activated_at` 屬性已設定為目前的UTC時間，現在可以使用資料元素參照。 請參閱 [下一節](#referencing-secrets) 以取得參考密碼的詳細資訊。

## 引用密碼 {#referencing-secrets}

為了參考密碼，您必須建立「 」型別的資料元素[!UICONTROL 密碼]&quot; (由 [[!UICONTROL 核心] 擴充功能](../../extensions/client/core/overview.md))。 設定此資料元素時，系統會提示您指出每個環境要使用的密碼。 然後，您可以建立參考機密資料元素的規則，例如HTTP呼叫的標頭內。

![密碼資料元素](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>若要將機密資料元素新增至程式庫，您必須至少有一個 `succeeded` 與建置程式庫之環境相關聯的密碼。 例如，如果程式庫有秘密資料元素，而此元素沒有 `succeeded` 密碼設定用於 [!UICONTROL 中繼密碼] 區段，嘗試在中繼環境中建置該程式庫將會導致錯誤。

在執行階段，秘密資料元素會由儲存在環境中的對應秘密交換成品取代。

## 后续步骤

本指南說明在Reactor API中使用秘密的基礎知識。 有關如何使用API呼叫管理秘密的詳細資訊，請參閱 [秘密端點指南](../endpoints/secrets.md).

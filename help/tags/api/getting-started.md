---
title: Reactor API快速入門
description: 瞭解如何開始使用Reactor API，包括產生所需存取憑證的步驟。
exl-id: fc1acc1d-6cfb-43c1-9ba9-00b2730cad5a
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 1%

---

# Reactor API快速入門

為了使用 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/)，每個請求都必須包含下列驗證標頭：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

本指南說明如何使用Adobe Developer主控台收集這些標頭的值，以便您開始呼叫Reactor API。

## 取得開發人員的Adobe Experience Platform存取權

您必須先擁有開發人員Experience Platform存取權，才能產生Reactor API的驗證值。 若要取得開發人員存取權，請依照 [Experience Platform驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成「取得使用者存取權」步驟後，請返回本教學課程，產生Reactor API的特定認證。

## 產生存取認證

使用Adobe Developer Console時，您必須產生下列三個存取認證：

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

您組織的ID (`{ORG_ID}`)和API金鑰(`{API_KEY}`)可在最初產生API呼叫後，於日後API呼叫中重複使用。 不過，您的存取權杖(`{ACCESS_TOKEN}`)是暫時性的，必須每24小時重新產生一次。

下文將詳細說明產生這些值的步驟。

### 一次性設定

前往 [Adobe Developer主控台](https://www.adobe.com/go/devs_console_ui) 並使用您的Adobe ID登入。 接下來，請依照以下教學課程中概述的步驟操作： [建立空白專案](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) 在開發人員控制檯檔案中。

建立專案後，選取 **新增API** 於 **專案概述** 畫面。

![](../images/api/getting-started/add-api-button.png)

此 **新增API** 畫面隨即顯示。 選取 **Experience Platform Reactor API** 從可用API清單中選取 **下一個**.

![](../images/api/getting-started/add-launch-api.png)

在下一個畫面中，系統提示您建立JSON Web權杖(JWT)認證，以便產生新的金鑰組或上傳您自己的公開金鑰。 在本教學課程中，選取 **產生金鑰組** 選項，然後選取 **產生金鑰組** 右下角。

![](../images/api/getting-started/create-jwt.png)

下一個畫面會確認金鑰組已成功產生，而包含公開憑證和私密金鑰的壓縮資料夾會自動下載至您的電腦。 在後續步驟中需要此私密金鑰才能產生存取權杖。

选择&#x200B;**下一步**&#x200B;以继续。

![](../images/api/getting-started/keypair-generated.png)

下一個畫面會提示您選取一或多個產品設定檔，以與API整合建立關聯。

>[!NOTE]
>
>產品設定檔由您的組織透過Adobe Admin Console管理，並包含精細功能的特定許可權集。 產品設定檔及其許可權只能由組織內具有管理員許可權的使用者管理。 如果您不確定要為API選擇哪些產品設定檔，請聯絡您的管理員。

從清單中選取所需的產品設定檔，然後選取「 」 **儲存已設定的API** 以完成API註冊。

![](../images/api/getting-started/select-product-profile.png)

將API新增至專案後，專案頁面會重新出現在Experience PlatformReactor API頁面上。 從這裡，向下捲動至 **服務帳戶(JWT)** 區段，提供所有呼叫Reactor API時所需的下列存取認證：

* **使用者端ID**：使用者端ID為必要項 `{API_KEY}` 此專案必須提供於 `x-api-key` 標頭。
* **組織ID**：組織ID `{ORG_ID}` 必須在下列專案中使用的值： `x-gw-ims-org-id` 標頭。

![](../images/api/getting-started/access-creds.png)

### 每個工作階段的驗證

現在您已擁有 `{API_KEY}` 和 `{ORG_ID}` 值，最後一個步驟是產生 `{ACCESS_TOKEN}` 值。

>[!NOTE]
>
>這些Token會在24小時後過期。 如果您在應用程式中使用此整合，最好以程式設計方式從應用程式中取得持有人權杖。

根據您的使用案例，您有兩個選項可產生存取權杖：

* [手動產生代號](#manual)
* [以程式設計方式產生代號](#program)

#### 手動產生存取權杖 {#manual}

在文字編輯器或瀏覽器中開啟您先前下載的私密金鑰，並複製其內容。 然後，導覽回開發人員主控台，並將私密金鑰貼入 **產生存取權杖** 區段（位於專案的Reactor API頁面上），然後選取 **產生Token**.

![](../images/api/getting-started/paste-private-key.png)

會產生新的存取Token，並提供按鈕以將該Token複製到剪貼簿。 此值用於必要的 `Authorization` 標頭，且必須以格式提供 `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/token-generated.png)

#### 以程式設計方式產生存取權杖 {#program}

如果您針對應用程式使用整合，可以透過API請求以程式設計方式產生存取權杖。 若要完成此作業，您必須取得下列值：

* 使用者端ID (`{API_KEY}`)
* 使用者端密碼(`{SECRET}`)
* JSON Web權杖(`{JWT}`)

您可以從專案的首頁面取得您的使用者端ID和密碼，請參閱 [上一步](#one-time-setup).

![](../images/api/getting-started/auto-access-creds.png)

若要取得您的JWT認證，請導覽至 **服務帳戶(JWT)** 在左側導覽中，然後選取 **產生JWT** 標籤。 在此頁面上，在 **產生自訂JWT**，將私密金鑰的內容貼到提供的文字方塊中，然後選取 **產生Token**.

![](../images/api/getting-started/generate-jwt.png)

產生的JWT完成處理後會顯示在下方，並附有一個範例cURL命令，您可以視需要用來測試權杖。 使用 **複製** 按鈕以將Token複製到剪貼簿。

![](../images/api/getting-started/jwt-generated.png)

收集您的認證後，您可以將下列API呼叫整合到您的應用程式中，以便以程式設計方式產生存取權杖。

**请求**

要求必須傳送 `multipart/form-data` 裝載，提供您的驗證認證，如下所示：

```shell
curl -X POST \
  https://ims-na1.adobelogin.com/ims/exchange/jwt/ \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

**响应**

成功的回應會傳回新的存取Token，以及到期前的秒數。

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399999
}
```

| 属性 | 描述 |
| :-- | :-- |
| `access_token` | 新產生的存取權杖值。 此值用於必要的 `Authorization` 標頭，且必須以格式提供 `Bearer {ACCESS_TOKEN}`. |
| `expires_in` | Token到期前的剩餘時間（毫秒）。 權杖過期後，必須產生新的權杖。 |

{style="table-layout:auto"}

## 后续步骤

依照本教學課程中的步驟進行，您應該要具備下列專案的有效值： `{ORG_ID}`， `{API_KEY}`、和 `{ACCESS_TOKEN}`. 您現在可以透過在Reactor API的簡單cURL請求中使用這些值來測試這些值。

首先嘗試對進行API呼叫 [列出所有公司](./endpoints/companies.md#list).

>[!NOTE]
>
>您的組織中可能沒有任何公司，在這種情況下，回應將為HTTP狀態404 （找不到）。 只要您沒有收到403 （禁止）錯誤，您的存取認證即有效且可運作。

在您確認存取憑證正常運作後，請繼續探索其他API參考檔案，以瞭解API的多種功能。

## 其他资源

JWT程式庫和SDK： [https://jwt.io/](https://jwt.io/)

Postman API開發： [https://www.postman.com/](https://www.postman.com/)

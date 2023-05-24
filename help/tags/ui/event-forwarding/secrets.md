---
title: 設定事件轉送中的秘密
description: 瞭解如何在UI中設定秘密，以驗證事件轉送屬性中使用的端點。
exl-id: eefd87d7-457f-422a-b159-5b428da54189
source-git-commit: c314cba6b822e12aa0367e1377ceb4f6c9d07ac2
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 4%

---

# 在事件轉送中設定秘密

在事件轉送中，密碼是代表其他系統之驗證認證的資源，允許安全交換資料。 密碼只能在事件轉送屬性中建立。

目前有三種支援的密碼型別：

| 密碼型別 | 描述 |
| --- | --- |
| [!UICONTROL Token] | 代表兩個系統已知且瞭解的驗證Token值的單一字元字串。 |
| [!UICONTROL HTTP] | 包含使用者名稱和密碼的兩個字串屬性。 |
| [!UICONTROL OAuth 2] | 包含數個屬性以支援 [使用者端憑證授權型別](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4) 的 [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) 驗證規格。 系統會要求您提供必要資訊，然後按照指定的間隔為您處理這些權杖的續約。 |
| [!UICONTROL Google OAuth 2] | 包含數個屬性以支援 [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) 驗證規格，用於 [Google Ads API](https://developers.google.com/google-ads/api/docs/oauth/overview) 和 [發佈/訂閱API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview). 系統會要求您提供必要資訊，然後按照指定的間隔為您處理這些權杖的續約。 |

{style="table-layout:auto"}

本指南提供如何設定事件轉送之密碼的高層級概觀([!UICONTROL Edge])屬性(在Experience PlatformUI或資料收集UI中)。

>[!NOTE]
>
>如需如何在Reactor API中管理秘密的詳細指引，包括秘密結構的JSON範例，請參閱 [secrets API指南](../../api/guides/secrets.md).

## 先决条件

本指南假設您已熟悉如何管理UI中標籤和事件轉送的資源，包括如何建立資料元素和事件轉送規則。 請參閱指南： [管理資源](../managing-resources/overview.md) 如果您需要簡介。

您也應該實際瞭解標籤和事件轉送的發佈流程，包括如何將資源新增至程式庫，以及將組建安裝至您的網站進行測試。 請參閱 [發佈概觀](../publishing/overview.md) 以取得更多詳細資料。

## 建立密碼 {#create}

>[!CONTEXTUALHELP]
>id="platform_eventforwarding_secrets_environments"
>title="密钥的环境"
>abstract="要使某个密钥可由事件转发使用，必须将此密钥分配给现有环境。如果您未为事件转发属性创建任何环境，则必须先配置它们，然后再继续。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html" text="环境概述"

若要建立密碼，請選取 **[!UICONTROL 事件轉送]** 在左側導覽中，然後開啟您要新增密碼的事件轉送屬性。 接下來，選取 **[!UICONTROL 秘密]** 在左側導覽列中，後面接著 **[!UICONTROL 建立新密碼]**.

![建立新密碼](../../images/ui/event-forwarding/secrets/create-new-secret.png)

下一個畫面可讓您設定密碼的詳細資訊。 要使某个密钥可由事件转发使用，必须将此密钥分配给现有环境。如果您沒有為事件轉送屬性建立任何環境，請參閱以下指南中的內容： [環境](../publishing/environments.md) 以取得如何設定這些變數的指引，然後再繼續。

>[!NOTE]
>
>如果您仍要在將密碼新增至環境前建立並儲存，請停用 **[!UICONTROL 將密碼附加至環境]** 在填入其餘資訊之前進行切換。 請注意，如果您想要使用密碼，您稍後必須將其指派給環境。
>
>![停用環境](../../images/ui/event-forwarding/secrets/env-disabled.png)

下 **[!UICONTROL 目標環境]**，使用下拉式選單選取您要指派密碼的環境。 下 **[!UICONTROL 密碼名稱]**&#x200B;中，為環境中的密碼命名。 在事件轉送屬性下的所有密碼中，此名稱必須是唯一的。

![環境和名稱](../../images/ui/event-forwarding/secrets/env-and-name.png)

密碼一次只能指派給一個環境，但您可以視需要為跨不同環境的多個密碼指派相同的認證。 選取 **[!UICONTROL 新增環境]** 以新增其他列至清單。

![新增環境](../../images/ui/event-forwarding/secrets/add-env.png)

對於您新增的每個環境，您必須為關聯的密碼提供另一個唯一名稱。 如果您耗盡所有可用的環境， **[!UICONTROL 新增環境]** 按鈕將不可用。

![新增環境無法使用](../../images/ui/event-forwarding/secrets/add-env-greyed.png)

在此，建立密碼的步驟會因您建立的密碼型別而異。 如需詳細資訊，請參閱以下小節：

* [[!UICONTROL Token]](#token)
* [[!UICONTROL HTTP]](#http)
* [[!UICONTROL OAuth 2]](#oauth2)
* [[!UICONTROL Google OAuth 2]](#google-oauth2)

### [!UICONTROL Token] {#token}

若要建立權杖密碼，請選取 **[!UICONTROL Token]** 從 **[!UICONTROL 型別]** 下拉式清單。 在 **[!UICONTROL Token]** 出現的欄位，提供您正在驗證的系統可辨識的認證字串。 選取 **[!UICONTROL 建立密碼]** 以儲存密碼。

![權杖密碼](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

若要建立HTTP密碼，請選取 **[!UICONTROL 簡單HTTP]** 從 **[!UICONTROL 型別]** 下拉式清單。 在下面顯示的欄位中，在選取之前提供認證的使用者名稱和密碼 **[!UICONTROL 建立密碼]** 以儲存密碼。

>[!NOTE]
>
>在儲存認證時，會使用 [「基本」HTTP驗證配置](https://www.rfc-editor.org/rfc/rfc7617.html).

![HTTP密碼](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth 2] {#oauth2}

若要建立OAuth 2密碼，請選取 **[!UICONTROL OAuth 2]** 從 **[!UICONTROL 型別]** 下拉式清單。 在下方顯示的欄位中，提供您的 [[!UICONTROL 使用者端ID] 和 [!UICONTROL 使用者端密碼]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/)，以及您的 [[!UICONTROL 權杖URL]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) ，用於您的OAuth整合。 此 [!UICONTROL 權杖URL] UI中的欄位是授權伺服器主機與權杖路徑之間的串連。

![OAuth 2密碼](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

下 **[!UICONTROL 認證選項]**，您可以提供其他認證選項，例如 `scope` 和 `audience` 鍵值配對的形式。 若要新增更多索引鍵/值組，請選取 **[!UICONTROL 新增另一個]**.

![認證選項](../../images/ui/event-forwarding/secrets/oauth-secret-2.png)

最後，您可以設定 **[!UICONTROL 重新整理位移]** 密碼的值。 這代表系統執行自動重新整理的權杖到期前的秒數。 以小時和分鐘為單位的等效時間會顯示在欄位右側，並在您輸入時自動更新。

![重新整理位移](../../images/ui/event-forwarding/secrets/oauth-secret-3.png)

例如，如果重新整理位移設定為預設值 `14400` （4小時）且存取Token具有 `expires_in` 值 `86400` （24小時），系統將在20小時內自動重新整理密碼。

>[!IMPORTANT]
>
>OAuth密碼在重新整理之間至少需要四個小時，並且至少八小時必須有效。 此限制讓您至少有四個小時可以在產生的Token發生問題時進行干預。
>
>例如，如果位移設定為 `28800` （8小時）且存取Token具有 `expires_in` 之 `36000` （十小時），由於產生的差異不到四小時，交換將會失敗。

完成後，選取 **[!UICONTROL 建立密碼]** 以儲存密碼。

![儲存OAuth 2位移](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

### [!UICONTROL Google OAuth 2] {#google-oauth2}

若要建立Google OAuth 2密碼，請選取 **[!UICONTROL Google OAuth 2]** 從 **[!UICONTROL 型別]** 下拉式清單。 下 **[!UICONTROL 範圍]**，選取您要使用此密碼授與存取權的Google API。 目前支援下列產品：

* [Google Ads API](https://developers.google.com/google-ads/api/docs/oauth/overview)
* [發佈/訂閱API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)

完成後，選取 **[!UICONTROL 建立密碼]**.

![Google OAuth 2密碼](../../images/ui/event-forwarding/secrets/google-oauth.png)

此時會出現彈出視窗，通知您需要透過Google手動授權密碼。 選取 **[!UICONTROL 建立並授權]** 以繼續。

![Google授權彈出視窗](../../images/ui/event-forwarding/secrets/google-authorization.png)

系統會顯示一個對話方塊，讓您輸入Google帳戶的認證。 依照提示操作，授予事件轉送存取許可權給選定範圍下的資料。 一旦授權程式完成，就會建立密碼。

>[!IMPORTANT]
>
>如果您的組織有為Google Cloud應用程式設定的重新驗證原則，則建立的密碼在驗證過期後不會成功重新整理（視原則設定而定，在1到24小時之間）。
>
>若要解決此問題，請登入Google Admin Console並導覽至 **[!DNL App access control]** 頁面，以便將事件轉送應用程式(Adobe Real-Time CDP事件轉送)標示為 [!DNL Trusted]. 請參閱Google檔案，網址為 [設定Google Cloud Services的工作階段長度](https://support.google.com/a/answer/9368756) 以取得詳細資訊。

## 編輯密碼

為屬性建立秘密後，您可在下列位置找到它們： **[!UICONTROL 秘密]** 工作區。 若要編輯現有密碼的詳細資訊，請從清單中選取其名稱。

![選取要編輯的密碼](../../images/ui/event-forwarding/secrets/edit-secret.png)

下一個畫面可讓您變更密碼的名稱和認證。

![編輯密碼](../../images/ui/event-forwarding/secrets/edit-secret-config.png)

>[!NOTE]
>
>如果密碼與現有環境相關聯，則無法將密碼重新指派給其他環境。 如果您想在不同的環境中使用相同的認證，您必須 [建立新密碼](#create) 而非。 從此畫面重新指派環境的唯一方法是如果您未事先將密碼指派給環境，或如果您刪除了密碼附加到的環境。

### 重試秘密交換

您可以從編輯畫面重試或重新整理秘密交換。 此過程因所編輯的密碼型別而異：

| 密碼型別 | 重試通訊協定 |
| --- | --- |
| [!UICONTROL Token] | 選取 **[!UICONTROL Exchange密碼]** 以重試秘密交換。 此控制項僅在環境附加至密碼時可用。 |
| [!UICONTROL HTTP] | 如果沒有附加到密碼的環境，請選取 **[!UICONTROL Exchange密碼]** 以交換認證至base64。 如果附加了環境，請選取「選取」 **[!UICONTROL Exchange和部署密碼]** 以交換至base64並部署密碼。 |
| [!UICONTROL OAuth 2] | 選取 **[!UICONTROL 產生Token]** 以交換認證，並從驗證提供者傳回存取權杖。 |

## 刪除密碼

若要刪除中的現有密碼  **[!UICONTROL 秘密]** 在選取之前，請選取其名稱旁的核取方塊 **[!UICONTROL 刪除]**.

![刪除密碼](../../images/ui/event-forwarding/secrets/delete.png)

## 在事件轉送中使用秘密

為了在事件轉送中使用秘密，您必須先建立 [資料元素](../managing-resources/data-elements.md) 會參照密碼本身。 儲存資料元素後，您可以將其納入事件轉送中 [規則](../managing-resources/rules.md) 並將這些規則新增至 [資料庫](../publishing/libraries.md)，然後可以部署到Adobe的伺服器作為 [建置](../publishing/builds.md).

建立資料元素時，選取 **[!UICONTROL 核心]** 擴充功能，然後選取 **[!UICONTROL 密碼]** （資料元素型別）。 右側面板會更新並提供下拉式控制項，以將最多三個秘密指派給資料元素：一個用於 [!UICONTROL 開發]， [!UICONTROL 分段]、和 [!UICONTROL 生產] （分別）。

![資料元素](../../images/ui/event-forwarding/secrets/data-element.png)

>[!NOTE]
>
>只有附加至開發、測試和生產環境的秘密才會顯示在其各自的下拉式清單中。

藉由將多個秘密指派給單一資料元素並將其納入規則，您可以讓資料元素的值隨著包含程式庫在 [發佈流程](../publishing/publishing-flow.md).

![具有多個密碼的資料元素](../../images/ui/event-forwarding/secrets/multi-secret-data-element.png)

>[!NOTE]
>
>建立資料元素時，必須指派開發環境。 暫存和生產環境的秘密並非必要，但如果組建的秘密型別資料元素未針對相關環境選取秘密，則嘗試轉移至這些環境的組建將會失敗。

## 后续步骤

本指南說明如何在UI中管理秘密。 有關如何使用Reactor API與秘密互動的資訊，請參閱 [秘密端點指南](../../api/endpoints/secrets.md).

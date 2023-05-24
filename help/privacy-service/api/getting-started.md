---
title: Privacy Service API快速入門
description: 在檔案中瞭解如何驗證Privacy ServiceAPI以及如何解譯範例API呼叫。
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 1%

---

# Privacy Service API快速入門

本指南會介紹您在嘗試呼叫Adobe Experience Platform Privacy Service API之前需要瞭解的核心概念。

## 先决条件

本指南需要您實際瞭解 [Privacy Service](../home.md) 以及它如何讓您管理來自Adobe Experience Cloud應用程式中資料主體（客戶）的存取和刪除請求。

為了建立API的存取認證，您組織內的管理員之前必須已設定產品設定檔以在Adobe Admin Console中Privacy Service。 您指派給API整合的產品設定檔決定在存取Privacy Service功能時，整合擁有哪些許可權。 請參閱指南： [管理Privacy Service許可權](../permissions.md) 以取得詳細資訊。

## 收集必要標題的值

若要呼叫Privacy ServiceAPI，您必須先收集要用於必要標題的存取認證：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

這些值的產生方式 [Adobe Developer主控台](https://developer.adobe.com/console). 您的 `{ORG_ID}` 和 `{API_KEY}` 只需產生一次，且可在未來API呼叫中重複使用。 不過，您的 `{ACCESS_TOKEN}` 是暫時性的，必須每24小時重新產生一次。

下文將詳細說明產生這些值的步驟。

### 一次性設定

前往 [Adobe Developer主控台](https://developer.adobe.com/console) 並使用您的Adobe ID登入。 接下來，請依照以下教學課程中概述的步驟操作： [建立空白專案](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) 在開發人員控制檯檔案中。

建立新專案後，選取 **[!UICONTROL 新增至專案]** 並選擇 **[!UICONTROL API]** 下拉式選單中的。

![API選項選取自 [!UICONTROL 新增至專案] 開發人員控制檯中專案詳細資訊頁面的下拉式清單](../images/api/getting-started/add-api-button.png)

#### 選取API並產生金鑰組 {#keypair}

此 **[!UICONTROL 新增API]** 畫面隨即顯示。 選取 **[!UICONTROL Experience Cloud]** 若要縮小可用API的清單，請選取資訊卡 **[!UICONTROL PRIVACY SERVICEAPI]** 選取之前 **[!UICONTROL 下一個]**.

![從可用API清單中選取的Privacy ServiceAPI卡](../images/api/getting-started/add-privacy-service-api.png)

此 **[!UICONTROL 設定API]** 畫面隨即顯示。 選取「 」選項以 **[!UICONTROL 產生金鑰組]**，然後選取 **[!UICONTROL 產生金鑰組]**.

![此 [!UICONTROL 產生金鑰組] 正在選取的選項 [!UICONTROL 設定API] 畫面](../images/api/getting-started/generate-key-pair.png)

系統會自動產生金鑰組，且瀏覽器會下載包含私密金鑰和公開憑證的ZIP檔案（以供稍後步驟使用）。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![在UI中顯示的產生金鑰組，其值會由瀏覽器自動下載](../images/api/getting-started/key-pair-generated.png)

#### 透過產品設定檔指派許可權 {#product-profiles}

最後一個設定步驟是選取此整合將繼承其許可權的產品設定檔。 如果您選取多個設定檔，則會結合其許可權集以進行整合。

>[!NOTE]
>
>管理員可透過Adobe Admin Console建立和管理產品設定檔及其提供的精細許可權。 請參閱指南： [Privacy Service許可權](../permissions.md) 以取得詳細資訊。

完成後，選取 **[!UICONTROL 儲存已設定的API]**.

![儲存設定之前，從清單中選取單一產品設定檔](../images/api/getting-started/select-product-profiles.png)

將API新增至專案後，專案頁面會重新出現在 **Privacy Service API概觀** 頁面。 從這裡，向下捲動至 **[!UICONTROL 服務帳戶(JWT)]** 區段，提供所有呼叫Privacy ServiceAPI時所需的下列存取認證：

* **[!UICONTROL 使用者端ID]**：使用者端ID為必要項 `{API_KEY}` 必須在下列位置提供： `x-api-key` 標頭。
* **[!UICONTROL 組織ID]**：組織ID `{ORG_ID}` 必須在下列專案中使用的值： `x-gw-ims-org-id` 標頭。

![使用者端ID和組織ID值，在設定API後會顯示在專案概觀頁面上](../images/api/getting-started/jwt-credentials.png)

### 每個工作階段的驗證

您必須收集的最終必要認證是 `{ACCESS_TOKEN}`，用於Authorization標頭。 不像 `{API_KEY}` 和 `{ORG_ID}`，必須每24小時產生新Token才能繼續使用API。

一般來說，產生存取權杖有兩種方法：

* [手動產生Token](#manual-token) 以進行測試和開發。
* [自動化權杖產生](#auto-token) 用於API整合。

#### 手動產生權杖 {#manual-token}

若要手動產生新的 `{ACCESS_TOKEN}`，開啟先前下載的私密金鑰，並將其內容貼到旁邊的文字方塊中 **[!UICONTROL 產生存取權杖]** 選取之前 **[!UICONTROL 產生Token]**.

![先前產生的存取Token會貼在專案的概觀頁面上，並使用 [!UICONTROL 產生Token] 之後正在選取的按鈕](../images/api/getting-started/paste-private-key.png)

會產生新的存取Token，並提供按鈕以將該Token複製到剪貼簿。 此值用於所需的Authorization標頭，且必須以格式提供 `Bearer {ACCESS_TOKEN}`.

![從UI複製的已產生存取權杖](../images/api/getting-started/generated-access-token.png)

#### 自動化權杖產生 {#auto-token}

您可以透過向AdobeIdentity Management服務(IMS)的POST請求傳送JSON Web權杖(JWT)，為自動化程式產生新的存取權杖。 請參閱開發人員控制檯檔案： [JWT驗證](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) 以取得詳細步驟。

## 讀取範例API呼叫

每個端點指南都提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/api-guide.md#sample-api) （位於Platform API快速入門手冊）。

## 后续步骤

現在您瞭解要使用哪些標頭，就可以開始呼叫Privacy ServiceAPI了。 選取其中一個端點指南以開始：

* [隱私權工作](./privacy-jobs.md)
* [同意](./consent.md)

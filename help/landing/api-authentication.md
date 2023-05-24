---
keywords: Experience Platform；首頁；熱門主題；驗證；存取
solution: Experience Platform
title: 驗證和存取Experience PlatformAPI
type: Tutorial
description: 此文档分步说明了如何获取 Adobe Experience Platform 开发人员帐户访问权限以调用 Experience Platform API。
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: fa4786b081b46c8f3c0030282ae3900891fbd652
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 6%

---


# 验证和访问 Experience Platform API

此文档分步说明了如何获取 Adobe Experience Platform 开发人员帐户访问权限以调用 Experience Platform API。在本教學課程結束時，您將產生所有Platform API呼叫所需的下列認證：

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

為了維護應用程式和使用者的安全性，對Adobe I/OAPI的所有請求都必須使用OAuth和JSON Web權杖(JWT)等標準進行驗證和授權。 JWT會與使用者端特定資訊搭配使用，以產生您的個人存取權杖。

本教學課程涵蓋如何收集驗證Platform API呼叫所需的認證，如下列流程圖所述：

![](./images/api-authentication/authentication-flowchart.png)

## 先决条件

為了成功呼叫Experience Platform API，您必須具備下列條件：

* 有權存取Adobe Experience Platform的組織。
* 能夠新增您為產品設定檔的開發人員和使用者的Admin Console管理員。

您也必須有Adobe ID才能完成本教學課程。 如果您沒有Adobe ID，可以使用下列步驟建立一個：

1. 前往 [Adobe Developer主控台](https://console.adobe.io).
2. 選取 **[!UICONTROL 建立新帳戶]**.
3. 完成註冊程式。

## 取得Experience Platform的開發人員和使用者存取權

在Adobe Developer Console上建立整合之前，您的帳戶必須擁有Adobe Admin Console中Experience Platform產品設定檔的開發人員和使用者許可權。

### 取得開發人員存取權

聯絡 [!DNL Admin Console] 組織中的管理員，以使用將您作為開發人員新增到Experience Platform產品設定檔 [[!DNL Admin Console]](https://adminconsole.adobe.com/). 請參閱 [!DNL Admin Console] 說明檔案，瞭解如何 [管理產品設定檔的開發人員存取權](https://helpx.adobe.com/cn/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

一旦指派您為開發人員，您就可以開始在中建立整合 [Adobe Developer主控台](https://www.adobe.com/go/devs_console_ui). 這些整合是從外部應用程式和服務到Adobe API的管道。

### 取得使用者存取權

您的 [!DNL Admin Console] 管理員還必須將您作為使用者新增至相同的產品設定檔。 請參閱指南： [管理使用者群組 [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) 以取得詳細資訊。

## 產生API金鑰、組織ID和使用者端密碼 {#api-ims-secret}

>[!NOTE]
>
>如果您要從 [Privacy Service API指南](../privacy-service/api/getting-started.md)，您現在可以返回該指南以產生 [!DNL Privacy Service].

在您透過取得開發人員和使用者的Platform存取權後 [!DNL Admin Console]，下一步是產生 `{ORG_ID}` 和 `{API_KEY}` Adobe Developer Console中的認證。 這些認證只需要產生一次，並可在未來平台API呼叫中重複使用。

### 將Experience Platform新增至專案

前往 [Adobe Developer主控台](https://www.adobe.com/go/devs_console_ui) 並使用您的Adobe ID登入。 接下來，請依照以下教學課程中概述的步驟操作： [建立空白專案](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) 在Adobe Developer Console檔案中。

建立新專案後，選取 **[!UICONTROL 新增API]** 於 **[!UICONTROL 專案概述]** 畫面。

![](./images/api-authentication/add-api.png)

此 **[!UICONTROL 新增API]** 畫面隨即顯示。 選取Adobe Experience Platform的產品圖示，然後選擇 **[!UICONTROL EXPERIENCE PLATFORMAPI]** 選取之前 **[!UICONTROL 下一個]**.

![](./images/api-authentication/platform-api.png)

從這裡，依照教學課程中概述的步驟進行 [使用服務帳戶(JWT)新增API至專案](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) （從「設定API」步驟開始）以完成此程式。

>[!IMPORTANT]
>
>在上述連結程式中的特定步驟中，您的瀏覽器會自動下載私密金鑰和相關聯的公開憑證。 請注意此私密金鑰儲存在電腦上的位置，因為在本教學課程的後續步驟中需要它。

### 收集認證

將API新增至專案後， **[!UICONTROL EXPERIENCE PLATFORMAPI]** 專案的頁面會顯示所有Experience PlatformAPI呼叫所需的下列認證：

* `{API_KEY}` ([!UICONTROL 使用者端ID])
* `{ORG_ID}` ([!UICONTROL 组织 ID])

![](././images/api-authentication/api-key-ims-org.png)

除了上述認證，您還需要產生的 **[!UICONTROL 使用者端密碼]** 以供日後步驟使用。 選取 **[!UICONTROL 擷取使用者端密碼]** 以顯示值，然後複製該值以供日後使用。

![](././images/api-authentication/client-secret.png)

## 產生JSON Web權杖(JWT) {#jwt}

下一步是根據您的帳戶憑證產生JSON Web權杖(JWT)。 此值用於產生 `{ACCESS_TOKEN}` 用於平台API呼叫的認證，必須每24小時重新產生一次。

>[!IMPORTANT]
>
>在本教學課程中，以下步驟會概述如何在開發人員控制檯中產生JWT。 不過，此產生方法僅能用於測試和評估目的。
>
>若要正常使用，必須自動產生JWT。 如需如何以程式設計方式產生JWT的詳細資訊，請參閱 [服務帳戶驗證指南](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/) 在Adobe Developer上。

選取 **[!UICONTROL 服務帳戶(JWT)]** 在左側導覽中，然後選取 **[!UICONTROL 產生JWT]**.

![](././images/api-authentication/generate-jwt.png)

在「 」底下提供的文字方塊中 **[!UICONTROL 產生自訂JWT]**，貼上您先前在將Platform API新增至服務帳戶時產生的私密金鑰內容。 然後，選取 **[!UICONTROL 產生Token]**.

![](././images/api-authentication/paste-key.png)

頁面會更新以顯示產生的JWT，以及可讓您產生存取權杖的範例cURL命令。 在本教學課程中，請選取 **[!UICONTROL 複製]** 旁邊 **[!UICONTROL 產生的JWT]** 以將Token複製到剪貼簿。

![](././images/api-authentication/copy-jwt.png)

## 產生存取權杖

產生JWT後，您可以在API呼叫中使用它來產生 `{ACCESS_TOKEN}`. 不像 `{API_KEY}` 和 `{ORG_ID}`，則必須每24小時產生新Token才能繼續使用Platform API。

**请求**

以下請求會產生新的 `{ACCESS_TOKEN}` 根據裝載中提供的認證。 此端點僅接受表單資料作為其裝載，因此必須給予它 `Content-Type` 頁首 `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| 属性 | 描述 |
| --- | --- |
| `{API_KEY}` | 此 `{API_KEY}` ([!UICONTROL 使用者端ID])中擷取的區段 [上一步](#api-ims-secret). |
| `{SECRET}` | 您在中擷取的使用者端密碼 [上一步](#api-ims-secret). |
| `{JWT}` | 您在中產生的JWT [上一步](#jwt). |

>[!NOTE]
>
>您可以使用相同的API金鑰、使用者端密碼和JWT，為每個工作階段產生新的存取權杖。 這可讓您在應用程式中自動產生存取權杖。

**响应**

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399992
}
```

| 属性 | 描述 |
| --- | --- |
| `token_type` | 傳回的Token型別。 若為存取權杖，此值一律為 `bearer`. |
| `access_token` | 產生的 `{ACCESS_TOKEN}`. 此值（以字為前置詞） `Bearer`，必須做為 `Authentication` 所有Platform API呼叫的標題。 |
| `expires_in` | 存取Token過期前的剩餘毫秒數。 此值達到0後，必須產生新的存取權杖才能繼續使用Platform API。 |

## 測試存取認證

收集完所有三個必要的認證後，您可以嘗試進行下列API呼叫。 此通話會列出所有標準 [!DNL Experience Data Model] (XDM)類別可供您的組織使用。

**请求**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**响应**

如果您的回應類似於下面顯示的回應，則您的認證有效且運作正常。 （此回應已因空格而截斷。）

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

## 使用Postman驗證和測試API呼叫

[Postman](https://www.postman.com/) 是常用的工具，可讓開發人員探索和測試RESTful API。 此 [中度貼文](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) 說明如何設定Postman以自動執行JWT驗證，並使用它來使用平台API。

## 具有Experience Platform許可權的開發人員和API存取控制

>[!NOTE]
>
>只有系統管理員才能在「許可權」中檢視和管理API認證。

在Adobe Developer Console上建立整合之前，您的帳戶必須擁有Adobe Admin Console中Experience Platform產品設定檔的開發人員和使用者許可權。

### 將開發人員新增至產品設定檔

转至[[!DNL Admin Console]](https://adminconsole.adobe.com/)并使用您的 Adobe ID 登录。

選取 **[!UICONTROL 產品]**，然後選取 **[!UICONTROL Adobe Experience Platform]** 從產品清單。

![Admin Console上的產品清單](././images/api-authentication/products.png)

從 **[!UICONTROL 產品設定檔]** 索引標籤，選取 **[!UICONTROL AEP-Default-All-Users]**. 或者，使用搜尋列，輸入名稱以搜尋產品描述檔。

![搜尋產品設定檔](././images/api-authentication/select-product-profile.png)

選取 **[!UICONTROL 開發人員]** 索引標籤，然後選取 **[!UICONTROL 新增開發人員]**.

![從「開發人員」標籤新增開發人員](././images/api-authentication/add-developer1.png)

輸入開發人員的 **[!UICONTROL 電子郵件或使用者名稱]**. 有效的 [!UICONTROL 電子郵件或使用者名稱] 將顯示開發人員詳細資訊。 选择&#x200B;**[!UICONTROL 保存]**。

![使用開發人員的電子郵件或使用者名稱新增開發人員](././images/api-authentication/add-developer-email.png)

已成功新增開發人員，並出現在 [!UICONTROL 開發人員] 標籤。

![「開發人員」標籤上列出的開發人員](././images/api-authentication/developer-added.png)

### 設定API

開發人員可以在Adobe Developer Console的專案中新增和設定API。

選取您的專案，然後選取 **[!UICONTROL 新增API]**.

![將API新增至專案](././images/api-authentication/add-api-project.png)

在 **[!UICONTROL 新增API]** 對話方塊選取 **[!UICONTROL Adobe Experience Platform]**，然後選取 **[!UICONTROL EXPERIENCE PLATFORMAPI]**.

![在Experience Platform中新增API](././images/api-authentication/add-api-platform.png)

在 **[!UICONTROL 設定API]** 畫面，選取 **[!UICONTROL AEP-Default-All-Users]**.

### 將API指派給角色

系統管理員可以在Experience PlatformUI中將API指派給角色。

選取 **[!UICONTROL 許可權]** 以及您想要將API新增至的角色。 選取 **[!UICONTROL API認證]** 索引標籤，然後選取 **[!UICONTROL 新增API認證]**.

![所選角色中的API認證索引標籤](././images/api-authentication/api-credentials.png)

選取您要新增至角色的API，然後選取 **[!UICONTROL 儲存]**.

![可供選擇的API清單](././images/api-authentication/select-api.png)

您會返回 [!UICONTROL API認證] 索引標籤，其中列出新新增的API。

![使用新增API的API憑證標籤](././images/api-authentication/api-credentials-with-added-api.png)

## 后续步骤

閱讀本檔案後，您已收集並成功測試您的Platform API存取認證。 您現在可以依照在整個中提供的範例API呼叫進行 [檔案](../landing/documentation/overview.md).

除了您在本教學課程中收集的驗證值之外，許多Platform API也需要有效的 `{SANDBOX_NAME}` 會以標頭形式提供。 有关更多信息，请参阅[沙盒概述](../sandboxes/home.md)。
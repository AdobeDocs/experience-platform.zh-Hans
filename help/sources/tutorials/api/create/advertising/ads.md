---
title: 使用Flow Service API建立Google Ads基本連線
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連結至Google Ads。
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 7c77b0dc658ad45a25f4ead4e14f5826701cf645
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 1%

---

# 建立Google Ads基本連線，使用 [!DNL Flow Service] API

>[!NOTE]
>
>Google Ads來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步帶您瞭解如何使用，為Google Ads建立基本連線。 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Experience Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

以下小節提供您需要瞭解的其他資訊，以便使用成功連線到Google Ads [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 若要與Google Ads連線，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `clientCustomerId` | 使用者端客戶ID是對應至您要使用Google Ads API管理的Google Ads使用者端帳戶的帳號。 此ID遵循的範本 `123-456-7890`. |
| `loginCustomerId` | 登入客戶ID是與您的Google Ads管理員帳戶對應的帳號，用於從特定的作業客戶擷取報表資料。 如需登入客戶ID的詳細資訊，請閱讀 [Google Ads API檔案](https://developers.google.com/google-ads/api/docs/migration/login-customer-id). |
| `developerToken` | 開發人員權杖可讓您存取Google Ads API。 您可以使用相同的開發人員Token，對所有Google Ads帳戶提出請求。 透過以下方式擷取您的開發人員權杖： [登入您的管理員帳戶](https://ads.google.com/home/tools/manager-accounts/) 然後導覽至 [!DNL API Center] 頁面。 |
| `refreshToken` | 重新整理權杖屬於 [!DNL OAuth2] 驗證。 此權杖可讓您在存取權杖過期後重新產生存取權杖。 |
| `clientId` | 使用者端ID會與使用者端密碼搭配使用，作為的一部分 [!DNL OAuth2] 驗證。 使用者端ID和使用者端密碼可讓您的應用程式藉由在Google中識別您的應用程式，以代表您的帳戶運作。 |
| `clientSecret` | 使用者端密碼會與使用者端ID搭配使用，作為的一部分 [!DNL OAuth2] 驗證。 使用者端ID和使用者端密碼可讓您的應用程式藉由在Google中識別您的應用程式，以代表您的帳戶運作。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 Google Ads的連線規格ID為： `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

閱讀API概觀檔案，瞭解 [Google Ads快速入門的詳細資訊](https://developers.google.com/google-ads/api/docs/first-call/overview).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供您的Google Ads驗證認證作為請求引數的一部分。

**API格式**

```https
POST /connections
```

**请求**

以下請求會建立Google Ads的基本連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Google Ads base connection",
      "description": "Google Ads base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
              "loginCustomerID": "{LOGIN_CUSTOMER_ID}",
              "developerToken": "{DEVELOPER_TOKEN}",
              "authenticationType": "{AUTHENTICATION_TYPE}"
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}",
              "refreshToken": "{REFRESH_TOKEN}"
          }
      },
      "connectionSpec": {
          "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.clientCustomerID` | 您的Google Ads帳戶的使用者端客戶ID。 |
| `auth.params.loginCustomerID` | 與您的Google Ads管理員帳戶對應的登入客戶ID。 |
| `auth.params.developerToken` | 您Google Ads帳戶的開發人員權杖。 |
| `auth.params.refreshToken` | Google Ads帳戶的重新整理Token。 |
| `auth.params.clientID` | Google Ads帳戶的使用者端ID。 |
| `auth.params.clientSecret` | 您的Google Ads帳戶的使用者端密碼。 |
| `connectionSpec.id` | Google Ads連線規格ID： `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**响应**

成功回應會傳回新建立的基本連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

依照本教學課程，您已使用建立Google Ads基本連線： [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用探索資料表格的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，以使用將廣告資料帶入Platform [!DNL Flow Service] API](../../collect/advertising.md)

---
keywords: Experience Platform；首頁；熱門主題；Hubspot；Hubspot
solution: Experience Platform
title: 使用Flow Service API建立HubSpot基本連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至HubSpot。
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# 建立 [!DNL HubSpot] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL HubSpot] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL HubSpot] 使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL HubSpot]，您必須提供下列連線屬性：

| 認證 | 描述 |
| ---------- | ----------- |
| `clientId` | 與您的關聯的使用者端ID [!DNL HubSpot] 應用程式。 |
| `clientSecret` | 與您的關聯的使用者端密碼 [!DNL HubSpot] 應用程式。 |
| `accessToken` | 最初驗證您的OAuth整合時獲得的存取權杖。 |
| `refreshToken` | 初次驗證您的OAuth整合時獲得的重新整理權杖。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL HubSpot] 為： `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

如需入門的詳細資訊，請參閱此 [HubSpot檔案](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL HubSpot] 要求引數中的驗證認證。

**API格式**

```https
POST /connections
```

**请求**

下列要求會建立 [!DNL HubSpot]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for HubSpot",
        "description": "connection for HubSpot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.clientId` | 與您的關聯的使用者端ID [!DNL HubSpot] 應用程式。 |
| `auth.params.clientSecret` | 與您的關聯的使用者端密碼 [!DNL HubSpot] 應用程式。 |
| `auth.params.accessToken` | 最初驗證您的OAuth整合時獲得的存取權杖。 |
| `auth.params.refreshToken` | 初次驗證您的OAuth整合時獲得的重新整理權杖。 |
| `connectionSpec.id` | 此 [!DNL HubSpot] 連線規格ID： `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

**响应**

成功回應會傳回新建立的連線，包括其唯一連線識別碼(`id`)。 在下一個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL HubSpot] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用探索資料表格的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，以使用將行銷自動化資料帶入Platform [!DNL Flow Service] API](../../collect/marketing-automation.md)

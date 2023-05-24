---
keywords: Experience Platform；首頁；熱門主題；方形；方形
title: 使用Flow Service API建立方形基底連線
description: 瞭解如何使用流量服務API將Square連線至Adobe Experience Platform。
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 1%

---

# 建立 [!DNL Square] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Square] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL Square] 使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL Square]，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| --- | --- |
| `host` | 的URL [!DNL Square] 執行個體。 |
| `clientId` | 與您的關聯的使用者端ID [!DNL Square] 帳戶。 |
| `clientSecret` | 與您的關聯的使用者端密碼 [!DNL Square] 帳戶。 |
| `accessToken` | 存取權杖會用於驗證您的 [!DNL Square] 具有OAuth 2.0驗證的帳戶。 存取權杖可以從 [!DNL Square]. |
| `refreshToken` | 重新整理Token可在您目前的存取Token過期後，用來產生新的存取Token。 重新整理權杖可以從 [!DNL Square]. |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Square] 為： `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

如需這些認證以及如何取得認證的詳細資訊，請參閱 [[!DNL Square] oauth上的檔案](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL Square] 要求引數中的驗證認證。

**API格式**

```http
POST /connections
```

**请求**

下列要求會建立 [!DNL Square]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Square Base Connection",
        "description": "Square Base Connection",
        "auth": {
        "specName": "OAuth2 Refresh Code",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            "accessToken": "{ACCESS_TOKEN}"
            "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.host` | 的URL [!DNL Square] 執行個體。 |
| `auth.params.clientId` | 與您的關聯的使用者端ID [!DNL Square] 帳戶。 |
| `auth.params.clientSecret` | 與您的關聯的使用者端密碼 [!DNL Square] 帳戶。 |
| `auth.params.accessToken` | 存取權杖會用於驗證您的 [!DNL Square] 具有OAuth 2.0驗證的帳戶。 存取權杖可以從 [!DNL Square]. |
| `auth.params.refreshToken` | 重新整理Token可在您目前的存取Token過期後，用來產生新的存取Token。 重新整理權杖可以從 [!DNL Square]. |
| `connectionSpec.id` | 此 [!DNL Square] 連線規格ID： `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`. |

**响应**

成功回應會傳回新建立的連線，包括其唯一連線識別碼(`id`)。 在下一個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL Square] 使用下列專案的連線： [!DNL Flow Service] API且已取得連線的唯一ID值。 您可在下一個教學課程中使用此ID，瞭解如何 [使用流程服務API探索付款應用程式](../../explore/payments.md).

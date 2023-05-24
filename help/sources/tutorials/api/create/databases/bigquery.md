---
keywords: Experience Platform；首頁；熱門主題；bigquery；Google；google；Google BigQuery
solution: Experience Platform
title: 使用流量服務API建立Google BigQuery基本連線
type: Tutorial
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至Google BigQuery。
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# 建立 [!DNL Google BigQuery] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Google BigQuery] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Experience Platform元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL Google BigQuery] 使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL Google BigQuery] 至Platform，您必須提供下列OAuth 2.0驗證值：

| 認證 | 描述 |
| ---------- | ----------- |
| `project` | 預設的專案ID [!DNL Google BigQuery] 要查詢的專案。 |
| `clientID` | 用來產生重新整理權杖的ID值。 |
| `clientSecret` | 用來產生重新整理權杖的密碼值。 |
| `refreshToken` | 重新整理權杖取得自 [!DNL Google] 用於授權存取 [!DNL Google BigQuery]. |
| `largeResultsDataSetId` | 預先建立的  [!DNL Google BigQuery] 啟用大型結果集支援所需的資料集ID。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Google BigQuery] 為： `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

如需這些值的詳細資訊，請參閱此 [[!DNL Google BigQuery] 檔案](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL Google BigQuery] 要求引數中的驗證認證。

**API格式**

```https
POST /connections
```

**请求**

下列要求會建立 [!DNL Google BigQuery]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection",
        "description": "Google BigQuery connection",
        "auth": {
            "specName": "Basic Authentication",
            "type": "OAuth2.0",
            "params": {
                    "project": "{PROJECT}",
                    "clientId": "{CLIENT_ID},
                    "clientSecret": "{CLIENT_SECRET}",
                    "refreshToken": "{REFRESH_TOKEN}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.project` | 預設的專案ID [!DNL Google BigQuery] 要查詢的專案。 反對。 |
| `auth.params.clientId` | 用來產生重新整理權杖的ID值。 |
| `auth.params.clientSecret` | 用來產生重新整理權杖的使用者端值。 |
| `auth.params.refreshToken` | 重新整理權杖取得自 [!DNL Google] 用於授權存取 [!DNL Google BigQuery]. |
| `connectionSpec.id` | 此 [!DNL Google BigQuery] 連線規格ID： `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

**响应**

成功回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL Google BigQuery] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用探索資料表格的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流以使用將資料庫資料帶到Platform [!DNL Flow Service] API](../../collect/database-nosql.md)

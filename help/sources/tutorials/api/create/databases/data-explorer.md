---
keywords: Experience Platform；首頁；熱門主題；Azure AzureData Explorer；AzureData Explorer；AzureData Explorer
solution: Experience Platform
title: 使用流程服務API建立Azure AzureData Explorer基底連線
type: Tutorial
description: 瞭解如何使用流量服務API將Azure AzureData Explorer連線到Adobe Experience Platform。
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 1%

---

# 建立 [!DNL Azure Azure Data Explorer] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程將逐步引導您完成建立基礎連線的步驟。 [!DNL Azure Data Explorer] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL Azure Data Explorer] 使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線 [!DNL Azure Data Explorer]，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `endpoint` | 的端點 [!DNL Azure Data Explorer] 伺服器。 |
| `database` | 的名稱 [!DNL Azure Data Explorer] 資料庫。 |
| `tenant` | 用來連線至的不重複租使用者ID [!DNL Azure Data Explorer] 資料庫。 |
| `servicePrincipalId` | 用來連線至的唯一服務主體ID [!DNL Azure Data Explorer] 資料庫。 |
| `servicePrincipalKey` | 用來連線至的唯一服務主體金鑰 [!DNL Azure Data Explorer] 資料庫。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Azure Data Explorer] 是 `0479cc14-7651-4354-b233-7480606c2ac3`. |

如需快速入門的詳細資訊，請參閱此 [[!DNL Azure Data Explorer] 檔案](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基本連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL Azure Data Explorer] 要求引數中的驗證認證。

**API格式**

```https
POST /connections
```

**请求**

下列要求會建立 [!DNL Azure Data Explorer]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Azure Data Explorer connection",
        "description": "A connection for Azure Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.endpoint` | 的端點 [!DNL Azure Data Explorer] 伺服器。 |
| `auth.params.database` | 的名稱 [!DNL Azure Data Explorer] 資料庫。 |
| `auth.params.tenant` | 用來連線至的不重複租使用者ID [!DNL Azure Data Explorer] 資料庫。 |
| `auth.params.servicePrincipalId` | 用來連線至的唯一服務主體ID [!DNL Azure Data Explorer] 資料庫。 |
| `auth.params.servicePrincipalKey` | 用來連線至的唯一服務主體金鑰 [!DNL Azure Data Explorer] 資料庫。 |
| `connectionSpec.id` | 此 [!DNL Azure Data Explorer] 連線規格ID： `0479cc14-7651-4354-b233-7480606c2ac3`. |

**响应**

成功回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下一個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL Azure Data Explorer] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用探索資料表格的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流以使用將資料庫資料帶到Platform [!DNL Flow Service] API](../../collect/database-nosql.md)

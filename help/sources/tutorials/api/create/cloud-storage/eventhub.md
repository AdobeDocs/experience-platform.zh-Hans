---
keywords: Experience Platform；首頁；熱門主題；事件中心；Azure事件中心；事件中心
solution: Experience Platform
title: 使用流程服務API建立Azure事件中樞來源連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至Azure事件中樞帳戶。
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 1%

---


# 建立 [!DNL Azure Event Hubs] 來源連線使用 [!DNL Flow Service] API

本教學課程將逐步引導您完成連線的步驟 [!DNL Azure Event Hubs] (以下稱&quot;[!DNL Event Hubs]&quot;)進行Experience Platform，使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

- [來源](../../../../home.md)： [!DNL Experience Platform] 允許從各種來源擷取資料，同時讓您能夠使用來建構、加標籤和增強傳入資料 [!DNL Platform] 服務。
- [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL Event Hubs] 至平台，使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線您的 [!DNL Event Hubs] 帳戶，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `sasKeyName` | 授權規則的名稱，也稱為SAS金鑰名稱。 |
| `sasKey` | 的主要索引鍵 [!DNL Event Hubs] 名稱空間。 此 `sasPolicy` 此 `sasKey` 對應的必須具有 `manage` 許可權設定順序為 [!DNL Event Hubs] 要填入的清單。 |
| `namespace` | 的名稱空間 [!DNL Event Hubs] 您正在存取。 一個 [!DNL Event Hubs] 名稱空間提供唯一的範圍設定容器，您可以在其中建立一或多個 [!DNL Event Hubs]. |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 此 [!DNL Event Hubs] 連線規格ID為： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

如需這些值的詳細資訊，請參閱 [此事件中樞檔案](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

建立來源連線的第一個步驟是驗證您的 [!DNL Event Hubs] 來源並產生基本連線ID。 基礎連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL Event Hubs] 要求引數中的驗證認證。

**API格式**

```http
POST /connections
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Event Hubs connection",
        "description": "Connector for Azure Event Hubs",
        "auth": {
            "specName": "Azure EventHub authentication credentials",
            "params": {
                "sasKeyName": "{SAS_KEY_NAME}",
                "sasKey": "{SAS_KEY}",
                "namespace": "{NAMESPACE}"
            }
        },
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.sasKeyName` | 授權規則的名稱，也稱為SAS金鑰名稱。 |
| `auth.params.sasKey` | 產生的共用存取權簽章。 |
| `auth.params.namespace` | 的名稱空間 [!DNL Event Hubs] 您正在存取。 |
| `connectionSpec.id` | 此 [!DNL Event Hubs] 連線規格ID為： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**响应**

成功回應會傳回新建立的基本連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此連線ID。

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 建立來源連線

來源連線會建立和管理與擷取資料之外部來源的連線。 來源連線包含資料來源、資料格式等資訊，以及建立資料流所需的來源連線ID。 租使用者和組織專屬的來源連線例項。

POST若要建立來源連線，請向 `/sourceConnections` 的端點 [!DNL Flow Service] API。

**API格式**

```http
POST /sourceConnections
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'authorization: Bearer {ACCESS_TOKEN}' \
    -H 'content-type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -d '{
        "name": "Azure Event Hubs source connection",
        "description": "A source connection for Azure Event Hubs",
        "baseConnectionId": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
        "connectionSpec": {
            "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "eventHubName": "{EVENTHUB_NAME}",
            "dataType": "raw",
            "reset": "latest",
            "consumerGroup": "{CONSUMER_GROUP}"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 來源連線的名稱。 確保來源連線的名稱是描述性的，因為您可以使用此名稱來查閱來源連線的資訊。 |
| `description` | 您可以提供的選用值，包含來源連線的更多資訊。 |
| `baseConnectionId` | 您的的連線ID [!DNL Event Hubs] 上一步驟中產生的來源。 |
| `connectionSpec.id` | 的固定連線規格ID [!DNL Event Hubs]. 此ID為： `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | 的格式 [!DNL Event Hubs] 您要擷取的資料。 目前唯一支援的資料格式為 `json`. |
| `params.eventHubName` | 您的名稱 [!DNL Event Hubs] 來源。 |
| `params.dataType` | 此引數會定義所擷取的資料型別。 支援的資料型別包括： `raw` 和 `xdm`. |
| `params.reset` | 此引數會定義資料讀取的方式。 使用 `latest` 以開始讀取最新的資料，並使用 `earliest` 以開始讀取資料流中的第一個可用資料。 此引數為選用引數，預設值為 `earliest` 若未提供。 |
| `params.consumerGroup` | 要使用的發佈或訂閱機制 [!DNL Event Hubs]. 此引數為選用引數，預設值為 `$Default` 若未提供。 請參閱此 [[!DNL Event Hubs] 活動消費者指南](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) 以取得詳細資訊。 |

## 后续步骤

依照本教學課程，您已建立 [!DNL Event Hubs] 來源連線使用 [!DNL Flow Service] API。 您可以在下一個教學課程中使用此來源連線ID來 [使用建立串流資料流 [!DNL Flow Service] API](../../collect/streaming.md).

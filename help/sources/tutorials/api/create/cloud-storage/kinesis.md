---
keywords: Experience Platform；首頁；熱門主題；Kinesis；kinesis；Amazon Kinesis；amazon kinesis
solution: Experience Platform
title: 使用流量服務API建立Amazon Kinesis來源連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至Amazon Kinesis來源。
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 1%

---

# 建立 [!DNL Amazon Kinesis] 使用流量服務API的來源連線

本教學課程將逐步引導您完成連線的步驟 [!DNL Amazon Kinesis] (以下稱&quot;[!DNL Kinesis]&quot;)進行Experience Platform，使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時能夠使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供對單一檔案進行分割的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

以下小節提供成功連線所需瞭解的其他資訊 [!DNL Kinesis] 至平台，使用 [!DNL Flow Service] API。

### 收集必要的認證

為了 [!DNL Flow Service] 以連線您的 [!DNL Amazon Kinesis] 帳戶，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `accessKeyId` | 存取金鑰ID是用來驗證您的存取金鑰組的一半。 [!DNL Kinesis] 至平台的帳戶。 |
| `secretKey` | 秘密存取金鑰是用來驗證您的存取金鑰組的另一半。 [!DNL Kinesis] 至平台的帳戶。 |
| `region` | 您的地區 [!DNL Kinesis] 帳戶。 請參閱指南： [將IP位址新增至允許清單](../../../../ip-address-allow-list.md) 以取得地區的詳細資訊。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 此 [!DNL Kinesis] 連線規格ID為： `86043421-563b-46ec-8e6c-e23184711bf6`. |

如需詳細資訊，請參閱 [!DNL Kinesis] 存取金鑰以及如何產生金鑰，請參閱此 [[!DNL AWS] IAM使用者管理存取金鑰指南](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

建立來源連線的第一個步驟是驗證您的 [!DNL Kinesis] 來源並產生基本連線ID。 基礎連線ID可讓您瀏覽和瀏覽來源內的檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

POST若要建立基本連線ID，請向 `/connections` 端點，同時提供 [!DNL Kinesis] 要求引數中的驗證認證。

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
        "name": "Amazon Kinesis connection",
        "description": "Connector for Amazon Kinesis",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Aws Kinesis authentication credentials",
            "params": {
                "accessKeyId": "{ACCESS_KEY_ID}",
                "secretKey": "{SECRET_KEY}",
                "region": "{REGION}"
            }
        },
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.accessKeyId` | 您的存取金鑰ID [!DNL Kinesis] 帳戶。 |
| `auth.params.secretKey` | 您的機密存取金鑰 [!DNL Kinesis] 帳戶。 |
| `auth.params.region` | 您的地區 [!DNL Kinesis] 帳戶。 |
| `connectionSpec.id` | 此 [!DNL Kinesis] 連線規格ID： `86043421-563b-46ec-8e6c-e23184711bf6` |

**响应**

成功回應會傳回新建立的基本連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 建立來源連線 {#source}

來源連線會建立和管理與擷取資料之外部來源的連線。 來源連線包含資料來源、資料格式及建立資料流所需的來源連線ID等資訊。 租使用者和組織專屬的來源連線例項。

POST若要建立來源連線，請向 `/sourceConnections` 的端點 [!DNL Flow Service] API。

**API格式**

```http
POST /sourceConnections
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "AWS Kinesis source connection",
        "description": "A source connection for AWS Kinesis",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "stream": "{STREAM}",
            "dataType": "raw",
            "reset": "latest"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 來源連線的名稱。 確保來源連線的名稱是描述性的，因為您可以使用此名稱來查閱來源連線的資訊。 |
| `description` | 您可以提供的選用值，包含來源連線的更多資訊。 |
| `baseConnectionId` | 您的的基本連線ID [!DNL Kinesis] 上一步驟中產生的來源。 |
| `connectionSpec.id` | 的固定連線規格ID [!DNL Kinesis]. 此ID為： `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | 的格式 [!DNL Kinesis] 您要擷取的資料。 目前唯一支援的資料格式為 `json`. |
| `params.stream` | 要從中提取記錄的資料流名稱。 |
| `params.dataType` | 此引數會定義所擷取的資料型別。 支援的資料型別包括： `raw` 和 `xdm`. |
| `params.reset` | 此引數會定義資料讀取的方式。 使用 `latest` 以開始讀取最新的資料，並使用 `earliest` 以開始讀取資料流中的第一個可用資料。 |

**响应**

成功的回應會傳回唯一識別碼(`id`)。 在下個教學課程中，需要此ID才能建立資料流。

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## 后续步骤

依照本教學課程，您已建立 [!DNL Kinesis] 來源連線使用 [!DNL Flow Service] API。 您可以在下一個教學課程中使用此來源連線ID來 [使用建立串流資料流 [!DNL Flow Service] API](../../collect/streaming.md).

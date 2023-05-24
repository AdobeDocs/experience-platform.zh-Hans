---
title: 使用Flow Service API建立Chatlio的來源連線和資料流
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連線至Chatlio。
badge: Beta
exl-id: 867b8096-0841-4462-9888-e60c97c2115e
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1458'
ht-degree: 1%

---

# 為以下專案建立來源連線和資料流： [!DNL Chatlio] 使用流量服務API

>[!NOTE]
>
>此 [!DNL Chatlio] 來源為測試版。 請閱讀 [來源概觀](../../../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

下列教學課程會逐步引導您完成建立來源連線和資料流的步驟，以便 [[!DNL Chatlio]](https://chatlio.com/) 使用將事件資料匯入Adobe Experience Platform [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门 {#getting-started}

本指南需要您實際瞭解下列Experience Platform元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時能夠使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## Connect [!DNL Chatlio] 至平台，使用 [!DNL Flow Service] API {#connect-platform-to-flow-api}

以下概述建立來源連線和資料流所需的步驟，以帶入 [!DNL Chatlio] 要Experience Platform的事件資料。

### 建立來源連線 {#source-connection}

向發出POST要求以建立來源連線 [!DNL Flow Service] API，同時提供來源的連線規格ID、名稱和說明等詳細資訊，以及資料的格式。

**API格式**

```https
POST /sourceConnections
```

**请求**

以下請求會為建立來源連線 [!DNL Chatlio]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Source Connection for Chatlio.",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for Chatlio.",
      "connectionSpec": {
          "id": "073127a3-26e3-496c-9d94-9f48fb93fba8",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 來源連線的名稱。 確保來源連線的名稱是描述性的，因為您可以使用此名稱來查閱來源連線的資訊。 |
| `description` | 您可以納入的選擇性值，可提供來源連線的詳細資訊。 |
| `connectionSpec.id` | 與您的來源對應的連線規格ID。 |
| `data.format` | 的格式 [!DNL Chatlio] 您要擷取的資料。 目前唯一支援的資料格式為 `json`. |

**响应**

成功的回應會傳回唯一識別碼(`id`)。 此ID在後續步驟中是建立資料流的必要專案。

```json
{
    "id": "7689a40d-43eb-4f74-a3f1-092a55884f6c",
    "etag": "\"01013ed0-0000-0200-0000-63f314d00000\""
}
```

### 建立目標XDM結構描述 {#target-schema}

為了在Platform中使用來源資料，必須建立目標結構描述，以根據您的需求來建構來源資料。 然後，目標結構描述會用於建立包含來源資料的Platform資料集。

可透過對以下專案執行POST請求來建立目標XDM結構描述： [結構描述登入API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

如需建立目標XDM結構的詳細步驟，請參閱以下教學課程： [使用API建立結構描述](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=en#create).

### 建立目標資料集 {#target-dataset}

您可以透過對「 」執行POST請求來建立目標資料集 [目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，在裝載中提供目標結構描述的ID。

如需建立目標資料集的詳細步驟，請參閱以下教學課程： [使用API建立資料集](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=en).

### 建立目標連線 {#target-connection}

目標連線代表與要儲存所擷取資料的目的地之間的連線。 若要建立目標連線，您必須提供對應至資料湖的固定連線規格ID。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

您現在擁有目標結構描述、目標資料集和到資料湖的連線規格ID的唯一識別碼。 使用這些識別碼，您可以使用 [!DNL Flow Service] 指定將包含傳入來源資料之資料集的API。

**API格式**

```https
POST /targetConnections
```

**请求**

以下請求會建立目標連線 [!DNL Chatlio]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Target Connection for a Chatlio.",
      "description": "Streaming Target Connection for a Chatlio.",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "https://ns.adobe.com/extconndev/schemas/49cecec83dd1a8da1aef4a96c67c06654e8c337a0a3b4262",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "63ef7df781f14a1bd02a7e49"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 目標連線的名稱。 確保目標連線的名稱是描述性的，因為您可以使用此名稱來查詢目標連線的資訊。 |
| `description` | 您可以納入的選擇性值，可提供目標連線的詳細資訊。 |
| `connectionSpec.id` | 對應至Data Lake的連線規格ID。 此固定ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 的格式 [!DNL Chatlio] 您要擷取的資料。 |
| `params.dataSetId` | 在上一步中擷取的目標資料集ID。 |

**响应**

成功回應會傳回新目標連線的唯一識別碼(`id`)。 此ID在後續步驟中是必要的。

```json
{
    "id": "f7be8ab6-e5ea-4405-83b9-200cdfb2a9e5",
    "etag": "\"7f0072bc-0000-0200-0000-63f314a50000\""
}
```

### 建立對應 {#mapping}

為了將來源資料內嵌到目標資料集中，必須先將其對應到目標資料集所遵守的目標結構描述。 這是透過向執行POST請求來達成 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) 要求裝載中定義資料對應。

**API格式**

```http
POST /conversion/mappingSets
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/945546112b746524bfd9f1264b26c2b7d8e7f5b7fadb953a",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "mappings": [
        {
            "destinationXdmPath": "_extconndev.slackchannel_ID",
            "sourceAttribute": "slackChannelId",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.slackchannel_name",
            "sourceAttribute": "slackChannelName",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.UUID",
            "sourceAttribute": "visitor.UUID",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.chatlio_email",
            "sourceAttribute": "visitor.email",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.message",
            "sourceAttribute": "message",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.channel_ID",
            "sourceAttribute": "channelId",
            "identity": false,
            "version": 0
        }
    ]
  }'
```

| 属性 | 描述 |
| --- | --- |
| `outputSchema.schemaRef.id` | 的ID [目標XDM結構描述](#target-schema) 已在先前步驟中產生。 |
| `mappings.sourceType` | 正在對應的來源屬性型別。 |
| `mappings.source` | 需要對映至目的地XDM路徑的來源屬性。 |
| `mappings.destination` | 來源屬性對應到的目的地XDM路徑。 |

**响应**

成功回應會傳回新建立對應的詳細資料，包括其唯一識別碼(`id`)。 在後續步驟中需要此值，才能建立資料流。

```json
{
    "id": "4b7188aad69c44529a5e674ab5d3568b",
    "version": 0,
    "createdDate": 1676875099546,
    "modifiedDate": 1676875099546,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 建立流程 {#flow}

從以下來源取得資料的最後一步 [!DNL Chatlio] 對Platform而言，就是建立資料流。 到現在為止，您已準備下列必要值：

* [來源連線ID](#source-connection)
* [目標連線ID](#target-connection)
* [映射 ID](#mapping)

資料流負責從來源排程及收集資料。 您可以執行POST要求，同時在裝載中提供先前提及的值，藉此建立資料流。

**API格式**

```http
POST /flows
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Dataflow for Chatlio",
      "description": "Streaming Dataflow for Chatlio",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "7689a40d-43eb-4f74-a3f1-092a55884f6c"
      ],
      "targetConnectionIds": [
          "f7be8ab6-e5ea-4405-83b9-200cdfb2a9e5"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "4b7188aad69c44529a5e674ab5d3568b",
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 資料流的名稱。 確保資料流的名稱是描述性的，因為您可以使用此名稱來查閱資料流上的資訊。 |
| `description` | 您可以納入的選用值，可提供資料流的詳細資訊。 |
| `flowSpec.id` | 建立資料流所需的流量規格ID。 此固定ID為： `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | 流程規格ID的對應版本。 此值預設為 `1.0`. |
| `sourceConnectionIds` | 此 [來源連線ID](#source-connection) 已在先前步驟中產生。 |
| `targetConnectionIds` | 此 [目標連線ID](#target-connection) 已在先前步驟中產生。 |
| `transformations` | 此屬性包含套用至您的資料所需的各種轉換。 將非XDM相容的資料引進Platform時，需要此屬性。 |
| `transformations.name` | 指定給轉換的名稱。 |
| `transformations.params.mappingId` | 此 [對應ID](#mapping) 已在先前步驟中產生。 |
| `transformations.params.mappingVersion` | 對應ID的對應版本。 此值預設為 `0`. |

**响应**

成功的回應會傳回ID (`id`)。 您可以使用此ID來監視、更新或刪除資料流。

```json
{
    "id": "d947e6a9-ea53-42c4-985c-c9379265491f",
    "etag": "\"9b01c840-0000-0200-0000-63f3163e0000\""
}
```

### 取得您的串流端點URL {#get-streaming-endpoint}

建立資料流後，您現在可以擷取串流端點URL。 您將使用此端點URL將您的來源訂閱到webhook，允許您的來源與Experience Platform通訊。

GET若要擷取您的串流端點URL，請向 `/flows` 端點並提供資料流的ID。

**API格式**

```http
GET /flows/{FLOW_ID}
```

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/4982698b-e6b3-48c2-8dcf-040e20121fd2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回資料流上的資訊，包括標示為 `inletUrl`. 請參閱 [設定Webhook](../../../ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint-url) 頁面以取得所需的值。

```json
{
    "items": [
        {
            "id": "d947e6a9-ea53-42c4-985c-c9379265491f",
            "createdAt": 1676875325841,
            "updatedAt": 1676875331938,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Streaming Dataflow for Chatlio",
            "description": "Streaming Dataflow for Chatlio",
            "flowSpec": {
                "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"9b012541-0000-0200-0000-63f316430000\"",
            "etag": "\"9b012541-0000-0200-0000-63f316430000\"",
            "sourceConnectionIds": [
                "7689a40d-43eb-4f74-a3f1-092a55884f6c"
            ],
            "targetConnectionIds": [
                "f7be8ab6-e5ea-4405-83b9-200cdfb2a9e5"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "7689a40d-43eb-4f74-a3f1-092a55884f6c",
                        "connectionSpec": {
                            "id": "073127a3-26e3-496c-9d94-9f48fb93fba8",
                            "version": "1.0"
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "f7be8ab6-e5ea-4405-83b9-200cdfb2a9e5",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "inletUrl": "https://dcs.adobedc.net/collection/e71b6a6cd7270388674f8ab68ee438da58ba4434dea63cc547ee21547275923c"
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "4b7188aad69c44529a5e674ab5d3568b",
                        "mappingVersion": 0
                    }
                }
            ],
            "runs": "/runs?property=flowId==d947e6a9-ea53-42c4-985c-c9379265491f",
            "providerRefId": "bfac26f5-9256-438c-b1a0-e07a7dc675f6",
            "lastOperation": {
                "started": 0,
                "updated": 0,
                "operation": "enable"
            }
        }
    ]
}
```

## 附录 {#appendix}

下節提供您可以監視、更新和刪除資料流的步驟相關資訊。

### 監視資料流 {#monitor-dataflow}

建立資料流後，您可以監視透過它擷取的資料，以檢視有關資料流執行、完成狀態和錯誤的資訊。 如需完整的API範例，請閱讀以下指南： [使用API監控您的來源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### 更新您的資料流 {#update-dataflow}

透過向以下專案發出PATCH請求，更新資料流的詳細資訊，例如其名稱和說明，及其執行排程和相關聯的對應集 `/flows` 端點 [!DNL Flow Service] API，同時提供資料流的ID。 提出PATCH請求時，您必須提供資料流的 `etag` 在 `If-Match` 標頭。 如需完整的API範例，請閱讀以下指南： [使用API更新來源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### 更新您的帳戶 {#update-account}

透過對執行PATCH請求，更新來源帳戶的名稱、說明和認證 [!DNL Flow Service] API時，提供您的基本連線ID作為查詢引數。 提出PATCH請求時，您必須提供來源帳戶的唯一值 `etag` 在 `If-Match` 標頭。 如需完整的API範例，請閱讀以下指南： [使用API更新您的來源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### 刪除您的資料流 {#delete-dataflow}

透過對執行DELETE請求來刪除您的資料流 [!DNL Flow Service] API，同時提供您要作為查詢引數的一部分刪除的資料流的ID。 如需完整的API範例，請閱讀以下指南： [使用API刪除您的資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### 刪除您的帳戶 {#delete-account}

透過對執行DELETE請求來刪除您的帳戶 [!DNL Flow Service] API，同時提供您要刪除之帳戶的基本連線ID。 如需完整的API範例，請閱讀以下指南： [使用API刪除您的來源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).

---
keywords: Experience Platform；首頁；熱門主題；雲端儲存資料；串流資料；串流
solution: Experience Platform
title: 使用流量服務API為原始資料建立串流資料流
type: Tutorial
description: 本教學課程涵蓋擷取串流資料，以及使用來源聯結器和API將資料帶入Platform的步驟。
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 2%

---

# 使用為原始資料建立串流資料流 [!DNL Flow Service] API

本教學課程涵蓋從串流來源聯結器擷取原始資料，以及使用Experience Platform化原始資料的步驟。 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本教學課程需要您實際瞭解Adobe Experience Platform的下列元件：

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   - [結構描述組合基本概念](../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   - [Schema Registry開發人員指南](../../../../xdm/api/getting-started.md)：包含成功執行對Schema Registry API的呼叫所需瞭解的重要資訊。 這包括您的 `{TENANT_ID}`、「容器」的概念，以及發出請求所需的標頭（特別注意「接受」標頭及其可能的值）。
- [[!DNL Catalog Service]](../../../../catalog/home.md)：目錄是Experience Platform中資料位置和譜系的記錄系統。
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md)：Platform的串流擷取為使用者提供一種方法，可即時從使用者端和伺服器端裝置傳送資料至Experience Platform。
- [沙箱](../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../landing/api-guide.md).

### 建立來源連線 {#source}

本教學課程也要求您具備串流聯結器的有效來源連線ID。 如果您沒有這項資訊，請先參閱下列有關建立串流來源連線的教學課程，然後再嘗試進行本教學課程：

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

## 建立目標XDM結構描述 {#target-schema}

為了在Platform中使用來源資料，必須建立目標結構描述，以根據您的需求來建構來源資料。 然後，目標結構描述會用於建立包含來源資料的Platform資料集。 此目標XDM結構描述也會擴充XDM [!DNL Individual Profile] 類別。

POST若要建立目標XDM結構描述，請對 `/schemas` 的端點 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

**API格式**

```http
POST /tenant/schemas
```

**请求**

以下範例請求會建立可擴充XDM的XDM結構描述 [!DNL Individual Profile] 類別。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "type": "object",
        "title": "Sample schema for a streaming connector",
        "description": "Sample schema for a streaming connector",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
            }
        ],
        "meta:containerId": "tenant",
        "meta:resourceType": "schemas",
        "meta:xdmType": "object",
        "meta:class": "https://ns.adobe.com/xdm/context/profile"
    }'
```

**响应**

成功的回應會傳回新建立之綱要的詳細資料，包括其唯一識別碼(`$id`)。 在稍後的步驟中，建立目標資料集、對應和資料流時需要此ID。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:altId": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Sample schema for a streaming connector",
    "type": "object",
    "description": "Sample schema for a streaming connector",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1604960074752,
        "repo:lastModifiedDate": 1604960074752,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{MODIFIED_USER_ID}",
        "eTag": "8522a151effd974429518ed90c3eaf6efc9bf6ffb6644087a85c6d4455dcd045",
        "meta:globalLibVersion": "1.16.1"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "{SANDBOX_ID}",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 建立目標資料集

建立目標XDM結構描述並賦予其唯一性 `$id` 您現在可以建立目標資料集以包含來源資料。 若要建立目標資料集，請向以下發出POST請求： `dataSets` 的端點 [目錄服務API](https://www.adobe.io/experience-platform-apis/references/catalog/)，同時在裝載中提供目標結構描述的ID。

**API格式**

```http
POST /catalog/dataSets
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test streaming dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "identity": [
            "enabled:true"
            ],
            "profile": [
            "enabled:true"
            ]
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 要建立的資料集名稱。 |
| `schemaRef.id` | URI `$id` 資料集將以此為基礎的XDM結構描述。 |
| `schemaRef.contentType` | 結構描述的版本。 此值必須設定為 `application/vnd.adobe.xed-full-notext+json;version=1`，會傳回結構描述的最新次要版本。 請參閱以下小節： [結構描述版本設定](../../../../xdm/api/getting-started.md#versioning) XDM API指南中取得更多資訊。 |

**响应**

成功的回應會傳回陣列，其中包含以格式建立的新資料集的ID `"@/datasets/{DATASET_ID}"`. 資料集ID是系統產生的唯讀字串，用來參考API呼叫中的資料集。 在後續步驟中，建立目標連線和資料流時需要目標資料集ID。

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## 建立目標連線 {#target-connection}

Target連線會建立並管理與Platform或任何已傳輸資料著陸位置的目的地連線。 目標連線包含與建立資料流所需的資料目的地、資料格式和目標連線ID相關的資訊。 Target連線例項是租使用者和組織專屬的。

POST若要建立Target連線，請向 `/targetConnections` 的端點 [!DNL Flow Service] API。 在請求過程中，您必須提供資料格式 `dataSetId` 於上一步驟中擷取，且繫結至的固定連線規格ID [!DNL Data Lake]. 此ID為 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**API格式**

```http
POST /targetConnections
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Streaming target connection",
        "description": "Streaming target connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "5f7187bac6d00f194fb937c0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `connectionSpec.id` | 用來連線至 [!DNL Data Lake]. 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 您要帶入的指定資料格式 [!DNL Data Lake]. |
| `params.dataSetId` | 在上一步中擷取的目標資料集ID。 |

**响应**

成功回應會傳回新目標連線的唯一識別碼(`id`)。 此ID在後續步驟中是必要的。

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## 建立對應 {#mapping}

為了將來源資料內嵌到目標資料集中，必須先將其對應到目標資料集所遵守的目標結構描述。

若要建立對應集，請向以下發出POST請求： `mappingSets` 的端點 [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) 提供您的目標XDM結構描述時 `$id` 以及要建立的對應集的詳細資訊。

**API格式**

```http
POST /mappingSets
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "_{TENANT_ID}.schemas.e45dd983026ce0daec5185cfddd48cbc0509015d880d6186",
        "xdmVersion": "1.0",
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "firstName",
                "identity": false,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "lastName",
                "identity": false,
                "version": 0
            }
        ]
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `xdmSchema` | 此 `$id` 目標XDM結構描述的。 |

**响应**

成功回應會傳回新建立對應的詳細資料，包括其唯一識別碼(`id`)。 此ID在後續步驟中是建立資料流的必要專案。

```json
{
    "id": "380b032b445a46008e77585e046efe5e",
    "version": 0,
    "createdDate": 1604960750613,
    "modifiedDate": 1604960750613,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 擷取資料流規格清單 {#specs}

資料流負責從來源收集資料，並將資料匯入Platform。 若要建立資料流，您必須先透過對以下專案執行GET要求來取得資料流規格： [!DNL Flow Service] API。

**API格式**

```http
GET /flowSpecs
```

**请求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回資料流規格的清單。 您需要擷取的資料流規格ID，才能使用任何 [!DNL Amazon Kinesis]， [!DNL Azure Event Hubs]，或  [!DNL Google PubSub]，是 `d69717ba-71b4-4313-b654-49f9cf126d7a`.

```json
{
    "items": [
        {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "name": "Stream data with optional transformation",
            "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "86043421-563b-46ec-8e6c-e23184711bf6",
                "70116022-a743-464a-bbfe-e226a7f8210c"
            ],
            "targetConnectionSpecIds": [
                "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                "db4fe783-ef79-4a12-bda9-32b2b1bc3b2c"
            ],
            "transformationSpecs": [
                {
                    "name": "Mapping",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines various params required for different mapping from source to target",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            }
                        }
                    }
                }
            ],
            "attributes": {
                "uiAttributes": {
                    "apiFeatures": {
                        "flowRunsSupported": false
                    }
                }
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "StreamingSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        },
    ]
}
```

## 建立資料流

收集串流資料的最後一步是建立資料流。 到現在為止，您已準備下列必要值：

- [來源連線ID](#source)
- [目標連線ID](#target)
- [映射 ID](#mapping)
- [資料流規格ID](#specs)

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
        "name": "Streaming dataflow",
        "description": "Streaming dataflow",
        "flowSpec": {
            "id": "d69717ba-71b4-4313-b654-49f9cf126d7a",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "e96d6135-4b50-446e-922c-6dd66672b6b2"
        ],
        "targetConnectionIds": [
            "723222e2-6ab9-4b0b-b222-e26ab9bb0bc2"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "380b032b445a46008e77585e046efe5e",
                    "mappingVersion": 0
                }
            }
        ]
    }'
```

| 属性 | 描述 |
| --- | --- |
| `flowSpec.id` | 此 [流量規格ID](#specs) 已在上一步中擷取。 |
| `sourceConnectionIds` | 此 [來源連線ID](#source) 已在先前步驟中擷取。 |
| `targetConnectionIds` | 此 [目標連線ID](#target-connection) 已在先前步驟中擷取。 |
| `transformations.params.mappingId` | 此 [對應ID](#mapping) 已在先前步驟中擷取。 |

**响应**

成功的回應會傳回ID (`id`)。

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 后续步骤

依照本教學課程所述，您已建立資料流，以從串流聯結器收集串流資料。 傳入資料現在可供下游平台服務使用，例如 [!DNL Real-Time Customer Profile] 和 [!DNL Data Science Workspace]. 如需更多詳細資訊，請參閱下列檔案：

- [即時客戶個人檔案總覽](../../../../profile/home.md)
- [資料科學工作區概觀](../../../../data-science-workspace/home.md)

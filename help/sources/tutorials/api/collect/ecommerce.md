---
keywords: Experience Platform；首頁；熱門主題；收集電子商務資料；電子商務資料
solution: Experience Platform
title: 使用Flow Service API建立電子商務來源的資料流
type: Tutorial
description: 本教學課程涵蓋從協力廠商電子商務系統擷取資料，以及使用來源聯結器和API擷取資料到Platform的步驟。
exl-id: 0952f037-5e20-4d84-a2e6-2c9470f168f5
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 1%

---

# 使用為電子商務來源建立資料流 [!DNL Flow Service] API

本教學課程涵蓋從電子商務來源擷取資料，並使用將資料帶到Platform的步驟 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>為了建立資料流，您必須擁有包含電子商務來源的有效基底連線ID。 如果您沒有此ID，請參閱 [來源概觀](../../../home.md#ecommerce) 以取得可建立基礎連線的電子商務來源清單。

## 快速入门

本教學課程需要您實際瞭解Adobe Experience Platform的下列元件：

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述登入API](../../../../xdm/api/getting-started.md)：瞭解如何成功執行對結構描述登入API的呼叫。 這包括您的 `{TENANT_ID}`、「容器」的概念，以及發出請求所需的標頭（特別注意「接受」標頭及其可能的值）。
* [[!DNL Catalog Service]](../../../../catalog/home.md)：目錄是內資料位置和譜系的記錄系統 [!DNL Experience Platform].
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md)：批次擷取API可讓您將資料擷取到 [!DNL Experience Platform] 作為批次檔案。
* [[!DNL Sandboxes]](../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南中的 [Platform API快速入門](../../../../landing/api-guide.md).

## 建立來源連線 {#source}

您可以向以下發出POST要求來建立來源連線： [!DNL Flow Service] API。 來源連線由連線ID、來源資料檔案的路徑和連線規格ID組成。

若要建立來源連線，您也必須定義資料格式屬性的列舉值。

對檔案型聯結器使用下列列舉值：

| 資料格式 | 列舉值 |
| ----------- | ---------- |
| 已分隔 | `delimited` |
| JSON | `json` |
| Parquet | `parquet` |

對於所有表式聯結器，將值設定為 `tabular`.

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
        "name": "Shopify source connection",
        "baseConnectionId": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
        "description": "Shopify source connection",
        "data": {
            "format": "tabular"
        },
        "params": {
            "tableName": "Shopify.Orders",
            "columns": [
                {
                    "name": "Email",
                    "type": "string"
                },
                {
                    "name": "Phone",
                    "type": "string"
                },
            ]
        },
        "connectionSpec": {
            "id": "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `baseConnectionId` | 您的電子商務來源的連線ID。 |
| `params.path` | 來源檔案的路徑。 |
| `connectionSpec.id` | 您的電子商務來源的連線規格ID。 |

**响应**

成功的回應會傳回唯一識別碼(`id`)。 建立目標連線的後續步驟需要此ID。

```json
{
    "id": "c278ab14-acdf-440b-b67f-1265d15a7655",
    "etag": "\"10007c3f-0000-0200-0000-5fa9be720000\""
}
```

## 建立目標XDM結構描述 {#target-schema}

為了在Platform中使用來源資料，必須建立目標結構描述，以根據您的需求來建構來源資料。 然後，目標結構描述會用於建立包含來源資料的Platform資料集。

可透過對以下專案執行POST請求來建立目標XDM結構描述： [結構描述登入API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

如需建立目標XDM結構的詳細步驟，請參閱以下教學課程： [使用API建立結構描述](../../../../xdm/api/schemas.md).

## 建立目標資料集 {#target-dataset}

您可以透過對「 」執行POST請求來建立目標資料集 [目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，在裝載中提供目標結構描述的ID。

如需建立目標資料集的詳細步驟，請參閱以下教學課程： [使用API建立資料集](../../../../catalog/api/create-dataset.md).

## 建立目標連線 {#target-connection}

目標連線代表所擷取資料登陸目的地之間的連線。 若要建立目標連線，您必須提供與Data Lake相關聯的固定連線規格ID。 此連線規格ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

您現在擁有目標結構描述、目標資料集和與Data Lake的連線規格ID的唯一識別碼。 使用 [!DNL Flow Service] API後，您可以指定這些識別碼以及將包含傳入來源資料的資料集，藉此建立目標連線。

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
        "name": "Shopify target connection",
        "description": "Shopify target connection",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/854ddc36ad2c7bd001f66a4392575ed4004f81883328772f",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "dataSetId": "5fa9c083de62e418dd170b42"
        },
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `data.schema.id` | 此 `$id` 目標XDM結構描述的。 |
| `data.schema.version` | 結構描述的版本。 此值必須設定 `application/vnd.adobe.xed-full+json;version=1`，會傳回結構描述的最新次要版本。 |
| `params.dataSetId` | 目標資料集的識別碼。 |
| `connectionSpec.id` | 用來連線至Data Lake的連線規格ID。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**响应**

成功回應會傳回新目標連線的唯一識別碼(`id`)。 在後續步驟中需要此值，才能建立資料流。

```json
{
    "id": "6c0ba537-a96b-4d74-8c95-450eb88baee8",
    "etag": "\"00005506-0000-0200-0000-5fa9c13c0000\""
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
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/854ddc36ad2c7bd001f66a4392575ed4004f81883328772f",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "personalEmail.address",
                "sourceAttribute": "Email",
                "identity": false,
                "version": 0
            },
            {
                "destinationXdmPath": "mobilePhone.number",
                "sourceAttribute": "Shipping_Address_Phone",
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
    "id": "22922102bffd4369b6209c102a604062",
    "version": 0,
    "createdDate": 1604960750613,
    "modifiedDate": 1604960750613,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 查詢資料流規格 {#specs}

資料流負責從來源收集資料，並將資料匯入 [!DNL Platform]. 若要建立資料流，您必須先透過對以下專案執行GET要求來取得資料流規格： [!DNL Flow Service] API。 資料流規格負責從電子商務來源收集資料。

**API格式**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

**请求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回負責將資料從來源帶入Platform的資料流規格的詳細資訊。 回應包含唯一的流量規格 `id` 建立新資料流時需要。

>[!NOTE]
>
>為了簡單起見，以下JSON回應裝載已隱藏。 選取「裝載」以檢視回應裝載。

+++ 檢視裝載

```json
{
  "id": "14518937-270c-4525-bdec-c2ba7cce3860",
  "name": "CRMToAEP",
  "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
  "version": "1.0",
  "attributes": {
    "isSourceFlow": true,
    "flacValidationSupported": true,
    "frequency": "batch",
    "notification": {
      "category": "sources",
      "flowRun": {
        "enabled": true
      }
    }
  },
  "sourceConnectionSpecIds": [
    "3416976c-a9ca-4bba-901a-1f08f66978ff",
    "38ad80fe-8b06-4938-94f4-d4ee80266b07",
    "d771e9c1-4f26-40dc-8617-ce58c4b53702",
    "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
    "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
    "3000eb99-cd47-43f3-827c-43caf170f015",
    "26d738e0-8963-47ea-aadf-c60de735468a",
    "74a1c565-4e59-48d7-9d67-7c03b8a13137",
    "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
    "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
    "cb66ab34-8619-49cb-96d1-39b37ede86ea",
    "eb13cb25-47ab-407f-ba89-c0125281c563",
    "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
    "37b6bf40-d318-4655-90be-5cd6f65d334b",
    "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
    "221c7626-58f6-4eec-8ee2-042b0226f03b",
    "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
    "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
    "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
    "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
    "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
    "102706fb-a5cd-42ee-afe0-bc42f017ff43",
    "09182899-b429-40c9-a15a-bf3ddbc8ced7",
    "0479cc14-7651-4354-b233-7480606c2ac3",
    "d6b52d86-f0f8-475f-89d4-ce54c8527328",
    "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
    "1fe283f6-9bec-11ea-bb37-0242ac130002",
    "fcad62f3-09b0-41d3-be11-449d5a621b69",
    "ea1c2a08-b722-11eb-8529-0242ac130003",
    "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
    "ff4274f2-c9a9-11eb-b8bc-0242ac130003",
    "ba5126ec-c9ac-11eb-b8bc-0242ac130003",
    "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
    "929e4450-0237-4ed2-9404-b7e1e0a00309",
    "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
    "2fa8af9c-2d1a-43ea-a253-f00a00c74412"
  ],
  "targetConnectionSpecIds": [
    "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
  ],
  "permissionsInfo": {
    "view": [
      {
        "@type": "lowLevel",
        "name": "EnterpriseSource",
        "permissions": [
          "read"
        ]
      }
    ],
    "manage": [
      {
        "@type": "lowLevel",
        "name": "EnterpriseSource",
        "permissions": [
          "write"
        ]
      }
    ]
  },
  "optionSpec": {
    "name": "OptionSpec",
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "properties": {
        "errorDiagnosticsEnabled": {
          "title": "Error diagnostics.",
          "description": "Flag to enable detailed and sample error diagnostics summary.",
          "type": "boolean",
          "default": false
        },
        "partialIngestionPercent": {
          "title": "Partial ingestion threshold.",
          "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
          "type": "number",
          "exclusiveMinimum": 0
        }
      }
    }
  },
  "scheduleSpec": {
    "name": "PeriodicSchedule",
    "type": "Periodic",
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "properties": {
        "startTime": {
          "description": "epoch time",
          "type": "integer"
        },
        "frequency": {
          "type": "string",
          "enum": [
            "once",
            "minute",
            "hour",
            "day",
            "week"
          ]
        },
        "interval": {
          "type": "integer"
        },
        "backfill": {
          "type": "boolean",
          "default": true
        }
      },
      "required": [
        "startTime",
        "frequency"
      ],
      "if": {
        "properties": {
          "frequency": {
            "const": "once"
          }
        }
      },
      "then": {
        "allOf": [
          {
            "not": {
              "required": [
                "interval"
              ]
            }
          },
          {
            "not": {
              "required": [
                "backfill"
              ]
            }
          }
        ]
      },
      "else": {
        "required": [
          "interval"
        ],
        "if": {
          "properties": {
            "frequency": {
              "const": "minute"
            }
          }
        },
        "then": {
          "properties": {
            "interval": {
              "minimum": 15
            }
          }
        },
        "else": {
          "properties": {
            "interval": {
              "minimum": 1
            }
          }
        }
      }
    }
  },
  "transformationSpec": [
    {
      "name": "Copy",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "properties": {
          "deltaColumn": {
            "type": "object",
            "properties": {
              "name": {
                "type": "string"
              },
              "dateFormat": {
                "type": "string"
              },
              "timezone": {
                "type": "string"
              }
            },
            "required": [
              "name"
            ]
          }
        },
        "required": [
          "deltaColumn"
        ]
      }
    },
    {
      "name": "Mapping",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines various params required for different mapping from source to target",
        "properties": {
          "mappingId": {
            "type": "string"
          },
          "mappingVersion": {
            "type": "string"
          }
        }
      }
    }
  ],
  "runSpec": {
      "name": "ProviderParams",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines various params required for creating flow run.",
        "properties": {
          "startTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the run. The value is represented in Unix epoch time."
          },
          "windowStartTime": {
            "type": "integer",
            "description": "An integer that defines the start time of the window against which data is to be pulled. The value is represented in Unix epoch time."
          },
          "windowEndTime": {
            "type": "integer",
            "description": "An integer that defines the end time of the window against which data is to be pulled. The value is represented in Unix epoch time."
          },
          "deltaColumn": {
            "type": "object",
            "description": "The delta column is required to partition the data and separate newly ingested data from historic data.",
            "properties": {
              "name": {
                "type": "string"
              },
              "dateFormat": {
                "type": "string"
              },
              "timezone": {
                "type": "string"
              }
            },
            "required": [
              "name"
            ]
          }
        },
        "required": [
          "startTime",
          "windowStartTime",
          "windowEndTime",
          "deltaColumn"
        ]
      }
    }
}
```

+++

## 建立資料流

收集資料的最後一步是建立資料流。 此時，您應準備好下列必要值：

* [來源連線ID](#source)
* [目標連線ID](#target)
* [映射 ID](#mapping)
* [資料流規格ID](#specs)

資料流負責從來源排程及收集資料。 您可以執行POST要求，同時在要求裝載中提供先前提到的值，藉此建立資料流。

若要排程內嵌，您必須先將開始時間值設為以秒為單位的epoch時間。 然後，您必須將頻率值設定為下列五個選項之一： `once`， `minute`， `hour`， `day`，或 `week`. 間隔值會指定兩個連續內嵌之間的期間，而建立一次性內嵌不需要設定間隔。 對於所有其他頻率，間隔值必須設定為等於或大於 `15`.

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
        "name": "Test Shopify dataflow",
        "description": "Shopify With mapping ingestion",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "c278ab14-acdf-440b-b67f-1265d15a7655"
        ],
        "targetConnectionIds": [
            "6c0ba537-a96b-4d74-8c95-450eb88baee8"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "22922102bffd4369b6209c102a604062",
                    "mappingVersion": 0
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1604961070",
            "frequency": "once"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `flowSpec.id` | 此 [流量規格ID](#specs) 已在上一步中擷取。 |
| `sourceConnectionIds` | 此 [來源連線ID](#source) 已在先前步驟中擷取。 |
| `targetConnectionIds` | 此 [目標連線ID](#target-connection) 已在先前步驟中擷取。 |
| `transformations.params.mappingId` | 此 [對應ID](#mapping) 已在先前步驟中擷取。 |
| `transformations.params.mappingId` | 與您的電子商務來源相關聯的對應ID。 |
| `scheduleParams.startTime` | 資料流的開始時間（以Epoch時間計）。 |
| `scheduleParams.frequency` | 此 `frequency` 資料流將收集資料的位置。 可接受的值包括： `once`， `minute`， `hour`， `day`，或 `week`. |
| `scheduleParams.interval` | 間隔會指定兩個連續資料流執行之間的期間。 間隔值應為非零整數。 在以下情況不需要間隔： `frequency` 設為 `once` 和應大於或等於 `15` 其他 `frequency` 值。 |

**响应**

成功的回應會傳回ID `id` 建立資料流的URL名稱。

```json
{
    "id": "20c115bc-46e3-40f3-bfe9-fb25abe4ba76",
    "etag": "\"030018cb-0000-0200-0000-5fa9c31a0000\""
}
```

## 監視資料流

建立資料流後，您可以監視透過它擷取的資料，以檢視有關資料流執行、完成狀態和錯誤的資訊。 如需如何監視資料流的詳細資訊，請參閱以下教學課程： [監視API中的資料流 ](../monitor.md)

## 后续步骤

依照本教學課程，您已建立來源聯結器，以依排程收集資料電子商務。 傳入資料現在可供下游使用 [!DNL Platform] 服務，例如 [!DNL Real-Time Customer Profile] 和 [!DNL Data Science Workspace]. 如需更多詳細資訊，請參閱下列檔案：

* [即時客戶個人檔案總覽](../../../../profile/home.md)
* [資料科學工作區概觀](../../../../data-science-workspace/home.md)

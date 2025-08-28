---
title: 创建数据流以将Source数据摄取到Experience Platform
description: 了解如何使用流服务API创建数据流并将源数据摄取到Experience Platform。
hide: true
hidefromtoc: true
source-git-commit: 4e9448170a6c3eb378e003bcd7520cb0e573e408
workflow-type: tm+mt
source-wordcount: '2137'
ht-degree: 2%

---

# 创建数据流以从源中摄取数据

阅读本指南，了解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)创建数据流并将数据摄取到Adobe Experience Platform。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [批量摄取](../../../../ingestion/batch-ingestion/overview.md)：了解如何高效地批量上传大量数据。
* [目录服务](../../../../catalog/datasets/overview.md)：在Experience Platform中组织和跟踪数据集。
* [数据准备](../../../../data-prep/home.md)：转换并映射传入的数据以匹配您的架构要求。
* [数据流](../../../../dataflows/home.md)：设置和管理将数据从源移动到目标的管道。
* [体验数据模型(XDM)架构](../../../../xdm/home.md)：使用XDM架构构建数据，以便在Experience Platform中使用。
* [沙盒](../../../../sandboxes/home.md)：可在不影响生产数据的独立环境中安全测试和开发。
* [源](../../../home.md)：了解如何将外部数据源连接到Experience Platform。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请阅读[Experience Platform API快速入门](../../../../landing/api-guide.md)指南。

### 创建基本连接

您必须具有经过完全身份验证的源帐户及其对应的基本连接ID，才能成功为源创建数据流。 如果没有此ID，请访问[源目录](../../../home.md)以获取可创建基础连接的源列表。

### 创建目标XDM架构 {#target-schema}

Experience Data Model (XDM)架构提供了一种标准化的方式，用于在Experience Platform中组织和描述客户体验数据。 要将源数据摄取到Experience Platform，您必须首先创建目标XDM架构，该架构定义要摄取的数据结构和类型。 此架构将用作您摄取的数据将驻留的Experience Platform数据集的蓝图。

通过对[架构注册表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)执行POST请求，可以创建目标XDM架构。 有关如何创建目标XDM模式的步骤，请阅读以下指南：

* [使用API创建架构](../../../../xdm/api/schemas.md)。
* [使用用户界面创建架构](../../../../xdm/tutorials/create-schema-ui.md)。

创建后，稍后需要目标XDM架构`$id`才能进行目标数据集和映射。

### 创建目标数据集 {#target-dataset}

数据集是用于数据集合的存储和管理结构，通常是表格，其中包含架构（列）和字段（行）。成功引入Experience Platform的数据将作为数据集存储在数据湖中。 在此步骤中，您可以创建新数据集或使用现有数据集。

您可以创建目标数据集，方法是：向[目录服务API](https://developer.adobe.com/experience-platform-apis/references/catalog/)发出POST请求，同时在有效负载中提供目标架构的ID。 有关如何创建目标数据集的详细步骤，请阅读有关[使用API创建数据集](../../../../catalog/api/create-dataset.md)的指南。

>[!TIP]
>
>如果要将数据摄取到Real-time Customer Profile，则必须确保已为配置文件启用目标XDM架构和目标数据集。

+++选择以查看示例

**API格式**

```HTTP
POST /dataSets
```

**请求**

以下示例显示如何创建已启用实时客户配置文件提取的目标数据集。 在此请求中，`unifiedProfile`属性设置为`true`（在`tags`对象下），以告知Experience Platform将此数据集包含在实时客户配置文件中。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Target Dataset",
    "schemaRef": {
      "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
      "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "tags": {
      "unifiedProfile": [
        "enabled: true"
      ]
    }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 目标数据集的描述性名称。 使用清晰且唯一的名称，以便在未来操作中更容易识别和管理您的数据集。 |
| `schemaRef.id` | 目标XDM架构的ID。 |
| `tags.unifiedProfile` | 一个布尔值，通知Experience Platform是否要将数据摄取到实时客户个人资料。 |

**响应**

成功的响应将返回您的目标数据集ID。 稍后需要此ID才能创建目标连接。

```json
[
    "@/dataSets/6889f4f89b982b2b90bc1207"
]
```

+++

## 创建源连接

源连接定义如何从外部源将数据引入Experience Platform。 它指定源系统和传入数据的格式，并引用包含身份验证详细信息的基本连接。 每个源连接对于您的组织都是唯一的。

* 对于基于文件的源（如云存储），源连接可以包括列分隔符、编码类型、压缩类型、文件选择的正则表达式以及是否递归摄取文件等设置。
* 对于基于表的源（如数据库、CRM和营销自动化提供程序），源连接可以指定详细信息，如表名和列映射。

要创建源连接，请向`/sourceConnections` API的[!DNL Flow Service]端点发出POST请求，并提供您的基本连接ID、连接规范ID以及源数据文件的路径。

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
    "name": "ACME source connection",
    "baseConnectionId": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "description": "A source connection for ACME contact data",
    "data": {
      "format": "tabular"
    },
    "params": {
      "tableName": "Contact",
      "columns": [
        {
          "name": "TestID",
          "type": "string",
          "xdm": {
            "type": "string"
          }
        },
        {
          "name": "Name",
          "type": "string",
          "xdm": {
            "type": "string"
          }
        },
        {
          "name": "Datefield",
          "type": "string",
          "meta:xdmType": "date-time",
          "xdm": {
            "type": "string",
            "format": "date-time"
          }
        }
      ],
      "cdcEnabled": true
    },
    "connectionSpec": {
      "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
      "version": "1.0"
    }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的描述性名称。 使用清晰且唯一的名称，以便在未来操作中更容易识别和管理您的连接。 |
| `description` | 可添加的可选描述，用于提供源连接的其他信息。 |
| `baseConnectionId` | 基础连接的`id`。 您可以使用[!DNL Flow Service] API向Experience Platform验证源以检索此ID。 |
| `data.format` | 数据的格式。 对于基于表的源（如数据库、CRM和营销自动化提供程序），将此值设置为`tabular`。 |
| `params.tableName` | 您的源帐户中要摄取到Experience Platform的表的名称。 |
| `params.columns` | 要摄取到Experience Platform的特定数据表列。 |
| `params.cdcEnabled` | 一个布尔值，指示是否启用更改历史记录捕获。 以下数据库源支持此属性： <ul><li>[!DNL Azure Databricks]</li><li>[!DNL Google BigQuery]</li><li>[!DNL Snowflake]</li></ul> 有关详细信息，请阅读有关在源[中使用](../change-data-capture.md)更改数据捕获的指南。 |
| `connectionSpec.id` | 正在使用的源的连接规范ID。 |

**响应**

成功的响应将返回源连接的ID。 创建数据流和摄取数据时需要此ID。

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## 创建目标连接 {#target-connection}

目标连接表示与所摄取数据所登陆的目标之间的连接。 要创建目标连接，您必须提供与数据湖关联的固定连接规范ID。 此连接规范ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

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
      "name": "ACME target connection",
      "description": "ACME target connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 目标连接的描述性名称。 使用清晰且唯一的名称，以便在未来操作中更容易识别和管理您的连接。 |
| `description` | 可添加的可选描述，用于提供目标连接的其他信息。 |
| `data.schema.id` | 目标XDM架构的ID。 |
| `params.dataSetId` | 目标数据集的ID。 |
| `connectionSpec.id` | 数据湖的连接规范ID。 此ID已修复： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |

## 映射 {#mapping}

接下来，必须将源数据映射到目标数据集所遵循的目标架构。 要创建映射，请向`mappingSets`API[[!DNL Data Prep] 的](https://developer.adobe.com/experience-platform-apis/references/data-prep/)端点发出POST请求，并提供您的目标XDM架构ID和要创建的映射集的详细信息。

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
      "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
      "xdmVersion": "1.0",
      "id": null,
      "mappings": [
          {
              "destinationXdmPath": "_id",
              "sourceAttribute": "TestID",
              "identity": false,
              "identityGroup": null,
              "namespaceCode": null,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.fullName",
              "sourceAttribute": "Name",
              "identity": false,
              "identityGroup": null,
              "namespaceCode": null,
              "version": 0
          },
          {
              "destinationXdmPath": "person.birthDate",
              "sourceAttribute": "Datefield",
              "identity": false,
              "identityGroup": null,
              "namespaceCode": null,
              "version": 0
          }
      ]
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `xdmSchema` | 目标XDM架构的`$id`。 |

**响应**

成功的响应返回新创建的映射的详细信息，包括其唯一标识符(`id`)。 此ID是稍后步骤创建数据流所必需的。

```json
{
    "id": "93ddfa69c4864d978832b1e5ef6ec3b9",
    "version": 0,
    "createdDate": 1612309018666,
    "modifiedDate": 1612309018666,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 检索数据流规范

在创建数据流之前，必须首先检索与源对应的数据流规范。 要检索此信息，请向`/flowSpecs` API的[!DNL Flow Service]端点发出GET请求。

**API格式**

```http
GET /flowSpecs?property=name=="{NAME}"
```

| 查询参数 | 描述 |
| --- | --- |
| `property=name=="{NAME}"` | 数据流规范的名称。 <ul><li>对于基于文件的源（如云存储），将此值设置为`CloudStorageToAEP`。</li><li>对于基于表的源（如数据库、CRM和营销自动化提供程序），将此值设置为`CRMToAEP`。</li></ul> |

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回数据流规范的详细信息，该规范负责将数据从源引入Experience Platform。 响应包括创建新数据流所需的唯一流规范`id`。

为确保您使用正确的数据流规范，请检查响应中的`items.sourceConnectionSpecIds`数组。 确认源的连接规范ID已包含在此列表中。

+++选择以查看

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
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
                "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
                "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
                "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
                "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
                "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
                "09182899-b429-40c9-a15a-bf3ddbc8ced7",
                "0479cc14-7651-4354-b233-7480606c2ac3",
                "d6b52d86-f0f8-475f-89d4-ce54c8527328",
                "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
                "fcad62f3-09b0-41d3-be11-449d5a621b69",
                "ea1c2a08-b722-11eb-8529-0242ac130003",
                "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
                "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
                "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
                "2fa8af9c-2d1a-43ea-a253-f00a00c74412",
                "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
            ],
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
            "transformationSpecs": [
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
            },
            "attributes": {
                "recordTypeEnabled": true,
                "defaultRecordType": "profile",
                "isSourceFlow": true,
                "flacValidationSupported": true,
                "isDraftModeSupported": true,
                "frequency": "batch",
                "notification": {
                    "category": "sources",
                    "flowRun": {
                        "enabled": true
                    }
                }
            },
            "permissionsInfo": {
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ],
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ]
            }
        }
    ]
}
```

+++

## 创建数据流

数据流是已配置的管道，可在Experience Platform服务之间传输数据。 它定义如何从外部源（如数据库、云存储或API）摄取数据、如何处理数据并将其路由到目标数据集。 然后，Identity Service、实时客户档案和Destinations等服务使用这些数据集进行激活和分析。

要创建数据流，必须具有以下项的值：

* Source连接Id
* 目标连接ID
* 映射 ID
* 数据流规范ID

在此步骤中，您可以在`scheduleParams`中使用以下参数配置数据流的摄取计划：

| 计划参数 | 描述 |
| --- | --- |
| `startTime` | 数据流应启动的时段时间（以秒为单位）。 |
| `frequency` | 摄取频率。 配置频率以指示数据流运行的频率。 您可以将频率设置为： <ul><li>`once`：将频率设置为`once`以创建一次性摄取。 创建一次性摄取数据流时，间隔和回填配置不可用。 默认情况下，调度频率设置为一次。</li><li>`minute`：将频率设置为`minute`以安排数据流按分钟摄取数据。</li><li>`hour`：将频率设置为`hour`以计划数据流每小时摄取数据。</li><li>`day`：将频率设置为`day`以计划每天摄取数据的数据流。</li><li>`week`：将频率设置为`week`可安排数据流每周摄取数据。</li></ul> |
| `interval` | 连续摄取之间的间隔（除`once`之外的所有频率均需要此间隔）。 配置间隔设置以建立每次引入之间的时间范围。 例如，如果将频率设置为天并将间隔配置为15，则数据流将每15天运行一次。 不能将间隔设置为零。 每个频率的最小接受间隔值如下：<ul><li>`once`：不适用</li><li>`minute`： 15</li><li>`hour`: 1</li><li>`day`: 1</li><li>`week`: 1</li></ul> |
| `backfill` | 指示是否摄取`startTime`之前的历史数据。 |

{style="table-layout:auto"}


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
      "name": "ACME Contact Dataflow",
      "description": "A dataflow for ACME contact data",
      "flowSpec": {
          "id": "14518937-270c-4525-bdec-c2ba7cce3860",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "b7581b59-c603-4df1-a689-d23d7ac440f3"
      ],
      "targetConnectionIds": [
          "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
      ],
      "transformations": [
          {
              "name": "Copy",
              "params": {
                  "deltaColumn": {
                      "name": "Datefield",
                      "dateFormat": "YYYY-MM-DD",
                      "timezone": "UTC"
                  }
              }
          },
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "93ddfa69c4864d978832b1e5ef6ec3b9",
                  "mappingVersion": 0
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1612310466",
          "frequency":"minute",
          "interval":"15",
          "backfill": "true"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 数据流的描述性名称。 使用清晰且唯一的名称，以便在未来操作中更容易识别和管理您的数据流。 |
| `description` | 可添加的可选描述，用于提供数据流的附加信息。 |
| `flowSpec.id` | 与源对应的流规范的ID。 |
| `sourceConnectionIds` | 在之前的步骤中生成的源连接ID。 |
| `targetConnectionIds` | 在之前的步骤中生成的目标连接ID。 |
| `transformations.params.deltaColum` | 用于区分新数据和现有数据的指定列。 将根据选定列的时间戳摄取增量数据。 `deltaColumn`支持的格式为`yyyy-MM-dd HH:mm:ss`。 对于[!DNL Microsoft Dynamics]，`deltaColumn`支持的格式为`yyyy-MM-ddTHH:mm:ssZ`。 |
| `transformations.params.deltaColumn.dateFormat` | 增量列的日期格式。 |
| `transformations.params.deltaColumn.timeZone` | 解释增量列中的值时要使用的时区。 |
| `transformations.params.mappingId` | 在之前的步骤中生成的映射ID。 |
| `scheduleParams.startTime` | 数据流以纪元时间表示的开始时间（自Unix纪元以来的秒数）。 确定数据流何时开始首次运行。 |
| `scheduleParams.frequency` | 数据流运行的频率。 可接受的值包括： `once`、`minute`、`hour`、`day`或`week`。 |
| `scheduleParams.interval` | 连续数据流运行之间的时间间隔，基于所选频率。 必须为非零整数。 例如，间隔为`15`且频率为`minute`意味着数据流每15分钟运行一次。 |
| `scheduleParams.backfill` | 一个布尔值（`true`或`false`），用于确定在首次创建数据流时是否摄取历史数据（回填）。 |

{style="table-layout:auto"}

**响应**

成功的响应返回新创建的数据流的ID (`id`)。

```json
{
    "id": "ae0a9777-b322-4ac1-b0ed-48ae9e497c7e",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

### 使用用户界面验证API工作流

您可以使用Experience Platform用户界面验证数据流的创建。 导航到Experience Platform UI中的&#x200B;*[!UICONTROL 源]*&#x200B;目录，然后从标题选项卡中选择&#x200B;**[!UICONTROL 数据流]**。 接下来，使用[!UICONTROL 数据流名称]列并找到您使用[!DNL Flow Service] API创建的数据流。

![Experience Platform UI中源工作区的数据流界面](../../../images/tutorials/validations/dataflows-interface.png)

您可以通过[!UICONTROL 数据流活动]接口进一步验证数据流。 使用右边栏查看数据流的[!UICONTROL API使用情况]信息。 此部分显示的数据流ID、数据集ID和映射ID与在[!DNL Flow Service]中的数据流创建过程中生成的数据流ID相同。

![源工作区的数据流视图页面。](../../../images/tutorials/validations/api-usage.png)

## 后续步骤

本教程将指导您完成使用[!DNL Flow Service] API在Experience Platform中创建数据流的过程。 您已了解如何创建和配置必要的组件，包括目标XDM架构、数据集、源连接、目标连接和数据流本身。 通过执行以下步骤，您可以将数据从外部源摄取到Experience Platform中自动化，从而使下游服务（如实时客户档案和目标服务）能够将摄取的数据用于高级用例。

### 监测数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关摄取率、成功和错误的信息。 有关如何监视数据流的详细信息，请访问有关[监视帐户和数据流](../../../../dataflows/ui/monitor-sources.md)的教程。

### 更新您的数据流

要更新数据流计划、映射和常规信息的配置，请访问有关[更新源数据流](../../api/update-dataflows.md)的教程。

## 删除您的数据流

您可以删除不再必需的数据流或使用&#x200B;**[!UICONTROL 数据流]**&#x200B;工作区中提供的&#x200B;**[!UICONTROL 删除]**&#x200B;功能错误地创建的数据流。 有关如何删除数据流的详细信息，请访问有关[删除数据流](../../api/delete.md)的教程。
---
keywords: Experience Platform；主页；热门主题；收集协议数据；协议数据
solution: Experience Platform
title: 通过源连接器和API收集协议数据
topic: overview
type: Tutorial
description: 本教程介绍从协议应用程序检索数据并通过源连接器和API将其引入平台的步骤。
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 1%

---


# 通过源连接器和API收集协议数据

本教程介绍从第三方协议应用程序检索数据并通过源连接器和[[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API将其引入Adobe Experience Platform的步骤。

## 入门指南

本教程要求您通过有效的基本连接以及要引入平台的文件的相关信息（包括表的路径和结构）来访问协议系统。 如果您没有此信息，请在尝试本教程之前，参阅教程（位于[浏览使用流服务API](../explore/protocols.md)的协议系统）。

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式注册开发人员指南](../../../../xdm/api/getting-started.md):包括成功执行对模式注册表API的调用时需要了解的重要信息。这包括您的`{TENANT_ID}`、“容器”的概念以及发出请求所需的标头（特别要注意“接受”标头及其可能的值）。
* [[!DNL Catalog Service]](../../../../catalog/home.md):目录是Experience Platform内数据位置和谱系的记录系统。
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md):批处理摄取API允许您将数据作为批处理文件导入到Experience Platform中。
* [沙箱](../../../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个平台实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用[!DNL Flow Service] API成功连接到协议应用程序。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中的[如何阅读示例API调用](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

### 收集所需标题的值

要调用平台API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Experience Platform中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 创建源连接{#source}

可以通过向[!DNL Flow Service] API发出POST请求来创建源连接。 源连接由连接ID、源数据文件的路径和连接规范ID组成。

要创建源连接，还必须为数据格式属性定义枚举值。

为基于文件的连接器使用以下枚举值：

| 数据格式 | 枚举值 |
| ----------- | ---------- |
| 分隔 | `delimited` |
| JSON | `json` |
| 镶木 | `parquet` |

对于所有基于表的连接器，将值设置为`tabular`。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Generic OData source connection",
        "connectionId": "a5c6b647-e784-4b58-86b6-47e784ab580b",
        "description": "Generic OData source connection",
        "data": {
            "format": "tabular",
        },
        "params": {
            "path": "Orders"
        },
        "connectionSpec": {
            "id": "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `connectionId` | 协议应用程序的连接ID |
| `params.path` | 源文件的路径。 |
| `connectionSpec.id` | 协议应用程序的连接规范ID。 |

**响应**

成功的响应会返回新创建的源连接的唯一标识符(`id`)。 此ID是后续步骤中创建目标连接时必需的。

```json
{
    "id": "0a768941-ddfb-499d-b689-41ddfbf99db0",
    "etag": "\"8f00753e-0000-0200-0000-5e8a547d0000\""
}
```

## 创建目标XDM模式{#target-schema}

要在平台中使用源模式，必须创建一个目标，以根据您的需求构建源数据。 然后，目标模式用于创建包含源数据的平台数据集。 此目标XDM模式还扩展了XDM [!DNL Individual Profile]类。

通过对[目标注册表API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)执行POST请求，可以创建模式XDM模式。

**API格式**

```http
POST /tenant/schemas
```

**请求**

以下示例请求创建一个XDM模式，它扩展了XDM [!DNL Individual Profile]类。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "type": "object",
        "title": "Generic OData target XDM schema",
        "description": "Generic OData target XDM schema",
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
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

成功的响应会返回新创建的模式的详细信息，包括其唯一标识符(`$id`)。 后续步骤中需要此ID才能创建目标数据集、映射和数据流。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
    "meta:altId": "_{TENANT_ID}.schemas.e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Generic OData target XDM schema",
    "type": "object",
    "description": "Generic OData target XDM schema",
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
    "imsOrg": "{IMS_ORG}",
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
        "repo:createdDate": 1586124086523,
        "repo:lastModifiedDate": 1586124086523,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "8b281c23af03ff6a8b7d8061c62d73f7bcbfa1fc7dbabebfb4d8ca77130576ca"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 创建目标数据集

通过向[目录服务API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)执行目标请求，提供有效负荷内目标模式的ID，可以创建POST数据集。

**API格式**

```http
POST /dataSets
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Generic OData target dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `schemaRef.id` | 目标XDM模式的`$id`。 |

**响应**

成功的响应返回一个数组，其中包含格式为`"@/datasets/{DATASET_ID}"`的新创建数据集的ID。 数据集ID是由系统生成的只读字符串，用于在API调用中引用数据集。 按照后续步骤中的要求存储目标数据集ID，以创建目标连接和数据流。

```json
[
    "@/dataSets/5e8a55ca53662c18af37a83a"
]
```

## 创建目标连接{#target-connection}

目标连接表示到所摄取数据所进入的目的地的连接。 要创建目标连接，必须提供与数据湖关联的固定连接规范ID。 此连接规范ID为：`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

您现在将唯一标识符作为目标模式目标集和连接规范ID到数据湖。 使用[!DNL Flow Service] API，您可以通过指定这些标识符以及将包含入站源目标的数据集来创建连接。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target Connection for protocols",
        "description": "Target Connection for protocols",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
            }
        },
        "params": {
            "dataSetId": "5e8a55ca53662c18af37a83a"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `data.schema.id` | 目标XDM模式的`$id`。 |
| `params.dataSetId` | 目标数据集的ID。 |
| `connectionSpec.id` | 用于连接到数据湖的连接规范ID。 此ID为：`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |

**响应**

成功的响应会返回新目标连接的唯一标识符(`id`)。 此值是后续步骤中创建数据流的必需值。

```json
{
    "id": "576d5ecf-f114-4587-ad5e-cff1144587f4",
    "etag": "\"13013506-0000-0200-0000-5e8a56d80000\""
}
```

## 创建映射{#mapping}

为了将源数据引入目标数据集，必须首先将其映射到目标数据集所附加的目标模式。 这是通过对[转换服务API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mapping-service-api.yaml)执行POST请求来实现的，该转换服务API具有在请求有效负荷中定义的数据映射。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "OrderID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "CustomerID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "EmployeeID",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "createdByBatchID",
                "sourceAttribute": "OrderDate",
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
| `xdmSchema` | 目标XDM模式的`$id`。 |

**响应**

成功的响应返回新创建的映射的详细信息，包括其唯一标识符(`id`)。 此ID是后续步骤中创建数据流的必需ID。

```json
{
    "id": "37409d3017e24a3eb4a2dc21020f7a5b",
    "version": 0,
    "createdDate": 1586124873209,
    "modifiedDate": 1586124873209,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 查找数据流规范{#specs}

数据流负责从源收集数据并将其引入平台。 要创建数据流，必须首先获得负责从协议应用程序收集数据的数据流规范。

**API格式**

```http
GET /flowSpecs?property=name=="CRMToAEP"
```

**请求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="CRMToAEP"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回负责将数据从源引入平台的数据流规范的详细信息。 响应包括创建新数据流所需的唯一流规范`id`。

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
                "1fe283f6-9bec-11ea-bb37-0242ac130002"
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
            "attributes": {
                "notification": {
                    "category": "sources",
                    "flowRun": {
                        "enabled": true
                    }
                }
            },
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
            }
        }
    ]
}
```

## 创建数据流

收集数据的最后一步是创建数据流。 此时，您应准备以下必需值：

* [源连接ID](#source)
* [目标连接ID](#target)
* [映射ID](#mapping)
* [数据流规范ID](#specs)

数据流负责从源调度和收集数据。 通过在有效负荷中提供先前提到的值时执行POST请求，可以创建数据流。

要计划摄取，您必须首先将开始时间值设置为纪元时间（以秒为单位）。 然后，您必须将频率值设置为以下五个选项之一：`once`、`minute`、`hour`、`day`或`week`。 间隔值指定两个连续摄取之间的周期，并且创建一次摄取不需要设置间隔。 对于所有其他频率，间隔值必须设置为等于或大于`15`。

**API格式**

```http
POST /flows
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Creating a dataflow for a protocols source",
        "description": "Creating a dataflow for a protocols source",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "0a768941-ddfb-499d-b689-41ddfbf99db0"
        ],
        "targetConnectionIds": [
            "576d5ecf-f114-4587-ad5e-cff1144587f4"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": {
                        "name": "updatedAt",
                        "dateFormat": "YYYY-MM-DD",
                        "timezone": "UTC"
                    }
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "7409d3017e24a3eb4a2dc21020f7a5b",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1567411548",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `flowSpec.id` | 在上一步中检索到的[流规范ID](#specs)。 |
| `sourceConnectionIds` | 在之前的步骤中检索到的[源连接ID](#source)。 |
| `targetConnectionIds` | 在之前的步骤中检索到的[目标连接ID](#target-connection)。 |
| `transformations.params.mappingId` | 在之前的步骤中检索到的[映射ID](#mapping)。 |
| `transformations.params.deltaColum` | 用于区分新数据和现有数据的指定列。 增量数据将根据所选列的时间戳被摄取。 使用通用OData时，`deltaColumn`的支持格式为`yyyy-MM-ddTHH:mm:ssZ`。 |
| `transformations.params.mappingId` | 与数据库关联的映射ID。 |
| `scheduleParams.startTime` | 开始时间中数据流的数据时间。 |
| `scheduleParams.frequency` | 数据流收集数据的频率。 可接受的值包括：`once`、`minute`、`hour`、`day`或`week`。 |
| `scheduleParams.interval` | 该间隔指定两个连续流运行之间的周期。 间隔的值应为非零整数。 当频率设置为`once`时，不需要间隔，对于其他频率值，间隔应大于或等于`15`。 |

**响应**

成功的响应会返回新创建的数据流的ID `id`。

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## 监视数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关流运行、完成状态和错误的信息。 有关如何监视数据流的详细信息，请参见有关API ](../monitor.md)中[监视数据流的教程。

## 后续步骤

通过遵循本教程，您已创建了一个源连接器来按计划从协议应用程序收集数据。 现在，下游平台服务（如[!DNL Real-time Customer Profile]和[!DNL Data Science Workspace]）可以使用传入数据。 有关更多详细信息，请参阅以下文档:

* [实时客户用户档案概述](../../../../profile/home.md)
* [数据科学工作区概述](../../../../data-science-workspace/home.md)
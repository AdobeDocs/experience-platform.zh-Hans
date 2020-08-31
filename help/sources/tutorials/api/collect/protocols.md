---
keywords: Experience Platform;home;popular topics; flow service; protocol; generic odata
solution: Experience Platform
title: 通过源连接器和API收集协议数据
topic: overview
description: 本教程介绍从第三方协议提供商检索数据并通过源连接器和流服务API将其引入平台的步骤。
translation-type: tm+mt
source-git-commit: 6578fd607d6f897a403d0af65c81dafe3dc12578
workflow-type: tm+mt
source-wordcount: '1591'
ht-degree: 1%

---


# 通过源连接器和API收集协议数据

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程介绍了从第三方协议应用程序检索数据并通过源连接 [!DNL Platform] 器和[!DNL流服务] [API将其引入](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) 的步骤。

## 入门指南

本教程要求您通过有效的基本连接以及要引入的文件（包括表的路径和结构）的相关信息 [!DNL Platform]来访问协议系统。 如果您没有此信息，请在尝试本教程 [之前参阅教程，了解如何使用流服务](../explore/protocols.md) API浏览协议系统。

* [[!DNL体验数据模型(XDM)系统]](../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式注册开发人员指南](../../../../xdm/api/getting-started.md):包括成功执行对模式注册表API的调用时需要了解的重要信息。 这包括您 `{TENANT_ID}`的、“容器”的概念以及发出请求所需的标题（特别要注意“接受”标题及其可能的值）。
* [[!DNL目录服务]](../../../../catalog/home.md):目录是数据位置和谱系的记录系统 [!DNL Experience Platform]。
* [[!DNL批量摄取]](../../../../ingestion/batch-ingestion/overview.md):批处理摄取API允许您将数据作为批 [!DNL Experience Platform] 处理文件收录。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用API成功连接到协议应用程 [!DNL Flow Service] 序。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

中的所有资 [!DNL Experience Platform]源(包括属于这些资 [!DNL Flow Service]源)都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 创建源连接 {#source}

您可以通过向API发出POST请求来创建源 [!DNL Flow Service] 连接。 源连接由连接ID、源数据文件的路径和连接规范ID组成。

要创建源连接，还必须为数据格式属性定义枚举值。

对基于文件的连接器使 **用以下枚举值**:

| Data.format | 枚举值 |
| ----------- | ---------- |
| 分隔文件 | `delimited` |
| JSON文件 | `json` |
| 镶木文件 | `parquet` |

对于所 **有基于表的连接器** ，请使用枚举值： `tabular`.

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
        "name": "Protocols source connection",
        "baseConnectionId": "a5c6b647-e784-4b58-86b6-47e784ab580b",
        "description": "Protocols source connection to ingest Orders",
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
| `baseConnectionId` | 协议应用程序的连接ID |
| `params.path` | 源文件的路径。 |
| `connectionSpec.id` | 协议应用程序的连接规范ID。 |

**响应**

成功的响应会返回新创建的源`id`连接的唯一标识符()。 此ID是后续步骤中创建目标连接时必需的。

```json
{
    "id": "0a768941-ddfb-499d-b689-41ddfbf99db0",
    "etag": "\"8f00753e-0000-0200-0000-5e8a547d0000\""
}
```

## 创建目标XDM模式 {#target-schema}

在前面的步骤中，创建了一个专门的XDM模式来构造源数据。 为了在中使用源数据，还必 [!DNL Platform]须创建目标模式，以根据您的需要构建源数据。 然后，目标模式用于创建包含 [!DNL Platform] 源数据的数据集。 此目标XDM模式还扩展了XDM [!DNL Individual Profile] 类。

通过对目标注册表API执行POST请求，可以创 [建模式XDM模式](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)。 如果您希望在中使用用户界 [!DNL Experience Platform]面， [模式编辑器教程](../../../../xdm/tutorials/create-schema-ui.md) 提供了在模式编辑器中执行类似操作的分步说明。
**API格式**

```http
POST /tenant/schemas
```

**请求**

以下示例请求创建一个扩展XDM类的XDM模式 [!DNL Individual Profile] 符。

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
        "title": "Target schema for protocols",
        "description": "Target schema for protocols",
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

成功的响应会返回新创建模式的详细信息，包括其唯一标识符(`$id`)。 后续步骤中需要此ID才能创建目标数据集、映射和数据流。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
    "meta:altId": "_{TENANT_ID}.schemas.e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Protocols target schema",
    "type": "object",
    "description": "Protocols target schema",
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
    "imsOrg": "7DC732555AECDB4C0A494036@AdobeOrg",
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

通过向Catalog Service API执行目标请求 [，提供有效负荷中POST模式的ID](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，可以创建目标数据集。

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
        "name": "Protocols target dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/e669d7aba5a02f294fafb7b269af25f7cd4a66ce59193545",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `schemaRef.id` | 目标 `$id` XDM模式。 |

**响应**

成功的响应会返回一个数组，其中包含格式为新创建数据集的ID `"@/datasets/{DATASET_ID}"`。 数据集ID是由系统生成的只读字符串，用于在API调用中引用数据集。 按照后续步骤中的要求存储目标数据集ID，以创建目标连接和数据流。

```json
[
    "@/dataSets/5e8a55ca53662c18af37a83a"
]
```

## 创建目标连接 {#target-connection}

目标连接表示到所摄取数据所进入的目的地的连接。 要创建目标连接，必须提供与数据库关联的固定连接规范ID。 此连接规范ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

您现在将唯一标识符作为目标模式目标集和连接规范ID到数据湖。 使用这些标识符，您可以使用API创建目标 [!DNL Flow Service] 连接，以指定将包含入站源数据的数据集。

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
            "id": "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `data.schema.id` | 目标 `$id` XDM模式。 |
| `params.dataSetId` | 目标数据集的ID。 |
| `connectionSpec.id` | 到数据湖的固定连接规范ID。 此ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

**响应**

成功的响应会返回新目标连接的唯一标识符(`id`)。 此值是后续步骤中创建数据流的必需值。

```json
{
    "id": "576d5ecf-f114-4587-ad5e-cff1144587f4",
    "etag": "\"13013506-0000-0200-0000-5e8a56d80000\""
}
```

## 创建映射 {#mapping}

为了将源数据引入目标数据集，必须首先将其映射到目标数据集所附加的目标模式。 这是通过对Conversion Service API执行POST请求 [来实现的](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mapping-service-api.yaml) ，该请求在请求有效负荷中定义了数据映射。

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
| `xdmSchema` | 目标 `$id` XDM模式。 |

**响应**

成功的响应会返回新创建的映射的详细信息，包括其唯一标识符(`id`)。 此ID是后续步骤中创建数据流的必需ID。

```json
{
    "id": "37409d3017e24a3eb4a2dc21020f7a5b",
    "version": 0,
    "createdDate": 1586124873209,
    "modifiedDate": 1586124873209,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## 查找数据流规范 {#specs}

数据流负责从源收集数据并将其引入 [!DNL Platform]。 要创建数据流，必须首先通过对API执行GET请求来获取数据流规 [!DNL Flow Service] 范。 数据流规范负责从外部协议应用程序收集数据。

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

成功的响应会返回数据流规范的详细信息，该规范负责将协议应用程序中的数据引入 [!DNL Platform]。 下一步中需要此ID才能创建新数据流。

```json
{
    "items": [
        {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "name": "CRMToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
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
                        "endTime": {
                            "description": "epoch time",
                            "type": "integer"
                        },
                        "interval": {
                            "type": "integer"
                        },
                        "frequency": {
                            "type": "string",
                            "enum": [
                                "minute",
                                "hour",
                                "day",
                                "week"
                            ]
                        },
                        "backfill": {
                            "type": "boolean",
                            "default": true
                        }
                    },
                    "required": [
                        "startTime",
                        "frequency",
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

要计划摄取，您必须首先将开始时间值设置为纪元时间（以秒为单位）。 然后，您必须将频率值设置为以下五个选项之一： `once`、 `minute`、 `hour`、 `day`或 `week`。 间隔值指定两个连续摄取之间的周期，并且创建一次摄取不需要设置间隔。 对于所有其他频率，间隔值必须设置为等于或大于 `15`。


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
| `flowSpec.id` | 在上 [一步中检索](#specs) 的流程规范ID。 |
| `sourceConnectionIds` | 在 [先前步骤中检索](#source) 的源连接ID。 |
| `targetConnectionIds` | 在 [先前步骤中检索](#target-connection) 的目标连接ID。 |
| `transformations.params.mappingId` | 在 [先前步骤](#mapping) 中检索的映射ID。 |
| `transformations.params.deltaColum` | 用于区分新数据和现有数据的指定列。 增量数据将根据所选列的时间戳被摄取。 使用通用OData时 `deltaColumn` 支持的格式为 `yyyy-MM-ddTHH:mm:ssZ`。 |
| `transformations.params.mappingId` | 与数据库关联的映射ID。 |
| `scheduleParams.startTime` | 开始时间中数据流的数据时间。 |
| `scheduleParams.frequency` | 数据流收集数据的频率。 可接受的值包括： `once`、 `minute`、 `hour`、 `day`或 `week`。 |
| `scheduleParams.interval` | 该间隔指定两个连续流运行之间的周期。 间隔的值应为非零整数。 当频率设置为时，间隔不 `once` 是必需的，对于其他频率值， `15` 应大于或等于。 |

**响应**

成功的响应会返回新 `id` 创建的数据流的ID。

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## 监视数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关流运行、完成状态和错误的信息。 有关如何监视数据流的详细信息，请参阅API中 [的数据流监视教程 ](../monitor.md)


## 后续步骤

通过遵循本教程，您已创建了一个源连接器来按计划从协议应用程序收集数据。 现在，下游服务（如和）可 [!DNL Platform] 以使用传入 [!DNL Real-time Customer Profile] 数据 [!DNL Data Science Workspace]。 有关更多详细信息，请参阅以下文档:

* [实时客户用户档案概述](../../../../profile/home.md)
* [数据科学工作区概述](../../../../data-science-workspace/home.md)
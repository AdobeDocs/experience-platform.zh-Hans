---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 通过源连接器和API收集营销自动化数据
topic: overview
translation-type: tm+mt
source-git-commit: 14d06635b3ed3c38bae3573a275dd37c990c280e
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 1%

---


# 通过源连接器和API收集营销自动化数据

Flow Service用于在Adobe Experience Platform内收集和集中来自不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程介绍从营销自动化系统检索数据并通过源连接器和API将其引入平台的步骤。

## 入门指南

本教程要求您通过有效的连接以及要引入平台的文件的相关信息（包括文件的路径和结构）来访问第三方营销自动化系统。 如果您没有此信息，请在尝试本教程 [之前参阅教程，了解如何使用流服务API](../explore/marketing-automation.md) ，探索第三方营销自动化系统。

本教程还要求您对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式注册开发人员指南](../../../../xdm/api/getting-started.md): 包括成功执行对模式注册表API的调用时需要了解的重要信息。 这包括您 `{TENANT_ID}`的、“容器”的概念以及发出请求所需的标题（特别要注意“接受”标题及其可能的值）。
* [目录服务](../../../../catalog/home.md): Catalog是Experience Platform中数据位置和世系的记录系统。
* [批量摄取](../../../../ingestion/batch-ingestion/overview.md): Batch Ingestion API允许您将数据作为批处理文件导入到Experience Platform中。
* [沙箱](../../../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和改进数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用Flow Service API成功连接到营销自动化系统。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的部分。

### 收集所需标题的值

要调用平台API，您必须先完成身份验证 [教程](../../../../tutorials/authentication.md)。 完成身份验证教程后，将提供所有Experience Platform API调用中每个所需标头的值，如下所示：

* 授权： 承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源（包括属于流服务的资源）都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* 内容类型： `application/json`

## 创建点对点XDM类和模式

要通过源连接器将外部数据引入平台，必须为原始源数据创建一个临时XDM类和模式。

要创建点对点类和模式，请按照点对点模式教 [程中概述的步骤操作](../../../../xdm/tutorials/ad-hoc.md)。 创建点对点类时，必须在请求主体中描述源数据中找到的所有字段。

继续按照开发人员指南中概述的步骤操作，直到您创建临时模式。 需要ad-`$id`hoc模式的唯一标识符()才能继续本教程的下一步。

## 创建源连接 {#source}

创建点对点XDM模式后，现在可以使用对流服务API的POST请求创建源连接。 源连接由连接ID、源数据文件和对描述源模式的引用组成。

要创建源连接，还必须为数据格式属性定义枚举值。

对基于文件的连接器使 **用以下枚举值**:

| Data.format | 枚举值 |
| ----------- | ---------- |
| 分隔文件 | `delimited` |
| JSON文件 | `json` |
| 镶木文件 | `parquet` |

对于所 **有基于表的连接器** ，请使用枚举值： `tabular`.

**API格式**

```https
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
        "name": "Source connection for marketing automation",
        "baseConnectionId": "c6d4ee17-6752-4e83-94ee-1767522e83fa",
        "description": "Source connection for a marketing automationj connector",
        "data": {
            "format": "tabular",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/5c65688f44feff94fe61cb3ae34de445fc885548b5ba5d57",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "Hubspot.Contacts"
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `baseConnectionId` | 您访问的第三方营销自动化系统的唯一连接ID。 |
| `data.schema.id` | 临时XDM模式的ID。 |
| `params.path` | 您正在访问的源文件的路径。 |
| `connectionSpec.id` | 营销自动化系统的连接规范ID。 |

**响应**

成功的响应会返回新创建的源`id`连接的唯一标识符()。 按照以后创建目标连接的步骤中的要求存储此值。

```json
{
    "id": "f44dbef2-a4f0-4978-8dbe-f2a4f0e978cf",
    "etag": "\"5f00fba7-0000-0200-0000-5ed560520000\""
}
```

## 创建目标XDM模式 {#target}

在前面的步骤中，创建了一个专门的XDM模式来构造源数据。 要在平台中使用源模式，还必须创建一个目标，以根据您的需求构建源数据。 然后，目标模式用于创建包含源数据的平台数据集。

通过对目标注册表API执行POST请求，可以创 [建模式XDM模式](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)。

如果您希望使用Experience Platform中的用户界面，模式编 [辑器教程提供了在模式编辑器中](../../../../xdm/tutorials/create-schema-ui.md) ，执行类似操作的分步说明。

**API格式**

```https
POST /schemaregistry/tenant/schemas
```

**请求**

以下示例请求创建一个XDM模式，它扩展了XDM单个用户档案类。

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
        "title": "Target schema for marketing automation",
        "description": "Target schema for marketing automation",
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

成功的响应会返回新创建模式的详细信息，包括其唯一标识符(`$id`)。 按照后续步骤中的要求存储此ID，以创建目标数据集、映射和数据流。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID/schemas/da411446eec78026c28d9fafd9e406e304b771d55b07b91b",
    "meta:altId": "_{TENANT_ID.schemas.da411446eec78026c28d9fafd9e406e304b771d55b07b91b",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for a marketing automation connector",
    "type": "object",
    "description": "Target schema for marketing automation",
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
        "repo:createdDate": 1591042937856,
        "repo:lastModifiedDate": 1591042937856,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "3f205600107156ffc394bef428e92cbe25b2faa34e15dd916c0d8bb58d9b7dd3",
        "meta:globalLibVersion": "1.10.4.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID"
}
```

## 创建目标数据集

通过对Catalog Service API执行POST请求，提供有效负 [荷内目标模式的ID](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，可以创建目标数据集。

**API格式**

```https
POST /catalog/dataSets
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
        "name": "Target dataset for a marketing automation connector",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/da411446eec78026c28d9fafd9e406e304b771d55b07b91b",
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
    "@/dataSets/5ed5639d798a22191b6987b2"
]
```

## 创建目标连接

目标连接表示到所摄取数据所进入的目的地的连接。 要创建目标连接，必须提供与数据库关联的固定连接规范ID。 此连接规范ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

您现在将唯一标识符作为目标模式目标集和连接规范ID到数据湖。 使用这些标识符，您可以使用流服务API创建目标连接，以指定将包含入站源数据的数据集。
**API格式**

```https
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
        "name": "Target Connection for a marketing automation connector",
        "description": "Target Connection for a marketing automation connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/da411446eec78026c28d9fafd9e406e304b771d55b07b91b",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5ed5639d798a22191b6987b2"
        },
            "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `data.schema.id` | 目标 `$id` XDM模式。 |
| `params.dataSetId` | 目标数据集的ID。 |
| `connectionSpec.id` | 到数据湖的固定连接规范ID。 此ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |

```json
{
    "id": "4b3d05d8-b7aa-40de-bd05-d8b7aa80de65",
    "etag": "\"dd00a1a2-0000-0200-0000-5ed564850000\""
}
```

## 创建映射 {#mapping}

为了将源数据引入目标数据集，必须首先将其映射到目标数据集所附加的目标模式。 这是通过在请求有效负荷中定义数据映射来执行对转换服务API的POST请求来实现的。

**API格式**

```https
POST /conversion/mappingSets
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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/da411446eec78026c28d9fafd9e406e304b771d55b07b91b",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Vid",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "Properties_Firstname_Value",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_repo.createDate",
                "sourceAttribute": "Added_At",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            }
        ]
    }'
```

| 属性 | 描述 |
| --- | --- |
| `xdmSchema` | 目标XDM模式的ID。 |

**响应**

成功的响应会返回新创建的映射的详细信息，包括其唯一标识符(`id`)。 按照后续步骤中创建数据流时的要求存储此值。

```json
{
    "id": "500a9b747fcf4908a21917d49bd61780",
    "version": 0,
    "createdDate": 1591043336298,
    "modifiedDate": 1591043336298,
    "createdBy": "28AF22BA5DE6B0B40A494036@AdobeID",
    "modifiedBy": "28AF22BA5DE6B0B40A494036@AdobeID"
}
```

## 查找数据流规范 {#specs}

数据流负责从源收集数据并将其引入平台。 要创建数据流，必须先获得负责收集营销自动化数据的数据流规范。

**API格式**

```https
GET /flowSpecs?property=name=="CRMToAEP"
```

**请求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CRMToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回数据流规范的详细信息，该规范负责将营销自动化系统的数据引入平台。 按照下一步 `id` 中创建新数据流时的要求存储字段值。

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

收集营销自动化数据的最后一步是创建数据流。 现在，您准备了以下必需值：

* [源连接ID](#source)
* [目标连接ID](#target)
* [映射ID](#mapping)
* [数据流规范ID](#specs)

数据流负责从源调度和收集数据。 您可以通过执行POST请求来创建数据流，同时在有效负荷中提供以前提到的值。

要计划摄取，您必须首先将开始时间值设置为纪元时间（以秒为单位）。 然后，您必须将频率值设置为以下五个选项之一： `once`、 `minute`、 `hour`、 `day`或 `week`。 间隔值指定两个连续摄取之间的周期，并且创建一次摄取不需要设置间隔。 对于所有其他频率，间隔值必须设置为等于或大于 `15`。

**API格式**

```https
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
        "name": "Dataflow for a marketing automation source",
        "description": "collecting Hubspot.Contacts",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "f44dbef2-a4f0-4978-8dbe-f2a4f0e978cf"
        ],
        "targetConnectionIds": [
            "4b3d05d8-b7aa-40de-bd05-d8b7aa80de65"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "deltaColumn": "date-time"
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "500a9b747fcf4908a21917d49bd61780",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1591043454",
            "frequency":"once",
            "interval":"15"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `flowSpec.id` | 在上一步中检索的流规范ID。 |
| `sourceConnectionIds` | 在先前步骤中检索的源连接ID。 |
| `targetConnectionIds` | 在之前的步骤中检索的目标连接ID。 |
| `transformations.params.mappingId` | 在先前步骤中检索的映射ID。 |
| `scheduleParams.startTime` | 开始数据流的时间（以秒为单位）。 |
| `scheduleParams.frequency` | 可选频率值包括： `once`、 `minute`、 `hour`、 `day`或 `week`。 |
| `scheduleParams.interval` | 该间隔指定两个连续流运行之间的周期。 间隔的值应为非零整数。 当频率设置为时，间隔不 `once` 是必需的，对于其他频率值， `15` 间隔应大于或等于。 |

**响应**

成功的响应会返回新创`id`建的数据流的ID()。

```json
{
    "id": "e0bd8463-0913-4ca1-bd84-6309134ca1f6",
    "etag": "\"04004fe9-0000-0200-0000-5ebc4c8b0000\""
}
```

## 后续步骤

按照本教程，您已创建了源连接器，以按计划从营销自动化系统收集数据。 现在，下游平台服务(如实时客户用户档案和数据科学工作区)可以使用传入数据。 有关更多详细信息，请参阅以下文档:

* [实时客户用户档案概述](../../../../profile/home.md)
* [数据科学工作区概述](../../../../data-science-workspace/home.md)
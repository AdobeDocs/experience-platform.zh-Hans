---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 通过源连接器和API收集云存储数据
topic: overview
translation-type: tm+mt
source-git-commit: 1eb6883ec9b78e5d4398bb762bba05a61c0f8308
workflow-type: tm+mt
source-wordcount: '1489'
ht-degree: 1%

---


# 通过源连接器和API收集云存储数据

本教程介绍从第三方云存储检索数据并通过源连接器和API将其引入平台的步骤。

## 入门指南

本教程要求您通过有效的基本连接以及要引入平台的文件的相关信息（包括文件的路径和结构）来访问第三方云存储。 如果您没有此信息，请参阅教程，在尝 [试本教程之前，使用流服务API探](../explore/cloud-storage.md) 索第三方云存储。

本教程还要求您对Adobe Experience Platform的以下组件有充分的了解：

- [体验数据模型(XDM)系统](../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
   - [模式合成基础](../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式注册开发人员指南](../../../../xdm/api/getting-started.md): 包括成功执行对模式注册表API的调用时需要了解的重要信息。 这包括您 `{TENANT_ID}`的、“容器”的概念以及发出请求所需的标题（特别要注意“接受”标题及其可能的值）。
- [目录服务](../../../../catalog/home.md): Catalog是Experience Platform中数据位置和世系的记录系统。
- [批量摄取](../../../../ingestion/batch-ingestion/overview.md): Batch Ingestion API允许您将数据作为批处理文件导入到Experience Platform中。
- [沙箱](../../../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和改进数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用流服务API成功连接到云存储。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的部分。

### 收集所需标题的值

要调用平台API，您必须先完成身份验证 [教程](../../../../tutorials/authentication.md)。 完成身份验证教程后，将提供所有Experience Platform API调用中每个所需标头的值，如下所示：

- 授权： 承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源（包括属于流服务的资源）都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

- 内容类型： `application/json`

## 创建点对点XDM类和模式

要通过源连接器将外部数据引入平台，必须为原始源数据创建一个临时XDM类和模式。

要创建点对点类和模式，请按照点对点模式教 [程中概述的步骤操作](../../../../xdm/tutorials/ad-hoc.md)。 创建点对点类时，必须在请求主体中描述源数据中找到的所有字段。

继续按照开发人员指南中概述的步骤操作，直到您创建临时模式。 获取并存储点对点模式`$id`的唯一标识符()，然后继续执行本教程的下一步。

## 创建源连接 {#source}

创建点对点XDM模式后，现在可以使用对流服务API的POST请求创建源连接。 源连接由基本连接、源数据文件和对描述源模式的引用组成。

**API格式**

```http
POST /sourceConnections
```

**请求**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Source Connection for a cloud storage",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "description": "Source Connection to ingest data.csv",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/140c03de81b959db95879033945cfd4c",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "/some/path/data.csv",
            "recursive": "true"
        },
        "connectionSpec": {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
    }'
```

| 属性 | 描述 |
| --- | --- |
| `baseConnectionId` | 云存储系统的基本连接的ID。 |
| `data.schema.id` | 临时XDM模式的ID。 |
| `params.path` | 源文件的路径。 |

**响应**

成功的响应会返回新创建的源`id`连接的唯一标识符()。 按照以后创建目标连接的步骤中的要求存储此值。

```json
{
    "id": "9a603322-19d2-4de9-89c6-c98bd54eb184"
}
```

## 创建目标XDM模式 {#target}

在前面的步骤中，创建了一个专门的XDM模式来构造源数据。 要在平台中使用源模式，还必须创建一个目标，以根据您的需求构建源数据。 然后，目标模式用于创建包含源数据的平台数据集。

如果您希望使用Experience Platform中的用户界面，模式编 [辑器教程提供了在模式编辑器中](../../../../xdm/tutorials/create-schema-ui.md) ，执行类似操作的分步说明。

**API格式**

```http
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
        "title": "Target schema for cloud storage source connector",
        "description": "",
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
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
    "meta:altId": "{TENANT_ID}.schemas.417a33eg81a221bd10495920574gfa2d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for cloud storage source connector",
    "description": "",
    "type": "object",
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
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "meta:containerId": "tenant",
    "meta:registryMetadata": {
        "eTag": "6m/FrIlXYU2+yH6idbcmQhKSlMo="
    }
}
```

## 创建目标数据集

通过对Catalog Service API执行POST请求，提供有效负荷中目标模式的ID，可以创建目标数据集。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Target Dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `schemaRef.id` | 目标XDM模式的ID。 |

**响应**

成功的响应会返回一个数组，其中包含格式为新创建数据集的ID `"@/datasets/{DATASET_ID}"`。 数据集ID是由系统生成的只读字符串，用于在API调用中引用数据集。 按照后续步骤中的要求存储目标数据集ID，以创建目标连接和数据流。

```json
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## 创建数据集基础连接

为了将外部数据引入Platform，必须先获取Experience Platform数据集基础连接。

要创建数据集基础连接，请按照数据集基础连接教 [程中概述的步骤操作](../create-dataset-base-connection.md)。

继续按照开发人员指南中所述的步骤操作，直到您创建了数据集基础连接。 获取并存储唯一标识符(`$id`)，然后在下一步中继续将它用作基本连接ID以创建目标连接。

## 创建目标连接

您现在具有数据集基础连接、目标模式和目标数据集的唯一标识符。 使用这些标识符，您可以使用流服务API创建目标连接，以指定将包含入站源数据的数据集。

**API格式**

```http
POST /targetConnections
```

**请求**

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "baseConnectionId": "d6c3988d-14ef-4000-8398-8d14ef000021",
        "name": "Target Connection",
        "description": "Target Connection for cloud storage data",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5c8c3c555033b814b69f947f"
        },
        "connectionSpec": {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `baseConnectionId` | 数据集基础连接的ID。 |
| `data.schema.id` | 目标 `$id` XDM模式。 |
| `params.dataSetId` | 目标数据集的ID。 |
| `connectionSpec.id` | 云存储的连接规范ID。 |

>[!NOTE] 创建目标连接时，请确保将Data Lake基连接值用于基连接，而 `id` 非第三方源连接器的基连接。

**响应**

成功的响应会返回新目标连接的唯一标识符(`id`)。 按照后续步骤中的要求存储此值。

```json
{
    "id": "4ee890c7-519c-4291-bd20-d64186b62da8",
    "etag": "\"2a007aa8-0000-0200-0000-5e597aaf0000\""
}
```

## 创建映射 {#mapping}

为了将源数据引入目标数据集，必须首先将其映射到目标数据集所附加的目标模式。 这是通过对转换服务执行POST请求来实现的，其中数据映射在请求有效负荷中定义。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name.firstName",
                "sourceAttribute": "FirstName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "person.name.lastName",
                "sourceAttribute": "LastName",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "mobilePhone.number",
                "sourceAttribute": "Phone",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "personalEmail.address",
                "sourceAttribute": "Email",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
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
    "id": "ab91c736-1f3d-4b09-8424-311d3d3e3cea",
    "version": 1,
    "createdDate": 1568047685000,
    "modifiedDate": 1568047703000,
    "inputSchemaRef": {
        "id": null,
        "contentType": null
    },
    "outputSchemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/417a33eg81a221bd10495920574gfa2d",
        "contentType": "1.0"
    },
    "mappings": [
        {
            "id": "7bbea5c0f0ef498aa20aa2e2e5c22290",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "Id",
            "destination": "_id",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "Id",
            "destinationXdmPath": "_id"
        },
        {
            "id": "def7fd7db2244f618d072e8315f59c05",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "FirstName",
            "destination": "person.name.firstName",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "FirstName",
            "destinationXdmPath": "person.name.firstName"
        },
        {
            "id": "e974986b28c74ed8837570f421d0b2f4",
            "version": 0,
            "createdDate": 1568047685000,
            "modifiedDate": 1568047685000,
            "sourceType": "text/x.schema-path",
            "source": "LastName",
            "destination": "person.name.lastName",
            "identity": false,
            "primaryIdentity": false,
            "matchScore": 0.0,
            "sourceAttribute": "LastName",
            "destinationXdmPath": "person.name.lastName"
        }
    ],
    "status": "PUBLISHED",
    "xdmVersion": "1.0",
    "schemaRef": {
        "id": "https://ns.adobe.com/adobe_mcdp_connectors_stg/schemas/2574494fdb01fa14c25b52d717ccb828",
        "contentType": "1.0"
    },
    "xdmSchema": "https://ns.adobe.com/adobe_mcdp_connectors_stg/schemas/2574494fdb01fa14c25b52d717ccb828"
}
```

## 检索数据流规范 {#specs}

数据流负责从源收集数据并将其引入平台。 要创建数据流，必须先获取负责收集云存储数据的数据流规范。

**API格式**

```http
GET /flowSpecs?property=name=="CloudStorageToAEP"
```

**请求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回数据流规范的详细信息，该规范负责将来自您的云存储的数据引入平台。 按照下一步 `id` 中创建新数据流时的要求存储字段值。

```json
{
    "items": [
        {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "name": "CloudStorageToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
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

收集云存储数据的最后一步是创建数据流。 现在，您准备了以下必需值：

- [源连接ID](#source)
- [目标连接ID](#target)
- [映射ID](#mapping)
- [数据流规范ID](#specs)

数据流负责从源调度和收集数据。 您可以通过执行POST请求来创建数据流，同时在有效负荷中提供以前提到的值。

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
        "name": "Dataflow between cloud storage and Platform",
        "description": "collecting data.csv",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "9a603322-19d2-4de9-89c6-c98bd54eb184"
        ],
        "targetConnectionIds": [
            "4ee890c7-519c-4291-bd20-d64186b62da8"
        ],
        "transformations": [
            {
                "name": "Copy",
                "params": {
                    "mode": "append"
                }
            },
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "ab91c736-1f3d-4b09-8424-311d3d3e3cea"
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
| --- | --- |
| `flowSpec.id` | 数据流规范ID |
| `sourceConnectionIds` | 源连接ID |
| `targetConnectionIds` | 目标连接ID |
| `transformations.params.mappingId` | 映射ID |

**响应**

成功的响应会返回新创`id`建的数据流的ID()。

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```

## 后续步骤

通过遵循本教程，您已创建了源连接器，以按计划从您的云存储收集数据。 现在，下游平台服务(如实时客户用户档案和数据科学工作区)可以使用传入数据。 有关更多详细信息，请参阅以下文档:

- [实时客户用户档案概述](../../../../profile/home.md)
- [数据科学工作区概述](../../../../data-science-workspace/home.md)

## 附录

以下部分列表不同的云存储源连接器及其连接规范。

### 连接规范

| 连接器名称 | 连接规范 |
| -------------- | --------------- |
| Amazon S3(S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| Amazon Kinesis(Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| Azure Blob(Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| Azure Data Lake存储Gen2(ADLS Gen2) | `0ed90a81-07f4-4586-8190-b40eccef1c5a` |
| Azure事件集线器(EventHub) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| Google Cloud存储 | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| SFTP | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |
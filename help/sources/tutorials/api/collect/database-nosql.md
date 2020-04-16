---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 通过源连接器和API从外部数据库或NoSQL系统收集数据
topic: overview
translation-type: tm+mt
source-git-commit: 00764a59629eb8a5a06ac28ad446084b0bdb2293

---


# 通过源连接器和API从外部数据库或NoSQL系统收集数据

Flow Service用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程介绍了从数据库或NoSQL系统检索数据并通过源连接器和API将其引入平台的步骤。

## 入门指南

本教程要求您通过有效的基本连接访问第三方数据库或NoSQL系统，并了解要引入平台的文件的相关信息，包括文件的路径和结构。 如果您没有此信息，请参阅教程，在尝 [试本教程之前，使用Flow Service API浏览数据库或NoSQL系统](../explore/database-nosql.md) 。

本教程还要求您对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成的基础知识](../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式注册开发人员指南](../../../../xdm/api/getting-started.md):包括成功执行对模式注册表API的调用所需了解的重要信息。 这包括您 `{TENANT_ID}`的“容器”概念以及发出请求所需的标题（特别注意“接受”标题及其可能的值）。
* [目录服务](../../../../catalog/home.md):Catalog是Experience Platform中用于数据位置和世系的记录系统。
* [批量摄取](../../../../ingestion/batch-ingestion/overview.md):Batch Ingestion API允许您将数据作为批处理文件导入到Experience Platform中。
* [沙箱](../../../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供了使用Flow Service API成功连接到数据库或NoSQL系统时需要了解的其他信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

* 授权：承载人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源（包括属于Flow Service的资源）都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标题：

* 内容类型： `application/json`

## 创建点对点XDM类和模式

要通过源连接器将外部数据引入平台，必须为原始源数据创建一个专门的XDM类和模式。

要创建点对点类和模式，请按照点对点模式教程中 [概述的步骤操作](../../../../xdm/tutorials/ad-hoc.md)。 创建点对点类时，在源数据中找到的所有字段都必须在请求主体中进行说明。

继续按照开发人员指南中所述的步骤操作，直到您创建临时模式。 获取并存储ad-hoc模式的唯一标识符(`$id`)，然后继续执行本教程的下一步。

## 创建源连接 {#source}

创建点对点XDM模式后，现在可以使用对Flow Service API的POST请求创建源连接。 源连接由基本连接、源数据文件和对描述源数据的模式的引用组成。

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
        "name": "Source Connection for database or NoSQL",
        "baseConnectionId": "54c22133-3a01-4d3b-8221-333a01bd3b03",
        "description": "Source Connection for database or NoSQL to ingest test1.Mytable",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c8c2b32d6f6a53d5ffc7212c37b3a9369282404a7bd551e8",
                "version": "application/vnd.adobe.xed-full-notext+json; version=1"
            }
        },
        "params": {
            "path": "test1.Mytable"
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
}'
```

| 属性 | 描述 |
| -------- | ----------- |
| `baseConnectionId` | 数据库或NoSQL系统的基本连接的ID。 |
| `data.schema.id` | 临 `$id` 时XDM模式。 |
| `params.path` | 源文件的路径。 |
| `connectionSpec.id` | 数据库或NoSQL系统的连接规范ID。 |

**响应**

成功的响应会返回新创建的源连接的唯`id`一标识符()。 此ID是后续步骤中创建目标连接时必需的。

```json
{
    "id": "beefc650-f2dc-45e2-afc6-50f2dcc5e2b8",
    "etag": "\"1600f153-0000-0200-0000-5e4710880000\""
}
```

## 创建目标XDM模式 {#target}

在前面的步骤中，创建了一个专门的XDM模式来构造源数据。 为了使源数据在平台中使用，还必须创建目标模式，以根据您的需求构建源数据。 然后，目标模式用于创建包含源数据的平台数据集。 此目标XDM模式还扩展了XDM单个用户档案类。

通过对目标注册表API执行POST请求，可以创建 [模式XDM模式](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)。 如果您希望使用Experience Platform中的用户界面， [模式编辑器教程将提供在模式编辑器中执行类似操作的分步说明](../../../../xdm/tutorials/create-schema-ui.md) 。

**API格式**

```http
POST /tenant/schemas
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
        "title": "Target schema for database or NoSQL",
        "description": "Target schema for database or NoSQL",
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
    }'
```

**响应**

成功的响应返回新创建的模式的详细信息，包括其唯一标识符(`$id`)。 后续步骤中需要此ID才能创建目标数据集、映射和数据流。

```json
{
    "$id": "https://ns.adobe.com/{TENANT}/schemas/a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
    "meta:altId": "_{TENANT}.schemas.a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema for database or NoSQL",
    "type": "object",
    "description": "Target schema for database or NoSQL",
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
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/common/extensible"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1581716110281,
        "repo:lastModifiedDate": 1581716110281,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "6360f2175b40462ff25ec8735dc93a7e3af6a8faadd80a1cc500a59721e1a424"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "{TENANT_ID}"
}
```

## 创建目标数据集

通过向 [Catalog Service API执行POST请求](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，提供有效负荷内目标模式的ID，可以创建目标数据集。

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
        "name": "Target Dataset for database or NoSQL",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `schemaRef.id` | 目标XDM模式的ID。 |

**响应**

成功的响应会返回一个数组，其中包含格式中新创建的数据集的ID `"@/datasets/{DATASET_ID}"`。 数据集ID是系统生成的只读字符串，用于在API调用中引用数据集。 按照后续步骤中的要求存储目标数据集ID，以创建目标连接和数据流。

```json
[
    "@/dataSets/5e47161fa49bb818ad7f47bd"
]
```

## 创建数据集基础连接

为了将外部数据引入Platform中，必须首先获取Experience Platform数据集基础连接。

要创建数据集基础连接，请按照数据集基础连接教 [程中所述的步骤操作](../create-dataset-base-connection.md)。

继续按照开发人员指南中所述的步骤操作，直到您创建了数据集基础连接。 获取并存储唯一标识符(`$id`)，然后在下一步中继续将其用作基本连接ID以创建目标连接。

## 创建目标连接

您现在具有数据集基础连接、目标模式和目标数据集的唯一标识符。 使用这些标识符，您可以使用Flow Service API创建目标连接，以指定将包含入站源数据的数据集。

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
        "baseConnectionId": "d6c3988d-14ef-4000-8398-8d14ef000021",
        "name": "Target Connection for database or NoSQL",
        "description": "Target Connection for database or NoSQL",
        "data": {
            "format": "parquet_xdm",
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5e47161fa49bb818ad7f47bd"
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `baseConnectionId` | 数据集基础连接的ID。 |
| `data.schema.id` | 目标 `$id` XDM模式。 |
| `params.dataSetId` | 目标数据集的ID。 |
| `connectionSpec.id` | 第三方数据库的连接规范ID。 |

>[!NOTE] 创建目标连接时，请确保将数据集基本连接值用于基本连接，而不是第 `id` 三方源连接器的基本连接。

**响应**

成功的响应会返回新目标连接的唯一标识符(`id`)。 此值是后续步骤中创建数据流所必需的。

```json
{
    "id": "4f3845b6-87d9-4702-b845-b687d9270297",
    "etag": "\"2a007aa8-0000-0200-0000-5e597aaf0000\""
}
```

## 创建映射 {#mapping}

为了将源数据引入目标数据集，必须首先将其映射到目标数据集所附加的目标模式。 这是通过对转换服务API执行POST请求而实现的，该POST请求在请求有效负荷中定义了数据映射。

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/a9d63c5e3fab2687e064577959d0b91e274823f91f2f578e",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "person.name",
                "sourceAttribute": "Name",
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
                "sourceAttribute": "email",
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

成功的响应返回新创建的映射的详细信息，包括其唯一标识符(`id`)。 以后的步骤中需要此ID才能创建数据流。

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
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/efea012ad5deefcdf51afd23ceb3583f",
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
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2574494fdb01fa14c25b52d717ccb828",
        "contentType": "1.0"
    },
    "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2574494fdb01fa14c25b52d717ccb828"
}
```

## 查找数据流规范 {#specs}

数据流负责从源收集数据并将其引入平台。 要创建数据流，必须首先通过对Flow Service API执行GET请求来获取数据流规范。 数据流规范负责从外部数据库或NoSQL系统收集数据。

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

成功的响应会返回数据流规范的详细信息，该规范负责将数据库或NoSQL系统的数据引入平台。 下一步中需要此ID才能创建新数据流。

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
        "name": "Dataflow between database or NoSQL Platform",
        "description": "Inbound data to Platform",
        "flowSpec": {
            "id": "14518937-270c-4525-bdec-c2ba7cce3860",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "beefc650-f2dc-45e2-afc6-50f2dcc5e2b8"
        ],
        "targetConnectionIds": [
            "4f3845b6-87d9-4702-b845-b687d9270297"
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
                    "mappingId": "ab91c736-1f3d-4b09-8424-311d3d3e3cea",
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
| `flowSpec.id` | 与数据库或NoSQL系统关联的数据流规范ID。 |
| `sourceConnectionIds` | 与数据库或NoSQL系统关联的源连接ID。 |
| `targetConnectionIds` | 与数据库或NoSQL系统关联的目标连接ID。 |
| `transformations.params.mappingId` | 与数据库或NoSQL系统关联的映射ID。 |

**响应**

成功的响应会返回新创建`id`的数据流的ID()。

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```

## 后续步骤

按照本教程，您已创建了一个源连接器，以按计划从数据库或NoSQL系统收集数据。 现在，下游平台服务(如实时客户用户档案和数据科学工作区)可以使用传入的数据。 有关更多详细信息，请参阅以下文档:

* [实时客户用户档案概述](../../../../profile/home.md)
* [数据科学工作区概述](../../../../data-science-workspace/home.md)
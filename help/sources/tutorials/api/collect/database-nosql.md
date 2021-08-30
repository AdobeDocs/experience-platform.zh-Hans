---
keywords: Experience Platform；主页；热门主题；数据库数据库；第三方数据库
solution: Experience Platform
title: 使用源连接器和API从数据库收集数据
topic-legacy: overview
type: Tutorial
description: 本教程介绍使用源连接器和API从数据库检索数据并将其摄取到平台中的步骤。
exl-id: 1e1f9bbe-eb5e-40fb-a03c-52df957cb683
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 1%

---

# 使用源连接器和API从数据库收集数据

本教程介绍从第三方数据库检索数据并通过源连接器和[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)将其摄取到平台中的步骤。

## 快速入门

本教程要求您拥有与数据库的有效连接，以及有关要引入平台的文件（包括文件的路径和结构）的信息。 如果您没有此信息，请参阅教程中的[使用流服务API](../explore/database-nosql.md)浏览数据库，然后再尝试使用本教程。

此外，本教程还要求您对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [架构注册开发人员指南](../../../../xdm/api/getting-started.md):包括成功调用架构注册表API所需了解的重要信息。这包括您的`{TENANT_ID}`、“容器”的概念以及发出请求所需的标头（请特别注意“接受”标头及其可能值）。
* [[!DNL Catalog Service]](../../../../catalog/home.md):目录是Experience Platform中数据位置和谱系的记录系统。
* [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md):批量摄取API允许您将数据作为批处理文件导入到Experience Platform中。
* [沙盒](../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下各节提供了您需要了解的其他信息，以便您能够使用[[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API成功连接到第三方数据库。

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中[如何阅读示例API调用](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

### 收集所需标题的值

要调用Platform API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程可为所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Experience Platform中的所有资源（包括属于[!DNL Flow Service]的资源）都与特定虚拟沙箱隔离。 对Platform API的所有请求都需要一个标头来指定操作将在其中进行的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 创建源连接 {#source}

您可以通过向[!DNL Flow Service] API发出POST请求来创建源连接。 源连接由连接ID、源数据文件的路径和连接规范ID组成。

要创建源连接，还必须为数据格式属性定义枚举值。

对基于文件的连接器使用以下枚举值：

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
        "name": "Database source connection",
        "baseConnectionId": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
        "description": "Database source connection",
        "data": {
            "format": "tabular"
        },
        "params": {
            "tableName": "test1.Mytable",
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
            ]
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `baseConnectionId` | 数据库源的连接ID。 |
| `params.path` | 源文件的路径。 |
| `connectionSpec.id` | 数据库源的连接规范ID。 有关数据库规范ID的列表，请参阅[附录](#appendix)。 |

**响应**

成功的响应会返回新创建源连接的唯一标识符(`id`)。 在后续步骤中需要此ID才能创建目标连接。

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## 创建目标XDM架构 {#target-schema}

要在Platform中使用源数据，必须创建目标XDM架构以根据您的需求构建源数据。 然后，使用目标XDM架构创建包含源数据的Platform数据集。 此目标XDM架构还扩展了[!DNL XDM Individual Profile]类。

通过对[架构注册表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)执行POST请求，可以创建目标XDM架构。

**API格式**

```http
POST /tenant/schemas
```

**请求**

以下示例请求创建一个XDM架构，用于扩展XDM [!DNL Individual Profile]类。

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
        "title": "Database target XDM schema",
        "description": "Database target XDM schema",
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

成功的响应会返回新创建架构的详细信息，包括其唯一标识符(`$id`)。 在后续步骤中需要此ID才能创建目标数据集、映射和数据流。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
    "meta:altId": "_{TENANT_ID}.schemas.52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Database target XDM schema",
    "type": "object",
    "description": "Database target XDM schema",
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
        "repo:createdDate": 1612308675206,
        "repo:lastModifiedDate": 1612308675206,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{MODIFIEDD_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "7c5c09e62421e6b172c925f059ac524a99f348dd837b5f13abd77ee91aa6bb61",
        "meta:globalLibVersion": "1.18.4"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "{SANDBOX_ID}",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 创建目标数据集

通过向[Catalog Service API](https://www.adobe.io/experience-platform-apis/references/catalog/)执行POST请求，并提供有效负载中目标架构的ID，可以创建目标数据集。

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
        "name": "Database target dataset",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `schemaRef.id` | 目标XDM架构的ID。 |
| `schemaRef.contentType` | 架构的版本。 此值必须设置为`application/vnd.adobe.xed-full-notext+json;version=1`，这将返回架构的最新次要版本。 |

**响应**

成功的响应会返回一个数组，其中包含格式为`"@/datasets/{DATASET_ID}"`的新创建数据集的ID。 数据集ID是由系统生成的只读字符串，用于在API调用中引用数据集。 按照后续步骤创建目标连接和数据流所需的方式存储目标数据集ID。

```json
[
    "@/dataSets/6019e0e7c5dcf718db5ebc71"
]
```

## 创建目标连接 {#target-connection}

目标连接表示所摄取数据所登陆目标的连接。 要创建目标连接，必须提供与数据湖关联的固定连接规范ID。 此连接规范ID为：`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

现在，您的唯一标识符是目标架构（目标数据集）以及与数据湖的连接规范ID。 使用[!DNL Flow Service] API，您可以通过指定这些标识符以及将包含入站源数据的数据集来创建目标连接。

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
        "name": "Database target connection",
        "description": "Database target connection",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
                "version": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "params": {
            "dataSetId": "6019e0e7c5dcf718db5ebc71"
        },
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `data.schema.id` | 目标XDM架构的`$id`。 |
| `data.schema.version` | 架构的版本。 此值必须设置为`application/vnd.adobe.xed-full+json;version=1`，这将返回架构的最新次要版本。 |
| `params.dataSetId` | 在上一步中收集的目标数据集的ID。 |
| `connectionSpec.id` | 用于连接到数据湖的连接规范ID。 此ID为：`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |

**响应**

成功的响应会返回新目标连接的唯一标识符(`id`)。 在后续步骤中需要此值才能创建数据流。

```json
{
    "id": "320f119a-5ac1-4ab1-88ea-eb19e674ea2e",
    "etag": "\"c0038936-0000-0200-0000-6019e1190000\""
}
```

## 创建映射 {#mapping}

要将源数据摄取到目标数据集，必须首先将其映射到目标数据集所遵循的目标架构。 这是通过向[!DNL Conversion Service] API执行POST请求来实现的，该API具有在请求负载中定义的数据映射。

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

成功的响应会返回新创建映射的详细信息，包括其唯一标识符(`id`)。 在后续步骤中需要此ID才能创建数据流。

```json
{
    "id": "0b090130b58b4819afc78b6dc98b484d",
    "version": 0,
    "createdDate": 1612309018666,
    "modifiedDate": 1612309018666,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 检索数据流规范 {#specs}

数据流负责从源中收集数据并将它们引入平台。 要创建数据流，必须首先通过向[[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) API执行GET请求来获取数据流规范。 数据流规范负责从外部数据库或NoSQL系统中收集数据。

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

成功的响应会返回负责将数据从源引入平台的数据流规范的详细信息。 响应包含创建新数据流所需的唯一流程规范`id`。

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
* [Target连接ID](#target)
* [映射ID](#mapping)
* [数据流规范ID](#specs)

数据流负责从源中调度和收集数据。 您可以通过执行POST请求来创建数据流，同时在请求负载中提供之前提到的值。

要计划摄取，您必须首先将开始时间值设置为以秒为单位的新纪元时间。 然后，您必须将频率值设置为以下五个选项之一：`once`、`minute`、`hour`、`day`或`week`。 间隔值可指定两个连续摄取和创建一次性摄取之间的周期，而无需设置间隔。 对于所有其他频率，间隔值必须设置为等于或大于`15`。

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
        "name": "Database dataflow using BigQuery",
        "description": "collecting test1.Mytable",
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
                    "mappingId": "0b090130b58b4819afc78b6dc98b484d",
                    "mappingVersion": "0"
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
| -------- | ----------- |
| `flowSpec.id` | 在上一步骤中检索到的[流量规范ID](#specs)。 |
| `sourceConnectionIds` | 在前面的步骤中检索到的[源连接ID](#source)。 |
| `targetConnectionIds` | 在前面的步骤中检索到的[目标连接ID](#target-connection)。 |
| `transformations.params.mappingId` | 在前面的步骤中检索到的[映射ID](#mapping)。 |
| `transformations.params.deltaColum` | 用于区分新数据和现有数据的指定列。 将根据选定列的时间戳摄取增量数据。 `deltaColumn`支持的日期格式为`yyyy-MM-dd HH:mm:ss`。 如果您使用Azure表存储，则`deltaColumn`支持的格式为`yyyy-MM-ddTHH:mm:ssZ`。 |
| `transformations.params.mappingId` | 与数据库关联的映射ID。 |
| `scheduleParams.startTime` | 新纪元时间中数据流的开始时间。 |
| `scheduleParams.frequency` | 数据流收集数据的频率。 可接受的值包括：`once`、`minute`、`hour`、`day`或`week`。 |
| `scheduleParams.interval` | 该间隔指定两个连续流运行之间的周期。 间隔的值应为非零整数。 当频率设置为`once`时，不需要间隔，对于其他频率值，间隔应大于或等于`15`。 |

**响应**

成功的响应会返回新创建数据流的ID(`id`)。

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## 监控数据流

创建数据流后，您可以监视通过其摄取的数据，以查看有关流量运行、完成状态和错误的信息。 有关如何监视数据流的更多信息，请参阅关于[在API ](../monitor.md)中监视数据流的教程

## 后续步骤

在本教程中，您创建了一个源连接器，用于按计划从数据库收集数据。 现在，下游Platform服务（如[!DNL Real-time Customer Profile]和[!DNL Data Science Workspace]）可以使用传入数据。 有关更多详细信息，请参阅以下文档：

* [实时客户资料概述](../../../../profile/home.md)
* [数据科学工作区概述](../../../../data-science-workspace/home.md)

## 附录

以下部分列出了不同的云存储源连接器及其连接规范。

### 连接规范

| 连接器名称 | 连接规范ID |
| -------------- | --------------- |
| [!DNL Amazon Redshift] | `3416976c-a9ca-4bba-901a-1f08f66978ff` |
| [!DNL Apache Hive] on  [!DNL Azure HDInsights] | `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |
| [!DNL Apache Spark] on  [!DNL Azure HDInsights] | `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |
| [!DNL Azure Data Explorer] | `0479cc14-7651-4354-b233-7480606c2ac3` |
| [!DNL Azure Synapse Analytics] | `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` |
| [!DNL Azure Table Storage] | `ecde33f2-c56f-46cc-bdea-ad151c16cd69` |
| [!DNL Couchbase] | `1fe283f6-9bec-11ea-bb37-0242ac130002` |
| [!DNL Google BigQuery] | `3c9b37f8-13a6-43d8-bad3-b863b941fedd` |
| [!DNL Greenplum] | `37b6bf40-d318-4655-90be-5cd6f65d334b` |
| [!DNL IBM DB2] | `09182899-b429-40c9-a15a-bf3ddbc8ced7` |
| [!DNL MariaDB] | `000eb99-cd47-43f3-827c-43caf170f015` |
| [!DNL Microsoft SQL Server] | `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec` |
| [!DNL MySQL] | `26d738e0-8963-47ea-aadf-c60de735468a` |
| [!DNL Oracle] | `d6b52d86-f0f8-475f-89d4-ce54c8527328` |
| [!DNL Phoenix] | `102706fb-a5cd-42ee-afe0-bc42f017ff43` |
| [!DNL PostgreSQL] | `74a1c565-4e59-48d7-9d67-7c03b8a13137` |

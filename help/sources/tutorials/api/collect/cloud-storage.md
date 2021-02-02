---
keywords: Experience Platform；主页；热门主题；云存储数据
solution: Experience Platform
title: 通过源连接器和API收集云存储数据
topic: overview
type: Tutorial
description: 本教程介绍从第三方云存储检索数据并通过源连接器和API将其引入平台的步骤。
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '1621'
ht-degree: 1%

---


# 通过源连接器和API收集云存储数据

本教程介绍从第三方云存储检索数据并通过源连接器和[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)将其引入平台的步骤。

## 入门指南

本教程要求您通过有效的连接以及要引入平台的文件的相关信息（包括文件的路径和结构）来访问第三方云存储。 如果您没有此信息，请参阅教程中的[使用 [!DNL Flow Service] API](../explore/cloud-storage.md)探索第三方云存储，然后再尝试本教程。

本教程还要求您对Adobe Experience Platform的以下组件有充分的了解：

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   - [模式合成基础](../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式注册开发人员指南](../../../../xdm/api/getting-started.md):包括成功执行对模式注册表API的调用时需要了解的重要信息。这包括您的`{TENANT_ID}`、“容器”的概念以及发出请求所需的标头（特别要注意“接受”标头及其可能的值）。
- [[!DNL Catalog Service]](../../../../catalog/home.md):目录是Experience Platform内数据位置和谱系的记录系统。
- [[!DNL Batch ingestion]](../../../../ingestion/batch-ingestion/overview.md):批处理摄取API允许您将数据作为批处理文件导入到Experience Platform中。
- [沙箱](../../../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个平台实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。以下各节提供了使用[!DNL Flow Service] API成功连接到云存储所需的其他信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中的[如何阅读示例API调用](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

### 收集所需标题的值

要调用平台API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程将提供所有Experience PlatformAPI调用中每个所需标头的值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Experience Platform中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

- `Content-Type: application/json`

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

>[!NOTE]
>
>您可以通过将列分隔符指定为属性，使用云存储源连接器收录CSV和TSV文件。 任何单个字符值都是允许的列分隔符。 如果未提供，则使用逗号`(,)`作为默认值。

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
        "name": "Cloud storage source connector",
        "connectionId": "9e2541a0-b143-4d23-a541-a0b143dd2301",
        "description": "Cloud storage source connector",
        "data": {
            "format": "delimited",
            "columnDelimiter": "\t"
        },
        "params": {
            "path": "/ingestion-demos/leads/tsv_data/*.tsv",
            "recursive": "true"
        },
            "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `connectionId` | 您正在访问的第三方云存储系统的唯一连接ID。 |
| `data.format` | 定义数据格式属性的枚举值。 |
| `data.columnDelimiter` | 可使用任何单字符列分隔符收集平面文件。 仅当引入CSV或TSV文件时，才需要此属性。 |
| `params.path` | 您正在访问的源文件的路径。 |
| `connectionSpec.id` | 与特定第三方云存储系统关联的连接规范ID。 有关连接规范ID的列表，请参见[附录](#appendix)。 |

**响应**

成功的响应会返回新创建的源连接的唯一标识符(`id`)。 此ID是后续步骤中创建数据流的必需ID。

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## 创建目标XDM模式{#target-schema}

要在平台中使用源模式，必须创建一个目标，以根据您的需求构建源数据。 然后，目标模式用于创建包含源数据的平台数据集。

通过对[目标注册表API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)执行POST请求，可以创建模式XDM模式。

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
        "title": "Target schema for a Cloud Storage connector",
        "description": "Target schema for a Cloud Storage connector",
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
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
    "meta:altId": "_{TENANT_ID}.schemas.995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "Target schema cloud storage",
    "type": "object",
    "description": "Target schema for cloud storage",
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
        "repo:createdDate": 1597783248870,
        "repo:lastModifiedDate": 1597783248870,
        "xdm:createdClientId": "{CREATED_CLIENT_ID}",
        "xdm:lastModifiedClientId": "{LAST_MODIFIED_CLIENT_ID}",
        "xdm:createdUserId": "{CREATED_USER_ID}",
        "xdm:lastModifiedUserId": "{LAST_MODIFIED_USER_ID}",
        "eTag": "596661ec6c7a9c6ae530676e98290a4a58ca29540ed92489cf4478b2bf013a65",
        "meta:globalLibVersion": "1.13.3"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "{TENANT_ID}"
}
```

## 创建目标数据集

通过向[目录服务API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)执行目标请求，提供有效负荷内目标模式的ID，可以创建POST数据集。

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
        "name": "Target dataset for cloud storage",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `schemaRef.id` | 目标XDM模式的ID。 |

**响应**

成功的响应返回一个数组，其中包含格式为`"@/datasets/{DATASET_ID}"`的新创建数据集的ID。 数据集ID是由系统生成的只读字符串，用于在API调用中引用数据集。 目标数据集ID是后续步骤中创建目标连接和数据流所必需的。

```json
[
    "@/dataSets/5f3c3cedb2805c194ff0b69a"
]
```

## 创建目标连接{#target-connection}

目标连接表示到所摄取数据所进入的目的地的连接。 要创建目标连接，必须提供与数据湖关联的固定连接规范ID。 此连接规范ID为：`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

您现在将唯一标识符作为目标模式目标集和连接规范ID到数据湖。 使用这些标识符，您可以使用[!DNL Flow Service] API创建目标连接，以指定将包含入站源数据的数据集。

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
        "name": "Target Connection for a Cloud Storage connector",
        "description": "Target Connection for a Cloud Storage connector",
        "data": {
            "schema": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
                "version": "application/vnd.adobe.xed-full+json;version=1.0"
            }
        },
        "params": {
            "dataSetId": "5f3c3cedb2805c194ff0b69a"
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
| `connectionSpec.id` | 到数据湖的固定连接规范ID。 此ID为：`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |

**响应**

成功的响应会返回新目标连接的唯一标识符(`id`)。 此ID是后续步骤中必需的。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 创建映射{#mapping}

为了将源数据引入目标数据集，必须首先将其映射到目标数据集所附加的目标模式。 这是通过对转换服务执行POST请求来实现的，该请求具有在请求有效负荷中定义的数据映射。

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
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "id": null,
        "mappings": [
            {
                "destinationXdmPath": "_id",
                "sourceAttribute": "Id",
                "identity": false,
                "identityGroup": null,
                "namespaceCode": null,
                "version": 0
            },
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
            }
        ]
    }'
```

| 属性 | 描述 |
| --- | --- |
| `xdmSchema` | 目标XDM模式的ID。 |

**响应**

成功的响应返回新创建的映射的详细信息，包括其唯一标识符(`id`)。 此值是后续步骤中创建数据流的必需值。

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

## 检索数据流规范{#specs}

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

成功的响应会返回负责将数据从源引入平台的数据流规范的详细信息。 响应包括创建新数据流所需的唯一流规范`id`。

```json
{
    "items": [
        {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "name": "CloudStorageToAEP",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
                "ecadc60c-7455-4d87-84dc-2a0e293d997b",
                "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
                "4c10e202-c428-4796-9208-5f1f5732b1cf",
                "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
                "32e8f412-cdf7-464c-9885-78184cb113fd",
                "b7bf2577-4520-42c9-bae9-cad01560f7bc",
                "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
                "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8"
            ],
            "targetConnectionSpecIds": [
                "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
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

收集云存储数据的最后一步是创建数据流。 现在，您准备了以下必需值：

- [源连接ID](#source)
- [目标连接ID](#target)
- [映射ID](#mapping)
- [数据流规范ID](#specs)

数据流负责从源调度和收集数据。 通过在有效负荷中提供先前提到的值时执行POST请求，可以创建数据流。

要计划摄取，您必须首先将开始时间值设置为纪元时间（以秒为单位）。 然后，您必须将频率值设置为以下五个选项之一：`once`、`minute`、`hour`、`day`或`week`。 间隔值指定两个连续摄取之间的周期，并且创建一次摄取不需要设置间隔。 对于所有其他频率，间隔值必须设置为等于或大于`15`。

>[!IMPORTANT]
>
>强烈建议在使用[FTP连接器](../../../connectors/cloud-storage/ftp.md)时计划数据流以进行一次性摄取。

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
        "name": "Cloud Storage flow to Platform",
        "description": "Cloud Storage flow to Platform",
        "flowSpec": {
            "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "26b53912-1005-49f0-b539-12100559f0e2"
        ],
        "targetConnectionIds": [
            "f7eb08fa-5f04-4e45-ab08-fa5f046e45ee"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1597784298",
            "frequency":"minute",
            "interval":"30"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `flowSpec.id` | 在上一步中检索到的[流规范ID](#specs)。 |
| `sourceConnectionIds` | 在之前的步骤中检索到的[源连接ID](#source)。 |
| `targetConnectionIds` | 在之前的步骤中检索到的[目标连接ID](#target-connection)。 |
| `transformations.params.mappingId` | 在之前的步骤中检索到的[映射ID](#mapping)。 |
| `scheduleParams.startTime` | 开始时间中数据流的数据时间。 |
| `scheduleParams.frequency` | 数据流收集数据的频率。 可接受的值包括：`once`、`minute`、`hour`、`day`或`week`。 |
| `scheduleParams.interval` | 该间隔指定两个连续流运行之间的周期。 间隔的值应为非零整数。 当频率设置为`once`时，不需要间隔，对于其他频率值，间隔应大于或等于`15`。 |

**响应**

成功的响应会返回新创建的数据流的ID(`id`)。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 监视数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关流运行、完成状态和错误的信息。 有关如何监视数据流的详细信息，请参见有关[监视API](../monitor.md)中数据流的教程

## 后续步骤

通过遵循本教程，您已创建了源连接器，以按计划从您的云存储收集数据。 现在，下游平台服务（如[!DNL Real-time Customer Profile]和[!DNL Data Science Workspace]）可以使用传入数据。 有关更多详细信息，请参阅以下文档:

- [实时客户用户档案概述](../../../../profile/home.md)
- [数据科学工作区概述](../../../../data-science-workspace/home.md)

## 附录 {#appendix}

以下部分列表不同的云存储源连接器及其连接规范。

### 连接规范

| 连接器名称 | 连接规范 |
| -------------- | --------------- |
| [!DNL Amazon S3] (S3) | `ecadc60c-7455-4d87-84dc-2a0e293d997b` |
| [!DNL Amazon Kinesis] (Kinesis) | `86043421-563b-46ec-8e6c-e23184711bf6` |
| [!DNL Azure Blob] (Blob) | `4c10e202-c428-4796-9208-5f1f5732b1cf` |
| [!DNL Azure Data Lake Storage Gen2] （ADLS第2代） | `0ed90a81-07f4-4586-8190-b40eccef1c5a` |
| [!DNL Azure Event Hubs] (事件中心) | `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| [!DNL Azure File Storage] | `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |
| [!DNL Google Cloud Storage] | `32e8f412-cdf7-464c-9885-78184cb113fd` |
| HDFS | `54e221aa-d342-4707-bcff-7a4bceef0001` |
| SFTP | `bf367b0d-3d9b-4060-b67b-0d3d9bd06094` |
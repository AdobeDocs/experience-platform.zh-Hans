---
keywords: Experience Platform；主页；热门主题；云存储数据；流数据；流
solution: Experience Platform
title: 使用流服务API为原始数据创建流数据流
type: Tutorial
description: 本教程介绍了有关检索流数据以及使用源连接器和API将它们引入Experience Platform的步骤。
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API为原始数据创建流式数据流

本教程介绍了从流源连接器检索原始数据以及使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)将这些数据引入Experience Platform的步骤。

## 快速入门

本教程要求您实际了解Adobe Experience Platform的以下组件：

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   - [架构组合的基础知识](../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   - [架构注册表开发人员指南](../../../../xdm/api/getting-started.md)：包含成功执行对架构注册表API的调用所需了解的重要信息。 这包括您的`{TENANT_ID}`、“容器”的概念以及发出请求所需的标头（请特别注意“接受”标头及其可能的值）。
- [[!DNL Catalog Service]](../../../../catalog/home.md)：目录是Experience Platform中数据位置和谱系的记录系统。
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md)： Experience Platform的流式摄取为用户提供了一种实时将数据从客户端和服务器端设备发送到Experience Platform的方法。
- [沙盒](../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../landing/api-guide.md)指南。

### 创建源连接 {#source}

本教程还要求您具有适用于流连接器的有效源连接ID。 如果您没有此信息，请先参阅以下有关创建流源连接的教程，然后再尝试本教程：

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

## 创建目标XDM架构 {#target-schema}

为了在Experience Platform中使用源数据，必须创建目标架构，以根据您的需求构建源数据。 然后，使用目标架构创建包含源数据的Experience Platform数据集。 此目标XDM架构还扩展XDM [!DNL Individual Profile]类。

要创建目标XDM架构，请向[[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)的`/schemas`端点发出POST请求。

**API格式**

```http
POST /tenant/schemas
```

**请求**

以下示例请求创建扩展XDM [!DNL Individual Profile]类的XDM架构。

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

成功的响应返回新创建架构的详细信息，包括其唯一标识符(`$id`)。 在后续步骤中，创建目标数据集、映射和数据流时需要此ID。

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

## 创建目标数据集

创建目标XDM架构及其唯一`$id`后，您现在可以创建目标数据集以包含源数据。 要创建目标数据集，请向[目录服务API](https://www.adobe.io/experience-platform-apis/references/catalog/)的`dataSets`端点发出POST请求，同时在有效负载中提供目标架构的ID。

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
| `name` | 要创建的数据集的名称。 |
| `schemaRef.id` | 数据集将基于的XDM架构的URI `$id`。 |
| `schemaRef.contentType` | 架构的版本。 此值必须设置为`application/vnd.adobe.xed-full-notext+json;version=1`，这将返回架构的最新次版本。 有关详细信息，请参阅XDM API指南中有关[架构版本控制](../../../../xdm/api/getting-started.md#versioning)的部分。 |

**响应**

成功的响应将返回一个数组，该数组包含新创建的数据集的ID，格式为`"@/datasets/{DATASET_ID}"`。 数据集ID是系统生成的只读字符串，用于在API调用中引用数据集。 在后续步骤中，需要目标数据集ID才能创建目标连接和数据流。

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## 创建目标连接 {#target-connection}

Target连接可创建并管理到Experience Platform的目标连接或传输的数据将要到达的任何位置。 目标连接包含有关创建数据流所需的数据目标、数据格式和目标连接ID的信息。 Target连接实例特定于租户和组织。

要创建目标连接，请向[!DNL Flow Service] API的`/targetConnections`端点发出POST请求。 作为请求的一部分，您必须提供数据格式、上一步中检索到的`dataSetId`以及绑定到[!DNL Data Lake]的固定连接规范ID。 此ID为`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

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
| `data.format` | 您带入数据湖的数据的指定格式。 |
| `params.dataSetId` | 上一步中生成的目标数据集的ID。 **注意**：创建目标连接时，必须提供有效的数据集ID。 无效的数据集ID将导致错误。 |
| `connectionSpec.id` | 用于连接到数据湖的连接规范ID。 此ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |

**响应**

成功的响应返回新目标连接的唯一标识符(`id`)。 此ID在后续步骤中是必需的。

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## 创建映射 {#mapping}

要将源数据摄取到目标数据集中，必须首先将其映射到目标数据集所遵循的目标架构。

要创建映射集，请在提供目标XDM架构`$id`和要创建的映射集的详细信息时，向[[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/)的`mappingSets`端点发出POST请求。

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
| `xdmSchema` | 目标XDM架构的`$id`。 |

**响应**

成功的响应返回新创建的映射的详细信息，包括其唯一标识符(`id`)。 此ID是稍后步骤创建数据流所必需的。

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

## 检索数据流规范列表 {#specs}

数据流负责从源收集数据并将这些数据导入Experience Platform。 要创建数据流，您必须首先通过向[!DNL Flow Service] API执行GET请求来获取数据流规范。

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

成功的响应将返回数据流规范列表。 使用[!DNL Amazon Kinesis]、[!DNL Azure Event Hubs]或[!DNL Google PubSub]的任何一个创建数据流所需检索的数据流规范ID是`d69717ba-71b4-4313-b654-49f9cf126d7a`。

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

## 创建数据流

>[!NOTE]
>
>创建或更新流数据流后，需要短暂暂停数据摄取5分钟，以防出现任何潜在的数据丢失或数据丢失情况。

收集流数据的最后一步是创建数据流。 现在，您已准备以下必需值：

- [Source连接Id](#source)
- [目标连接ID](#target)
- [映射 ID](#mapping)
- [数据流规范ID](#specs)

数据流负责从源中计划和收集数据。 您可以通过在有效负载中提供前面提到的值时执行POST请求来创建数据流。

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
| `flowSpec.id` | 在上一步中检索到[流规范ID](#specs)。 |
| `sourceConnectionIds` | 在之前的步骤中检索到[源连接ID](#source)。 |
| `targetConnectionIds` | 在之前的步骤中检索到[目标连接ID](#target-connection)。 |
| `transformations.params.mappingId` | 在之前的步骤中检索到[映射ID](#mapping)。 |

**响应**

成功的响应返回新创建的数据流的ID (`id`)。

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 发布要引入的数据

查看以下有效负载示例，了解可发送以供摄取的原始或XDM兼容JSON的示例。

>[!NOTE]
>
>在创建数据流和摄取任何流数据之间必须添加至少约5分钟的延迟。 这样一来，在摄取任何数据之前，都可以完全启用数据流。

以下示例适用于所有：

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

>[!BEGINTABS]

>[!TAB 原始数据]

```json
'{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

>[!TAB XDM数据]

```json
{
  "header": {
    "schemaRef": {
      "id": "https://ns.adobe.com/aepstreamingservicesint/schemas/73cae7e6db06ebca535cd973e3ece85e66253962f504e7d8",
      "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
    }
  },
  "body": {
    "xdmMeta": {
      "schemaRef": {
        "id": "https://ns.adobe.com/aepstreamingservicesint/schemas/73cae7e6db06ebca535cd973e3ece85e66253962f504e7d8",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
      }
    },
    "xdmEntity": {
      "_id": "acme",
      "workEmail": {
        "address": "mike@acme.com",
        "primary": true,
        "type": "work",
        "status": "active"
      },
      "person": {
        "gender": "male",
        "name": {
          "firstName": "Mike",
          "lastName": "Wazowski"
        },
        "birthDate": "1985-01-01"
      },
      "identityMap": {
        "ecid": [
          {
            "id": "01262118050522051420082102000000000000"
          }
        ]
      }
    }
  }
}
```

>[!ENDTABS]

## 后续步骤

通过阅读本教程，您已创建一个数据流以从流连接器收集流数据。 传入数据现在可供下游Experience Platform服务（如[!DNL Real-Time Customer Profile]和[!DNL Data Science Workspace]）使用。 有关更多详细信息，请参阅以下文档：

- [实时客户轮廓概述](../../../../profile/home.md)
- [数据科学工作区概述](../../../../data-science-workspace/home.md)

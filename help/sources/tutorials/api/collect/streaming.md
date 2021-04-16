---
keywords: Experience Platform；主页；热门主题；云存储数据；流数据；流
solution: Experience Platform
title: 使用源连接器和API收集流数据
topic: 概述
type: Tutorial
description: 本教程介绍了使用源连接器和API检索流数据并将其引入平台的步骤。
exl-id: 898df7fe-37a9-4495-ac05-30029258a6f4
translation-type: tm+mt
source-git-commit: 727c9dbd87bacfd0094ca29157a2d0283c530969
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 2%

---

# 使用源连接器和API收集流数据

[!DNL Flow Service] 用于收集和集中来自Adobe Experience Platform内不同来源的客户数据。该服务提供用户界面和RESTful API，所有受支持的源都可从中连接。

本教程介绍了从流源连接器检索数据并使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)将其引入[!DNL Experience Platform]的步骤。

## 入门指南

本教程要求您具有流连接器的有效连接ID。 如果您没有此信息，请在尝试本教程之前参阅以下有关创建流源连接的教程：

- [[!DNL Amazon Kinesis]](../create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../create/cloud-storage/eventhub.md)
- [[!DNL HTTP API]](../create/streaming/http.md)
- [[!DNL Google PubSub]](../create/cloud-storage/google-pubsub.md)

本教程还要求您对Adobe Experience Platform的以下组件有充分的了解：

- [[!DNL Experience Data Model (XDM) System]](../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   - [模式合成的基础](../../../../xdm/schema/composition.md):了解XDM模式的基本构建基块，包括模式构成的主要原则和最佳做法。
   - [模式 Registry开发人员指南](../../../../xdm/api/getting-started.md):包括成功执行对模式注册表API的调用所需了解的重要信息。这包括您的`{TENANT_ID}`、“容器”的概念以及发出请求所需的标头（特别要注意“接受”标头及其可能的值）。
- [[!DNL Catalog Service]](../../../../catalog/home.md):目录是数据位置和谱系的记录系 [!DNL Experience Platform]统。
- [[!DNL Streaming ingestion]](../../../../ingestion/streaming-ingestion/overview.md):流式摄取 [!DNL Platform] 为用户提供了将数据从客户端和服务器端设备实时发送到 [!DNL Experience Platform] 的方法。
- [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单 [!DNL Platform] 独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了使用[!DNL Flow Service] API成功收集流数据所需了解的其他信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中关于如何读取示例API调用](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。[

### 收集所需标题的值

要调用[!DNL Platform] API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个头，该头指定操作将在中执行的沙箱的名称：

- `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

- `Content-Type: application/json`

## 创建源连接{#source}

可以通过向[!DNL Flow Service] API发出POST请求来创建源连接。 源连接由连接ID、源数据文件的路径和连接规范ID组成。

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
        "name": "Test source connector for streaming data",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "connectionId": "f6aa6c58-3c3d-4c59-aa6c-583c3d6c599c",
        "description": "Test source connector for streaming data",
        "data": {
            "format": "delimited"
        },
            "connectionSpec": {
            "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `providerId` | 流连接器的提供者ID。 |
| `connectionId` | 流连接器的唯一连接ID。 |
| `connectionSpec.id` | 与特定流连接器关联的连接规范ID。 |

**响应**

成功的响应返回新创建的源连接的唯一标识符(`id`)。 在后续步骤中需要此ID才能创建数据流。

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## 获取流端点URL {#get-endpoint}

创建源连接后，您现在可以检索流端点URL。

**API格式**

```http
GET /flowservice/sourceConnections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 您先前创建的sourceConnections的`id`值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/sourceConnections/e96d6135-4b50-446e-922c-6dd66672b6b2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含有关所请求连接的详细信息。 流端点URL是使用连接自动创建的，可使用`inletUrl`值进行检索。

```json
{
    "items": [
        {
            "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
            "createdAt": 1617743929826,
            "updatedAt": 1617743930363,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "sandboxId": "d537df80-c5d7-11e9-aafb-87c71c35cac8",
            "sandboxName": "prod",
            "imsOrgId": "{IMS_ORG}",
            "name": "Test source connector for streaming data",
            "description": "Test source connector for streaming data",
            "baseConnectionId": "f6aa6c58-3c3d-4c59-aa6c-583c3d6c599c",
            "state": "enabled",
            "data": {
                "format": "delimited",
                "schema": null,
                "properties": null
            },
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "params": {
                "sourceId": "Streaming raw data",
                "inletUrl": "https://dcs.adobedc.net/collection/2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b",
                "inletId": "2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b",
                "dataType": "raw",
                "name": "hgtest"
            },
            "version": "\"d6006bc1-0000-0200-0000-606cd03a0000\"",
            "etag": "\"d6006bc1-0000-0200-0000-606cd03a0000\"",
            "inheritedAttributes": {
                "baseConnection": {
                    "id": "f6aa6c58-3c3d-4c59-aa6c-583c3d6c599c",
                    "connectionSpec": {
                        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                        "version": "1.0"
                    }
                }
            }
        }
    ]
}
```


## 创建目标XDM模式{#target-schema}

要在[!DNL Platform]中使用源模式，必须创建一个目标，以根据您的需要构建源数据。 然后，目标模式用于创建包含源数据的[!DNL Platform]数据集。 此目标XDM模式还扩展了XDM [!DNL Individual Profile]类。

通过对[目标注册表API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)执行POST请求，可以创建模式XDM模式。

**API格式**

```http
POST /tenant/schemas
```

**请求**

下面的示例请求创建一个XDM模式，用于扩展XDM [!DNL Individual Profile]类。

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

成功的响应返回新创建的模式的详细信息，包括其唯一标识符(`$id`)。 在后续步骤中需要此ID才能创建目标数据集、映射和数据流。

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

可以通过对[目录服务API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)执行POST请求，提供有效负荷内目标模式的ID来创建目标数据集。

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
        },
        "name": "Test streaming dataset"
    }'
```

| 属性 | 描述 |
| --- | --- |
| `schemaRef.id` | 目标 XDM模式的ID。 |
| `schemaRef.contentType` | 模式版本。 此值必须设置为`application/vnd.adobe.xed-full-notext+json;version=1`，这将返回模式的最新次要版本。 |

**响应**

成功的响应返回一个数组，其中包含格式为`"@/datasets/{DATASET_ID}"`的新创建数据集的ID。 数据集ID是一个只读的、由系统生成的字符串，用于在API调用中引用数据集。 在后续步骤中，需要目标数据集ID才能创建目标连接和数据流。

```json
[
    "@/dataSets/5f7187bac6d00f194fb937c0"
]
```

## 创建目标连接{#target-connection}

目标连接表示到所摄取数据所进入的目标的连接。 要创建目标连接，必须提供与数据湖关联的固定连接规范ID。 此连接规范ID为：`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

您现在具有将目标数据集和连接规范ID模式到数据湖的目标唯一标识符。 使用这些标识符，您可以使用[!DNL Flow Service] API创建目标连接，以指定将包含入站源数据的数据集。

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
        "name": "Streaming target connection",
        "description": "Streaming target connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "parquet_xdm"
        },
        "params": {
        "dataSetId": "5f7187bac6d00f194fb937c0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `params.dataSetId` | 目标数据集的ID。 |
| `connectionSpec.id` | 用于连接到数据湖的连接规范ID。 此ID为：`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。 |

**响应**

成功的响应返回新目标连接的唯一标识符(`id`)。 此ID是后续步骤中必需的。

```json
{
    "id": "d9300194-6a82-4163-b001-946a821163b8",
    "etag": "\"4006d3e4-0000-0200-0000-5f7189220000\""
}
```

## 创建映射{#mapping}

要将源数据引入目标数据集，必须首先将其映射到目标数据集附带的目标模式。 这是通过对转换服务执行POST请求来实现的，该请求在请求有效负荷中定义了数据映射。

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
| `xdmSchema` | 目标XDM模式的`$id`。 |

**响应**

成功的响应返回新创建映射的详细信息，包括其唯一标识符(`id`)。 在后续步骤中需要此ID才能创建数据流。

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

## 查找数据流规范{#specs}

数据流负责从源中收集数据并将它们引入[!DNL Platform]。 要创建数据流，必须首先对[!DNL Flow Service] API执行GET请求，以获得数据流规范。 数据流规范负责从流连接器收集数据。
**API格式**

```http
GET /flowSpecs?property=name=="Steam data with transformation"
```

**请求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name=="Steam data with transformation"' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回数据流规范的详细信息，该规范负责将流连接器中的数据导入[!DNL Platform]。 在下一步中需要此ID才能创建新数据流。

```json
{
    "items": [
        {
            "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
            "name": "Steam data with transformation",
            "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
            "version": "1.0",
            "sourceConnectionSpecIds": [
                "d27d4907-7351-47dd-bbc2-05a04365703d",
                "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
                "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb"
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
                        "description": "defines various params required for different mapping from Raw to XDM",
                        "properties": {
                            "mappingId": {
                                "type": "string"
                            }
                        },
                        "required": [
                            "mappingId"
                        ]
                    }
                }
            ],
            "attributes": {
                "uiAttributes": {
                    "apiFeatures": {
                        "deleteSupported": false,
                        "updateSupported": false,
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
        }
    ]
}
```

## 创建数据流

收集流数据的最后一步是创建数据流。 现在，您准备了以下必需值：

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
        "name": "Streaming dataflow",
        "description": "Streaming dataflow",
        "flowSpec": {
            "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
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
| `flowSpec.id` | 在上一步中检索到的[流规范ID](#specs)。 |
| `sourceConnectionIds` | 在前面的步骤中检索到的[源连接ID](#source)。 |
| `targetConnectionIds` | 在前面的步骤中检索到的[目标连接ID](#target-connection)。 |
| `transformations.params.mappingId` | 在之前的步骤中检索到的[映射ID](#mapping)。 |

**响应**

成功的响应返回新创建的数据流的ID(`id`)。

```json
{
    "id": "1f086c23-2ea8-4d06-886c-232ea8bd061d",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 发布要收录的原始数据{#ingest-data}

现在，您已创建了流，可以将JSON消息发送到之前创建的流端点。

**API格式**

```http
POST /collection/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 新创建的流连接的`id`值。 |

**请求**

该示例请求将原始数据摄取到先前创建的流端点。

```shell
curl -X POST https://dcs.adobedc.net/collection/2301a1f761f6d7bf62c5312c535e1076bbc7f14d728e63cdfd37ecbb4344425b \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: 1f086c23-2ea8-4d06-886c-232ea8bd061d' \
  -d '{
      "name": "Johnson Smith",
      "location": {
          "city": "Seattle",
          "country": "United State of America",
          "address": "3692 Main Street"
      },
      "gender": "Male"
      "birthday": {
          "year": 1984
          "month": 6
          "day": 9
      }
  }'
```

**响应**

成功的响应返回HTTP状态200，其中包含新摄取的信息的详细信息。

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 先前创建的流连接的ID。 |
| `xactionId` | 您刚刚发送的记录在服务器端生成的唯一标识符。 此ID可帮助Adobe在各种系统和调试过程中跟踪此记录的生命周期。 |
| `receivedTimeMs`:显示接收请求的时间的时间戳（以毫秒为单位）。 |

## 后续步骤

按照本教程，您创建了一个数据流以从流连接器收集流数据。 现在，下游[!DNL Platform]服务（如[!DNL Real-time Customer Profile]和[!DNL Data Science Workspace]）可以使用传入数据。 有关更多详细信息，请参阅以下文档:

- [实时客户用户档案概述](../../../../profile/home.md)
- [数据科学工作区概述](../../../../data-science-workspace/home.md)

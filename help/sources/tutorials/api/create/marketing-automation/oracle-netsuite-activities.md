---
title: 使用流服务API为Oracle NetSuite活动创建源连接和数据流
description: 了解如何使用流服务API创建源连接和数据流，将Oracle NetSuite事件数据引入Experience Platform。
exl-id: 4f695389-2261-469c-8d40-7bd29a4e7f77
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '1957'
ht-degree: 1%

---

# 使用流服务API为[!DNL Oracle NetSuite Activities]创建源连接和数据流

阅读以下教程，了解如何使用[!DNL Oracle NetSuite Activities]API[[!DNL Flow Service] 将](https://www.adobe.io/experience-platform-apis/references/flow-service/)帐户中的事件数据引入Adobe Experience Platform。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Oracle NetSuite Activities] API成功连接到[!DNL Flow Service]所需了解的其他信息。

### 身份验证

有关如何检索身份验证凭据的信息，请阅读[[!DNL Oracle NetSuite] 概述](../../../../connectors/marketing-automation/oracle-netsuite.md)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 使用[!DNL Oracle NetSuite Activities] API将[!DNL Flow Service]连接到Experience Platform

按照以下指南了解如何对[!DNL Oracle NetSuite Activities]源进行身份验证、创建源连接和创建数据流以将事件数据引入Experience Platform。

### 创建基本连接 {#base-connection}

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的`/connections`身份验证凭据作为请求正文的一部分时，向[!DNL Oracle NetSuite Activities]端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL Oracle NetSuite Activities]创建基本连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NeSuite Activities base connection",
      "description": "Authenticated base connection for Oracle NetSuite Activities",
      "connectionSpec": {
          "id": "fdf850b4-5a8d-4a5a-9ce8-4caef9abb2a8",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params": {
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
              "accessTokenUrl": "{ACCESS_TOKEN_URL}",
              "accessToken": "{ACCESS_TOKEN_URL}"
          }
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 基础连接的名称。 确保基本连接的名称是描述性的，因为您可以使用此名称查找有关基本连接的信息。 |
| `description` | 可包含的可选值，用于提供有关基本连接的更多信息。 |
| `connectionSpec.id` | 源的连接规范ID。 在您的源通过[!DNL Flow Service] API注册和批准后，可以检索此ID。 |
| `auth.specName` | 您用于向Experience Platform验证源的身份验证类型。 |
| `auth.params.clientId` | 创建集成记录时的客户端ID值。 可在[此处](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981)找到创建交互记录的进程。 该值是一个与`7fce.....b42f`类似的64个字符的字符串。 |
| `auth.params.clientSecret` | 创建集成记录时的客户端ID值。 可在[此处](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981)找到创建交互记录的进程。 该值是一个与`5c98.....1b46`类似的64个字符的字符串。 |
| `auth.params.accessTokenUrl` | [!DNL NetSuite]访问令牌URL，类似于`https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/auth/oauth2/v1/token`，您将在其中将ACCOUNT_ID替换为您的[!DNL NetSuite]帐户ID。 |
| `auth.params.accessToken` | 访问令牌值在[OAuth 2.0授权代码授予流程](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint)教程的[步骤二](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow)的末尾生成。 访问令牌的过期有效期仅为60分钟。 该值是一个格式为JSON Web令牌(JWT)的1024字符字符串，类似于`eyJr......f4V0`。 |

**响应**

成功的响应返回新创建的基本连接，包括其唯一连接标识符(`id`)。 在下一步中浏览源的文件结构和内容时，需要此ID。

```json
{
    "id": "60c81023-99b4-4aae-9c31-472397576dd2",
    "etag": "\"fa003785-0000-0200-0000-6555c5310000\""
}
```

### 浏览您的源 {#explore}

获得基本连接ID后，您现在可以通过对`/connections`端点执行GET请求来探索源数据的内容和结构，同时将基本连接ID作为查询参数提供。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**请求**

执行GET请求以浏览源的文件结构和内容时，必须包括下表列出的查询参数：

| 参数 | 描述 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 上一步中生成的基本连接ID。 |
| `objectType=rest` | 您希望探索的对象类型。 目前，此值始终设置为`rest`。 |
| `{OBJECT}` | 只有在查看特定目录时才需要此参数。 其值表示您希望浏览的目录的路径。 对于此源，该值将为`json`。 |
| `fileType=json` | 要带到Experience Platform的文件类型。 当前，`json`是唯一支持的文件类型。 |
| `{PREVIEW}` | 一个布尔值，定义连接的内容是否支持预览。 |
| `{SOURCE_PARAMS}` | 为要带到Experience Platform的源文件定义参数。 要检索`{SOURCE_PARAMS}`的已接受格式类型，必须以base64为整个字符串进行编码。 <br> [!DNL Oracle NetSuite Activities]的值为空。</li></ul> |

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=e30%3D' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回类似于以下内容的JSON结构：

+++选择以查看JSON有效负载

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "totalResults": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "offset": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "hasMore": {
                "type": "boolean"
            },
            "links": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "rel": {
                            "type": "string"
                        },
                        "href": {
                            "type": "string"
                        }
                    }
                }
            },
            "items": {
                "type": "object",
                "properties": {
                    "owner": {
                        "type": "string"
                    },
                    "createddate": {
                        "type": "string"
                    },
                    "lastmodifieddate": {
                        "type": "string"
                    },
                    "accesslevel": {
                        "type": "string"
                    },
                    "alldayevent": {
                        "type": "string"
                    },
                    "message": {
                        "type": "string"
                    },
                    "startdate": {
                        "type": "string"
                    },
                    "title": {
                        "type": "string"
                    },
                    "organizer": {
                        "type": "string"
                    },
                    "response": {
                        "type": "string"
                    },
                    "links": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {}
                        }
                    },
                    "location": {
                        "type": "string"
                    },
                    "timedevent": {
                        "type": "string"
                    },
                    "id": {
                        "type": "string"
                    },
                    "status": {
                        "type": "string"
                    }
                }
            }
        }
    },
    "data": [
        {
            "totalResults": 13,
            "offset": 0,
            "count": 13,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "accesslevel": "BUSY",
                "alldayevent": "F",
                "createddate": "2022-12-15",
                "id": "5",
                "lastmodifieddate": "2022-12-15",
                "location": "Caffe West",
                "message": "Bring Monthly Results",
                "organizer": "-5",
                "owner": "-5",
                "response": "ACCEPTED",
                "startdate": "2022-12-15",
                "status": "CONFIRMED",
                "timedevent": "T",
                "title": "Meeting with Tom"
            }
        },
        {
            "totalResults": 13,
            "offset": 0,
            "count": 13,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "accesslevel": "BUSY",
                "alldayevent": "F",
                "createddate": "2023-02-01",
                "id": "103",
                "lastmodifieddate": "2023-02-01",
                "location": "Caffe West",
                "message": "Bring Monthly Results",
                "organizer": "-5",
                "owner": "-5",
                "response": "ACCEPTED",
                "startdate": "2022-12-15",
                "status": "CONFIRMED",
                "timedevent": "T",
                "title": "Meeting with Tom"
            }
        },
        {
            "totalResults": 13,
            "offset": 0,
            "count": 13,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "accesslevel": "BUSY",
                "alldayevent": "F",
                "createddate": "2023-11-09",
                "id": "204",
                "lastmodifieddate": "2023-11-09",
                "location": "Caffe West",
                "message": "Bring Monthly Results",
                "organizer": "-5",
                "owner": "-5",
                "response": "ACCEPTED",
                "startdate": "2023-12-15",
                "status": "CONFIRMED",
                "timedevent": "T",
                "title": "Meeting with Tom"
            }
        },
    ]
}
```

+++

### 创建源连接 {#source-connection}

您可以通过向`/sourceConnections` API的[!DNL Flow Service]端点发出POST请求来创建源连接。 源连接由连接ID、源数据文件的路径以及连接规范ID组成。

**API格式**

```https
POST /sourceConnections
```

**请求**

以下请求为[!DNL Oracle NetSuite Activities]创建源连接。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Activities Source Connection",
      "description": "Oracle NetSuite Activities Source Connection",
      "baseConnectionId": "60c81023-99b4-4aae-9c31-472397576dd2",
      "connectionSpec": {
          "id": "fdf850b4-5a8d-4a5a-9ce8-4caef9abb2a8",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 源连接的名称。 请确保源连接的名称是描述性的，因为您可以使用此名称查找有关源连接的信息。 |
| `description` | 可包含的可选值，用于提供有关源连接的更多信息。 |
| `baseConnectionId` | [!DNL Oracle NetSuite Activities]的基本连接ID。 此ID是在前面的步骤中生成的。 |
| `connectionSpec.id` | 与源对应的连接规范ID。 |
| `data.format` | 要摄取的[!DNL Oracle NetSuite Activities]数据的格式。 当前，唯一支持的数据格式为`json`。 |

成功的响应返回新创建的源连接的唯一标识符(`id`)。 此ID是稍后步骤创建数据流所必需的。

```json
{
    "id": "574c049f-29fc-411f-be0d-f80002025f51",
    "etag": "\"0704acb3-0000-0200-0000-6555c5470000\""
}
```

### 创建目标XDM架构 {#target-schema}

为了在Experience Platform中使用源数据，必须创建目标架构，以根据您的需求构建源数据。 然后，使用目标架构创建包含源数据的Experience Platform数据集。

通过对[架构注册表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)执行POST请求，可以创建目标XDM架构。

有关如何创建目标XDM架构的详细步骤，请参阅有关使用API [创建架构的教程](../../../../../xdm/api/schemas.md#create-a-schema)。

### 创建目标数据集 {#target-dataset}

通过向[目录服务API](https://developer.adobe.com/experience-platform-apis/references/catalog/)执行POST请求，在有效负载中提供目标架构的ID，可以创建目标数据集。

有关如何创建目标数据集的详细步骤，请参阅有关[使用API创建数据集的教程](../../../../../catalog/api/create-dataset.md)。

### 创建目标连接 {#target-connection}

目标连接表示与要存储所摄取数据的目标的连接。 要创建目标连接，您必须提供对应于数据湖的固定连接规范ID。 此ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

现在，您拥有目标架构、目标数据集以及到数据湖的连接规范ID。 使用这些标识符，您可以使用[!DNL Flow Service] API创建目标连接，以指定将包含入站源数据的数据集。

**API格式**

```https
POST /targetConnections
```

**请求**

以下请求为[!DNL Oracle NetSuite Activities]创建目标连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Activities Target Connection Generic Rest",
      "description": "Oracle NetSuite Activities Target Connection Generic Rest",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
              "version": "1.2"
          }
      },
      "params": {
          "dataSetId": "65004470082ac828d2c3d6a0"
      }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 目标连接的名称。 确保目标连接的名称是描述性的，因为您可以使用此名称查找有关目标连接的信息。 |
| `description` | 可包含的可选值，用于提供有关目标连接的更多信息。 |
| `connectionSpec.id` | 对应于数据湖的连接规范ID。 此固定ID为： `6b137bf6-d2a0-48c8-914b-d50f4942eb85`。 |
| `data.format` | 要摄取的[!DNL Oracle NetSuite Activities]数据的格式。 |
| `params.dataSetId` | 在上一步中检索到的目标数据集ID。 |

**响应**

成功的响应返回新目标连接的唯一标识符(`id`)。 此ID在后续步骤中是必需的。

```json
{
    "id": "382fc614-3c5b-46b9-a971-786fb0ae6c5d",
    "etag": "\"e0016100-0000-0200-0000-655707a40000\""
}
```

### 创建映射 {#mapping}

要将源数据摄取到目标数据集中，必须首先将其映射到目标数据集所遵循的目标架构。 这是通过在请求有效负载中定义数据映射的情况下对[[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/)执行POST请求来实现的。

**API格式**

```http
POST /conversion/mappingSets
```

**请求**

以下请求为[!DNL DNL NetSuite Activities]创建映射

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.id",
            "destination": "_extconndev.NSA_ID"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.title",
            "destination": "_extconndev.NSA_title"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.createddate",
            "destination": "_extconndev.NSA_createddate"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.location",
            "destination": "_extconndev.NSA_location"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.lastmodifieddate",
            "destination": "_extconndev.NSA_lastmodifieddate"
        }
      ],
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `outputSchema.schemaRef.id` | 在之前的步骤中生成的[目标XDM架构](#target-schema)的ID。 |
| `mappings.sourceType` | 正在映射的源属性类型。 |
| `mappings.source` | 需要映射到目标XDM路径的源属性。 |
| `mappings.destination` | 源属性将映射到的目标XDM路径。 |

**响应**

成功的响应返回新创建的映射的详细信息，包括其唯一标识符(`id`)。 在后续步骤中需要使用此值来创建数据流。

```json
{
    "id": "ddf0592bcc9d4ac391803f15f2429f87",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 创建流 {#flow}

将数据从[!DNL Oracle NetSuite Activities]引入Experience Platform的最后一步是创建数据流。 现在，您已准备以下必需值：

* [Source连接Id](#source-connection)
* [目标连接ID](#target-connection)
* [映射 ID](#mapping)

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
    "name": "Oracle NetSuite Activities connector Flow Generic Rest",
    "description": "Oracle NetSuite Activities connector Description Flow Generic Rest",
    "flowSpec": {
        "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "d8827440-339f-428d-bf38-5e2ab1f0f7bb"
    ],
    "targetConnectionIds": [
        "e349a15e-c639-4047-8b2a-154aa7a857d7"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "10787532e0994eb686e76bdab69a9e88",
                "mappingVersion": 0
            }
        }
    ],
      "scheduleParams": {
          "startTime": 1700202649,
          "frequency": "once"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 您的数据流的名称。 确保数据流的名称是描述性的，因为您可以使用此名称查找数据流上的信息。 |
| `description` | 可包含的可选值，用于提供有关数据流的更多信息。 |
| `flowSpec.id` | 创建数据流所需的流规范ID。 此固定ID为： `6499120c-0b15-42dc-936e-847ea3c24d72`。 |
| `flowSpec.version` | 流规范ID的相应版本。 此值默认为`1.0`。 |
| `sourceConnectionIds` | 在之前的步骤中生成的[源连接ID](#source-connection)。 |
| `targetConnectionIds` | 在之前的步骤中生成的[目标连接ID](#target-connection)。 |
| `transformations` | 此属性包含需要应用于数据的各种转换。 将不符合XDM的数据引入Experience Platform时，需要此属性。 |
| `transformations.name` | 分配给转换的名称。 |
| `transformations.params.mappingId` | 在之前的步骤中生成的[映射ID](#mapping)。 |
| `transformations.params.mappingVersion` | 映射ID的相应版本。 此值默认为`0`。 |
| `scheduleParams.startTime` | 此属性包含有关数据流的摄取计划的信息。 |
| `scheduleParams.frequency` | 数据流收集数据的频率。 |
| `scheduleParams.interval` | 间隔指定两次连续流运行之间的周期。 间隔的值应为非零整数。 |

**响应**

成功的响应返回新创建的数据流的ID (`id`)。 您可以使用此ID监视、更新或删除数据流。

```json
{
     "id": "84c64142-1741-4b0b-95a9-65644eba0cf6",
     "etag": "\"3901770b-0000-0200-0000-655708970000\""
}
```

## 附录

以下部分提供了有关监视、更新和删除数据流的步骤的信息。

### 监测数据流

创建数据流后，您可以监视通过它摄取的数据，以查看有关流运行、完成状态和错误的信息。 有关完整的API示例，请阅读有关[使用API监视源数据流](../../monitor.md)的指南。

### 更新您的数据流

通过提供数据流的ID，向`/flows` API的[!DNL Flow Service]端点发出PATCH请求来更新数据流的详细信息，例如其名称和描述，以及其运行计划和关联的映射集。 发出PATCH请求时，必须在`etag`标头中提供数据流唯一的`If-Match`。 有关完整的API示例，请阅读有关[使用API更新源数据流](../../update-dataflows.md)的指南。

### 更新您的帐户

在提供基本连接ID作为查询参数的同时，通过向[!DNL Flow Service] API执行PATCH请求来更新源帐户的名称、描述和凭据。 发出PATCH请求时，必须在`etag`标头中提供源帐户的唯一`If-Match`。 有关完整的API示例，请阅读有关[使用API更新源帐户](../../update.md)的指南。

### 删除您的数据流

在查询参数中提供要删除的数据流的ID时，通过向[!DNL Flow Service] API执行DELETE请求来删除数据流。 有关完整的API示例，请阅读有关[使用API删除数据流](../../delete-dataflows.md)的指南。

### 删除您的帐户

在提供要删除的帐户的基本连接ID时，通过向[!DNL Flow Service] API执行DELETE请求来删除您的帐户。 有关完整的API示例，请阅读有关使用API[删除源帐户](../../delete.md)的指南。

---
keywords: Experience Platform；主页；热门主题；流连接；创建流连接；API指南；教程；创建流连接；流摄取；摄取；
title: 使用流服务API创建HTTP API流连接
description: 本教程提供了有关如何使用HTTP API源通过流服务API为原始数据和XDM数据创建流连接的步骤
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 3%

---


# 使用[!DNL Flow Service] API创建HTTP API流连接

流量服务用于收集和集中Adobe Experience Platform中来自不同来源的客户数据。 该服务提供了一个用户界面和RESTful API，所有受支持的源均可从该API连接。

本教程使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)引导您完成使用[!DNL Flow Service] API创建流连接的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md)： [!DNL Experience Platform]用于组织体验数据的标准化框架。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，实时提供统一的使用者配置文件。

此外，创建流连接需要您具有目标XDM架构和数据集。 要了解如何创建这些数据，请阅读有关[流式处理记录数据](../../../../../ingestion/tutorials/streaming-record-data.md)的教程或有关[流式处理时间序列数据](../../../../../ingestion/tutorials/streaming-time-series-data.md)的教程。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接指定源，并包含使流与流摄取API兼容所需的信息。 创建基本连接时，您可以选择创建未经身份验证和经过身份验证的连接。

### 未经身份验证的连接

未经身份验证的连接是标准的流连接，当您想要将数据流式传输到Experience Platform中时，可以创建。

要创建未经身份验证的基本连接，请在提供连接的名称、数据类型和HTTP API连接规范ID的同时向`/connections`端点发出POST请求。 此ID为`bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`。

**API格式**

```http
POST /flowservice/connections
```

**请求**

以下请求为HTTP API创建基本连接。

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection XDM Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "xdm"
      }
    }
  }'
```

>[!TAB 原始数据]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
    "name": "ACME Streaming Connection Raw Data",
    "description": "ACME streaming connection for customer data",
    "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
    },
    "auth": {
      "specName": "Streaming Connection",
      "params": {
        "dataType": "raw"
      }
    }
  }'
```

>[!ENDTABS]

| 属性 | 描述 |
| --- | --- |
| `name` | 基础连接的名称。 请确保该名称是描述性的，因为您可以使用此名称查找基础连接上的信息。 |
| `description` | （可选）可包含的资产，用于提供有关基本连接的更多信息。 |
| `connectionSpec.id` | 与HTTP API对应的连接规范ID。 此ID为`bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`。 |
| `auth.params.dataType` | 流连接的数据类型。 支持的值包括： `xdm`和`raw`。 |
| `auth.params.name` | 要创建的流连接的名称。 |

**响应**

成功的响应返回HTTP状态201，其中包含新创建的连接的详细信息，包括其唯一标识符(`id`)。

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 新创建的基本连接的`id`。 |
| `etag` | 分配给连接的标识符，用于指定基本连接的版本。 |

### 已验证的连接

当您需要区分来自受信任来源和不受信任来源的记录时，应使用经过身份验证的连接。 用户如果希望发送包含个人身份信息(PII)的信息，则应在将信息流式传输到Experience Platform时创建一个经过身份验证的连接。

要创建经过身份验证的基本连接，您必须在请求中包含`authenticationRequired`参数，并将其值指定为`true`。 在此步骤中，您还可以为已验证的基本连接提供源ID。 此参数是可选的，如果未提供，它将使用与`name`属性相同的值。


**API格式**

```http
POST /flowservice/connections
```

**请求**

以下请求为HTTP API创建经过身份验证的基本连接。

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection XDM Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Authenticated XDM streaming connection",
             "dataType": "xdm",
             "name": "Authenticated XDM streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!TAB 原始数据]

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "ACME Streaming Connection Raw Data Authenticated",
     "description": "ACME streaming connection for customer data",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Authenticated raw streaming connection",
             "dataType": "raw",
             "name": "Authenticated raw streaming connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!ENDTABS]

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.sourceId` | 创建经过身份验证的基本连接时可以使用的其他标识符。 此参数是可选的，如果未提供，它将使用与`name`属性相同的值。 |
| `auth.params.authenticationRequired` | 此参数指定流连接是否需要身份验证。 如果`authenticationRequired`设置为`true`，则必须为流连接提供身份验证。 如果`authenticationRequired`设置为`false`，则不需要身份验证。 |

**响应**

成功的响应返回HTTP状态201，其中包含新创建的连接的详细信息，包括其唯一标识符(`id`)。

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

## 获取流端点URL

在创建基本连接后，您现在可以检索流端点URL。

**API格式**

```http
GET /flowservice/connections/{BASE_CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 您之前创建的连接的`id`值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含有关所请求连接的详细信息。 流端点URL自动创建连接，可以使用`inletUrl`值检索。

```json
{
  "items": [
    {
      "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "createdAt": 1669238699119,
      "updatedAt": 1669238699119,
      "createdBy": "acme@AdobeID",
      "updatedBy": "acme@AdobeID",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "ACME Streaming Connection XDM Data",
      "description": "ACME streaming connection for customer data",
      "connectionSpec": {
        "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "Streaming Connection",
        "params": {
          "sourceId": "ACME Streaming Connection XDM Data",
          "inletUrl": "https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "authenticationRequired": false,
          "inletId": "667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec",
          "dataType": "xdm",
          "name": "ACME Streaming Connection XDM Data"
        }
      },
      "version": "\"f50185ed-0000-0200-0000-637e8fad0000\"",
      "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
    }
  ]
}
```

## 创建源连接 {#source}

要创建源连接，请在提供基本连接ID的同时向`/sourceConnections`端点发出POST请求。

**API格式**

```http
POST /flowservice/sourceConnections
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Source Connection for Customer Data",
      "description": "A streaming source connection for ACME XDM Customer Data",
      "baseConnectionId": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
      "connectionSpec": {
          "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
          "version": "1.0"
      }
    }'
```

**响应**

成功的响应返回HTTP状态201，其中包含新创建的源连接的详细信息，包括其唯一标识符(`id`)。

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

## 创建目标XDM架构 {#target-schema}

为了在Experience Platform中使用源数据，必须创建目标架构，以根据您的需求构建源数据。 然后，使用目标架构创建包含源数据的Experience Platform数据集。

通过对[架构注册表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)执行POST请求，可以创建目标XDM架构。

有关如何创建目标XDM架构的详细步骤，请参阅有关使用API [创建架构的教程](../../../../../xdm/api/schemas.md)。

### 创建目标数据集 {#target-dataset}

通过向[目录服务API](https://developer.adobe.com/experience-platform-apis/references/catalog/)执行POST请求，在有效负载中提供目标架构的ID，可以创建目标数据集。

有关如何创建目标数据集的详细步骤，请参阅有关[使用API创建数据集的教程](../../../../../catalog/api/create-dataset.md)。

## 创建目标连接 {#target}

目标连接表示与所摄取数据所登陆的目标之间的连接。 要创建目标连接，请在为目标数据集和目标XDM架构提供ID时向`/targetConnections`发出POST请求。 在此步骤中，您还必须提供数据湖连接规范ID。 此ID为`c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

**API格式**

```http
POST /flowservice/targetConnections
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Target Connection",
      "description": "ACME Streaming Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "version": "application/vnd.adobe.xed-full+json;version=1.0"
          }
      },
      "params": {
          "dataSetId": "637eb7fadc8a211b6312b65b"
      },
          "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
  }'
```

**响应**

成功的响应返回HTTP状态201，其中包含新创建的目标连接的详细信息，包括其唯一标识符(`id`)。

```json
{
  "id": "07f2f6ff-1da5-4704-916a-c615b873cba9",
  "etag": "\"340680f7-0000-0200-0000-637eb8730000\""
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
      "xdmSchema": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
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
  "id": "79a623960d3f4969835c9e00dc90c8df",
  "version": 0,
  "createdDate": 1669249214031,
  "modifiedDate": 1669249214031,
  "createdBy": "acme@AdobeID",
  "modifiedBy": "acme@AdobeID"
}
```

## 创建数据流

创建源和目标连接后，您现在可以创建数据流。 数据流负责从源中计划和收集数据。 您可以通过对`/flows`端点执行POST请求来创建数据流。

**API格式**

```http
POST /flows
```

**请求**

>[!BEGINTABS]

>[!TAB XDM]

以下请求为XDM数据创建流式数据流。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Streaming Dataflow",
      "description": "ACME streaming dataflow for customer data",
      "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ]
    }'
```

>[!TAB 原始]

以下请求为原始数据创建流式数据流。

创建包含转换的数据流时，无法更改`name`参数。 此值必须始终设置为`Mapping`。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "<name>",
      "description": "<description>",
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "sourceConnectionIds": [
        "34ece231-294d-416c-ad2a-5a5dfb2bc69f"
      ],
      "targetConnectionIds": [
        "07f2f6ff-1da5-4704-916a-c615b873cba9"
      ],
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "79a623960d3f4969835c9e00dc90c8df",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

>[!ENDTABS]

| 属性 | 描述 |
| --- | --- |
| `name` | 您的数据流的名称。 确保数据流的名称是描述性的，因为您可以使用此名称查找数据流上的信息。 |
| `description` | （可选）可包含的属性，用于提供有关数据流的更多信息。 |
| `flowSpec.id` | [!DNL HTTP API]的流规范ID。 要创建包含转换的数据流，必须使用`c1a19761-d2c7-4702-b9fa-fe91f0613e81`。 要创建不含转换的数据流，请使用`d8a6f005-7eaf-4153-983e-e8574508b877`。 |
| `sourceConnectionIds` | 在之前的步骤中检索到[源连接ID](#source)。 |
| `targetConnectionIds` | 在之前的步骤中检索到[目标连接ID](#target)。 |
| `transformations.params.mappingId` | 在之前的步骤中检索到[映射ID](#mapping)。 |

**响应**

成功的响应返回HTTP状态201，其中包含新创建的数据流的详细信息，包括其唯一标识符(`id`)。

```json
{
  "id": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
  "etag": "\"dc0459ae-0000-0200-0000-637ebaec0000\""
}
```

## 发布要引入到Experience Platform的数据 {#ingest-data}

>[!NOTE]
>
>在创建数据流和摄取任何流数据之间必须添加至少约5分钟的延迟。 这样一来，在摄取任何数据之前，都可以完全启用数据流。

现在您已经创建了流，接下来可以将JSON消息发送到之前创建的流端点。

**API格式**

```http
POST /collection/{INLET_URL}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{INLET_URL}` | 您的流端点URL。 您可以在提供基本连接ID的同时向`/connections`端点发出GET请求，以检索此URL。 |
| `{FLOW_ID}` | HTTP API流数据流的ID。 XDM和RAW数据都需要此ID。 |

**请求**

>[!BEGINTABS]

>[!TAB 发送XDM数据]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
  -d '{
        "header": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
          },
          "flowId": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
          "datasetId": "604a18a3bae67d18db6d258c"
        },
        "body": {
          "xdmMeta": {
            "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT}/schemas/7f682c29f887512a897791e7161b90a1ae7ed3dd07a177b1",
              "contentType": "application/vnd.adobe.xed-full-notext+json; version=1.0"
            }
          },
          "xdmEntity": {
            "_id": "http-source-connector-acme-01",
            "person": {
              "name": {
                "firstName": "suman",
                "lastName": "nolan"
              }
            },
            "workEmail": {
              "primary": true,
              "address": "suman@acme.com",
              "type": "work",
              "status": "active"
            }
          }
        }
      }'
```

>[!TAB 将具有流ID的原始数据作为HTTP标头发送]

在发送原始数据时，您可以将流ID指定为查询参数或HTTP标头的一部分。 以下示例将流ID指定为HTTP标头。

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' 
  -H 'x-adobe-flow-id=f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2' \
  -d '{
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

>[!TAB 将具有流ID的原始数据作为查询参数发送]

在发送原始数据时，您可以将流ID指定为查询参数或HTTP标头。 以下示例将流ID指定为查询参数。

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec?x-adobe-flow-id=f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2 \
  -H 'Content-Type: application/json' \
  -d '{
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

>[!ENDTABS]

**响应**

成功的响应返回HTTP状态200以及新摄取信息的详细信息。

```json
{
    "inletId": "{BASE_CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BASE_CONNECTION_ID}` | 之前创建的流连接的ID。 |
| `xactionId` | 在服务器端为您刚刚发送的记录生成的唯一标识符。 此ID可帮助Adobe跟踪此记录在各种系统和调试中的生命周期。 |
| `receivedTimeMs` | 显示收到请求时间的时间戳（以毫秒为单位）。 |


## 后续步骤

通过学习本教程，您已创建一个流HTTP连接，从而能够使用流端点将数据摄取到Experience Platform。 有关在UI中创建流连接的说明，请参阅[创建流连接教程](../../../ui/create/streaming/http.md)。

要了解如何将数据流式传输到Experience Platform，请阅读有关[流式传输时间序列数据](../../../../../ingestion/tutorials/streaming-time-series-data.md)的教程或有关[流式传输记录数据](../../../../../ingestion/tutorials/streaming-record-data.md)的教程。

## 附录

本节提供有关使用API创建流连接的补充信息。

### 向经过身份验证的流连接发送消息

如果流连接启用了身份验证，则客户端需要将`Authorization`标头添加到其请求中。

如果`Authorization`标头不存在，或发送了无效/过期的访问令牌，则将返回HTTP 401未授权响应，其响应如下所示：

**响应**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```


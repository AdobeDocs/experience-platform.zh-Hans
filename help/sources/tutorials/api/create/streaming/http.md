---
keywords: Experience Platform；主页；热门主题；流连接；创建流连接；API指南；教程；创建流连接；流摄取；摄取；
title: 使用流服务API创建HTTP API流连接
description: 本教程提供了有关如何使用流服务API，为原始和XDM数据使用HTTP API源创建流连接的步骤
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 26c967418e983322cc39aa799a681d258638d769
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 3%

---


# 使用创建HTTP API流连接 [!DNL Flow Service] API

流量服务用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供了用户界面和RESTful API，所有受支持的源都可从中连接。

本教程使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 来指导您完成使用 [!DNL Flow Service] API。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md):标准化框架， [!DNL Platform] 组织体验数据。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的消费者用户档案。

此外，创建流连接需要您具有目标XDM架构和数据集。 要了解如何创建这些模板，请阅读 [流记录数据](../../../../../ingestion/tutorials/streaming-record-data.md) 或 [流时间序列数据](../../../../../ingestion/tutorials/streaming-time-series-data.md).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接指定源，并包含使流与流摄取API兼容所需的信息。 创建基本连接时，您可以选择创建未验证和已验证的连接。

### 未验证连接

非身份验证连接是您在要将数据流式传输到Platform时可以创建的标准流连接。

要创建未经身份验证的基本连接，请向 `/connections` 端点，同时为连接、数据类型和HTTP API连接规范ID提供名称。 此ID为 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

**API格式**

```http
POST /flowservice/connections
```

**请求**

以下请求为HTTP API创建基连接。

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
| `name` | 基本连接的名称。 确保该名称具有描述性，因为您可以使用该名称查找有关基本连接的信息。 |
| `description` | （可选）可包含的属性，用于提供有关基本连接的更多信息。 |
| `connectionSpec.id` | 与HTTP API对应的连接规范ID。 此ID为 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`. |
| `auth.params.dataType` | 流连接的数据类型。 支持的值包括： `xdm` 和 `raw`. |
| `auth.params.name` | 要创建的流连接的名称。 |

**响应**

成功响应会返回HTTP状态201，其中包含新创建连接的详细信息，包括其唯一标识符(`id`)。

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 的 `id` 新建的基本连接。 |
| `etag` | 分配给连接的标识符，用于指定基本连接的版本。 |

### 已验证的连接

当您需要区分来自可信来源和不可信来源的记录时，应使用经过身份验证的连接。 要通过个人身份信息(PII)发送信息的用户，应在将信息流式传输到Platform时创建经过身份验证的连接。

要创建经过身份验证的基本连接，您必须指定源ID以及在向发出POST请求时是否需要进行身份验证 `/connections` 端点。


**API格式**

```http
POST /flowservice/connections
```

**请求**

以下请求会为HTTP API创建经过身份验证的基连接。

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
             "sourceId": "{SOURCE_ID}",
             "dataType": "xdm",
             "name": "Sample connection",
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
             "sourceId": "Sample connection",
             "dataType": "raw",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```

>[!ENDTABS]

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.sourceId` | 要创建的流连接的ID。 |
| `auth.params.authenticationRequired` | 指定已创建流连接的参数 |

**响应**

成功响应会返回HTTP状态201，其中包含新创建连接的详细信息，包括其唯一标识符(`id`)。

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

## 获取流端点URL

创建基本连接后，您现在可以检索流端点URL。

**API格式**

```http
GET /flowservice/connections/{BASE_CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 的 `id` 之前创建的连接的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含有关所请求连接的详细信息。 流端点URL将自动通过该连接创建，并可使用 `inletUrl` 值。

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

要创建源连接，请向 `/sourceConnections` 端点。

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

成功响应会返回HTTP状态201，其中包含新创建的源连接的详细信息，包括其唯一标识符(`id`)。

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

## 创建目标XDM架构 {#target-schema}

要在Platform中使用源数据，必须创建目标架构以根据您的需求构建源数据。 然后，目标架构用于创建包含源数据的Platform数据集。

通过对 [架构注册表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

有关如何创建目标XDM架构的详细步骤，请参阅 [使用API创建模式](../../../../../xdm/api/schemas.md).

### 创建目标数据集 {#target-dataset}

通过对 [目录服务API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，在有效负载中提供目标架构的ID。

有关如何创建目标数据集的详细步骤，请参阅 [使用API创建数据集](../../../../../catalog/api/create-dataset.md).

## 创建目标连接 {#target}

目标连接表示所摄取数据所登陆目标的连接。 要创建目标连接，请向发出POST请求 `/targetConnections` 为目标数据集和目标XDM架构提供ID时，不会将ID与ID关联。 在此步骤中，您还必须提供数据湖连接规范ID。 此ID为 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

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

成功响应会返回HTTP状态201，其中包含新创建的目标连接的详细信息，包括其唯一标识符(`id`)。

```json
{
  "id": "07f2f6ff-1da5-4704-916a-c615b873cba9",
  "etag": "\"340680f7-0000-0200-0000-637eb8730000\""
}
```

## 创建映射 {#mapping}

要将源数据摄取到目标数据集，必须先将其映射到目标数据集所附加的目标架构。

要创建映射集，请向 `mappingSets` 的端点 [[!DNL Data Prep] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-prep.yaml) 提供目标XDM模式时 `$id` 以及要创建的映射集的详细信息。

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
| `xdmSchema` | 的 `$id` 目标XDM架构的URL。 |

**响应**

成功的响应会返回新创建映射的详细信息，包括其唯一标识符(`id`)。 在后续步骤中需要此ID才能创建数据流。

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

| 属性 | 描述 |
| --- | --- |

## 创建数据流

创建源连接和目标连接后，您现在可以创建数据流。 数据流负责从源中调度和收集数据。 您可以通过执行对的POST请求来创建数据流 `/flows` 端点。

**API格式**

```http
POST /flows
```

**请求**

>[!BEGINTABS]

>[!TAB 无转换]

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

>[!TAB 具有转换]

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
| `name` | 数据流的名称。 确保数据流的名称具有描述性，因为您可以使用该名称查找有关数据流的信息。 |
| `description` | （可选）可包含的属性，用于提供有关数据流的更多信息。 |
| `flowSpec.id` | 的流量规范ID [!DNL HTTP API]. 要创建包含转换的数据流，您必须使用  `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. 要创建不带转换的数据流，请使用 `d8a6f005-7eaf-4153-983e-e8574508b877`. |
| `sourceConnectionIds` | 的 [源连接ID](#source) 在之前的步骤中检索。 |
| `targetConnectionIds` | 的 [目标连接ID](#target) 在之前的步骤中检索。 |
| `transformations.params.mappingId` | 的 [映射ID](#mapping) 在之前的步骤中检索。 |

**响应**

成功响应会返回HTTP状态201，其中包含新创建的数据流的详细信息，包括其唯一标识符(`id`)。

```json
{
  "id": "f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2",
  "etag": "\"dc0459ae-0000-0200-0000-637ebaec0000\""
}
```


## 要摄取到平台的帖子数据 {#ingest-data}

现在，您已创建流程，接下来可以将JSON消息发送到之前创建的流端点。

**API格式**

```http
POST /collection/{INLET_URL}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{INLET_URL}` | 您的流端点URL。 您可以通过向 `/connections` 端点。 |

**请求**

>[!BEGINTABS]

>[!TAB XDM]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: f2ae0194-8bd8-4a40-a4d9-f07bdc3e6ce2' \
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

>[!TAB 原始数据]

```shell
curl -X POST https://dcs.adobedc.net/collection/667b41cf2dbf3509927da1ebf7e93c20afa727cc8d8373e51da18b62e1b985ec \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: 1f086c23-2ea8-4d06-886c-232ea8bd061d' \
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

成功响应会返回HTTP状态200，其中包含新摄取的信息的详细信息。

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
| `xactionId` | 您刚刚发送的记录在服务器端生成的唯一标识符。 此ID可帮助Adobe通过各种系统和调试来跟踪此记录的生命周期。 |
| `receivedTimeMs` | 时间戳（以毫秒为单位），显示收到请求的时间。 |


## 后续步骤

在本教程之后，您创建了一个流HTTP连接，使您能够使用流端点将数据摄取到平台。 有关在UI中创建流连接的说明，请阅读 [创建流连接教程](../../../ui/create/streaming/http.md).

要了解如何将数据流式传输到Platform，请阅读 [流时间序列数据](../../../../../ingestion/tutorials/streaming-time-series-data.md) 或 [流记录数据](../../../../../ingestion/tutorials/streaming-record-data.md).

## 附录

本节提供了有关使用API创建流连接的补充信息。

### 向经过验证的流连接发送消息

如果流连接启用了身份验证，则将需要客户端添加 `Authorization` 头。

如果 `Authorization` 标头不存在，或者发送了无效/过期的访问令牌，则将返回HTTP 401未授权响应，其响应类似于以下：

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

---
keywords: Experience Platform；主页；热门主题；流连接；创建流连接；API指南；教程；创建流连接；流摄取；摄取；
solution: Experience Platform
title: 使用API创建流连接
topic-legacy: tutorial
type: Tutorial
description: 本教程将帮助您开始使用流摄取API，这是Adobe Experience Platform数据摄取服务API的一部分。
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 42b8710cf6c04fabf7df1f005fae6b3828eeee49
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 3%

---


# 使用API创建流连接

流量服务用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供了用户界面和RESTful API，所有受支持的源都可从中连接。

本教程使用[!DNL Flow Service] API指导您完成使用流服务API创建流连接的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md):用于组织体验数据 [!DNL Platform] 的标准化框架。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的消费者用户档案。

此外，创建流连接需要您具有目标XDM架构和数据集。 要了解如何创建这些数据，请阅读[流记录数据](../../../../../ingestion/tutorials/streaming-record-data.md)的教程或[流时间系列数据](../../../../../ingestion/tutorials/streaming-time-series-data.md)的教程。

以下部分提供了成功调用流摄取API所需了解的其他信息。

### 读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅[!DNL Experience Platform]疑难解答指南中[如何阅读示例API调用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程可为所有[!DNL Experience Platform] API调用中每个所需标头的值，如下所示：

- 授权：载体`{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都与特定虚拟沙箱隔离。 对[!DNL Platform] API的所有请求都需要一个标头来指定操作将在其中进行的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的更多信息，请参阅[沙盒概述文档](../../../../../sandboxes/home.md)。

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

- Content-Type:application/json

## 创建基本连接

基本连接指定源，并包含使流与流摄取API兼容所需的信息。 创建基本连接时，您可以选择创建未验证和已验证的连接。

### 未验证连接

非身份验证连接是您在要将数据流式传输到Platform时可以创建的标准流连接。

**API格式**

```http
POST /flowservice/connections
```

**请求**

要创建流连接，必须在POST请求中提供提供商ID和连接规范ID。 提供程序ID为`521eee4d-8cbe-4906-bb48-fb6bd4450033`，连接规范ID为`bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`。

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.sourceId` | 要创建的流连接的ID。 |
| `auth.params.dataType` | 流连接的数据类型。 此值必须为`xdm`。 |
| `auth.params.name` | 要创建的流连接的名称。 |
| `connectionSpec.id` | 流连接的连接规范`id`。 |

**响应**

成功响应会返回HTTP状态201，其中包含新创建连接的详细信息，包括其唯一标识符(`id`)。

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 新创建连接的`id`。 这在此称为`{CONNECTION_ID}`。 |
| `etag` | 分配给连接的标识符，用于指定连接的修订版本。 |

### 已验证的连接

当您需要区分来自可信来源和不可信来源的记录时，应使用经过身份验证的连接。 要通过个人身份信息(PII)发送信息的用户，应在将信息流式传输到Platform时创建经过身份验证的连接。

**API格式**

```http
POST /flowservice/connections
```

**请求**

要创建流连接，必须在POST请求中提供提供商ID和连接规范ID。 提供程序ID为`521eee4d-8cbe-4906-bb48-fb6bd4450033`，连接规范ID为`bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`。

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```


| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.sourceId` | 要创建的流连接的ID。 |
| `auth.params.dataType` | 流连接的数据类型。 此值必须为`xdm`。 |
| `auth.params.name` | 要创建的流连接的名称。 |
| `auth.params.authenticationRequired` | 指定已创建流连接的参数 |
| `connectionSpec.id` | 流连接的连接规范`id`。 |

**响应**

成功响应会返回HTTP状态201，其中包含新创建连接的详细信息，包括其唯一标识符(`id`)。

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 新创建连接的`id`。 这在此称为`{CONNECTION_ID}`。 |
| `etag` | 分配给连接的标识符，用于指定连接的修订版本。 |

## 获取流端点URL

创建基本连接后，您现在可以检索流端点URL。

**API格式**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 您之前创建的连接的`id`值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含有关所请求连接的详细信息。 流端点URL将通过连接自动创建，并可使用`inletUrl`值进行检索。

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## 创建源连接

创建基本连接后，需要创建源连接。 创建源连接时，您需要创建的基连接中的`id`值。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample source connection",
    "description": "Sample source connection description",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
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
    "id": "63070871-ec3f-4cb5-af47-cf7abb25e8bb",
    "etag": "\"28000b90-0000-0200-0000-6091b0150000\""
}
```

## 创建目标连接

创建源连接后，可以创建目标连接。 创建Target连接时，您将需要之前创建的数据集的`id`值。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample target connection",
    "description": "Sample target connection description",
    "connectionSpec": {
        "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
        "version": "1.0"
    },
    "data": {
        "format": "parquet_xdm"
    },
    "params": {
        "dataSetId": "{DATASET_ID}"
    }
}'
```

**响应**

成功响应会返回HTTP状态201，其中包含新创建的目标连接的详细信息，包括其唯一标识符(`id`)。

```json
{
    "id": "98a2a72e-a80f-49ae-aaa3-4783cc9404c2",
    "etag": "\"0500b73f-0000-0200-0000-6091b0b90000\""
}
```

## 创建数据流

创建源连接和目标连接后，您现在可以创建数据流。 数据流负责从源中调度和收集数据。 通过对`/flows`端点执行POST请求，可以创建数据流。

**API格式**

```http
POST /flows
```

**请求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Sample flow",
    "description": "Sample flow description",
    "flowSpec": {
        "id": "d8a6f005-7eaf-4153-983e-e8574508b877",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "{SOURCE_CONNECTION_ID}"
    ],
    "targetConnectionIds": [
        "{TARGET_CONNECTION_ID}"
    ]
}'
```

**响应**

成功响应会返回HTTP状态201，其中包含新创建的数据流的详细信息，包括其唯一标识符(`id`)。

```json
{
    "id": "ab03bde0-86f2-45c7-b6a5-ad8374f7db1f",
    "etag": "\"1200c123-0000-0200-0000-6091b1730000\""
}
```

## 后续步骤

在本教程之后，您创建了一个流HTTP连接，使您能够使用流端点将数据摄取到平台。 有关在UI中创建流连接的说明，请阅读[创建流连接教程](../../../ui/create/streaming/http.md)。

要了解如何将数据流式传输到Platform，请阅读[流时间系列数据](../../../../../ingestion/tutorials/streaming-time-series-data.md)的教程或[流记录数据](../../../../../ingestion/tutorials/streaming-record-data.md)的教程。

## 附录

本节提供了有关使用API创建流连接的补充信息。

### 向经过验证的流连接发送消息

如果流连接启用了身份验证，则需要客户端将`Authorization`标头添加到其请求中。

如果`Authorization`标头不存在，或发送了无效/过期的访问令牌，则将返回HTTP 401未授权响应，响应类似于以下：

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

### 将要摄取到平台的原始数据发布到Platform {#ingest-data}

现在，您已创建流程，接下来可以将JSON消息发送到之前创建的流端点。

**API格式**

```http
POST /collection/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 新创建的流连接的`id`值。 |

**请求**

该示例请求会将原始数据摄取到之前创建的流端点。

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
      "gender": "Male",
      "birthday": {
          "year": 1984,
          "month": 6,
          "day": 9
      }
  }'
```

**响应**

成功响应会返回HTTP状态200，其中包含新摄取的信息的详细信息。

```json
{
    "inletId": "{CONNECTION_ID}",
    "xactionId": "1584479347507:2153:240",
    "receivedTimeMs": 1584479347507
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 之前创建的流连接的ID。 |
| `xactionId` | 您刚刚发送的记录在服务器端生成的唯一标识符。 此ID可帮助Adobe通过各种系统和调试来跟踪此记录的生命周期。 |
| `receivedTimeMs` | 时间戳（以毫秒为单位），显示收到请求的时间。 |

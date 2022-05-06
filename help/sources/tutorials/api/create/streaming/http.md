---
keywords: Experience Platform；主页；热门主题；流连接；创建流连接；API指南；教程；创建流连接；流摄取；摄取；
solution: Experience Platform
title: 使用API创建HTTP API流连接
topic-legacy: tutorial
type: Tutorial
description: 本教程将帮助您开始使用流摄取API，这是Adobe Experience Platform数据摄取服务API的一部分。
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 2%

---


# 创建 [!DNL HTTP API] 使用API的流连接

流量服务用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供了用户界面和RESTful API，所有受支持的源都可从中连接。

本教程使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) 来指导您完成使用流服务API创建流连接的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md):标准化框架， [!DNL Platform] 组织体验数据。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的消费者用户档案。

此外，创建流连接需要您具有目标XDM架构和数据集。 要了解如何创建这些模板，请阅读 [流记录数据](../../../../../ingestion/tutorials/streaming-record-data.md) 或 [流时间序列数据](../../../../../ingestion/tutorials/streaming-time-series-data.md).

以下部分提供了成功调用流摄取API所需了解的其他信息。

### 读取示例API调用

本指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform]，包括属于 [!DNL Flow Service]，与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../../../../sandboxes/home.md).

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

要创建流连接，必须在POST请求中提供提供商ID和连接规范ID。 提供程序ID为 `521eee4d-8cbe-4906-bb48-fb6bd4450033` 连接规范ID是 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
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
| `auth.params.dataType` | 流连接的数据类型。 此值必须为 `xdm`. |
| `auth.params.name` | 要创建的流连接的名称。 |
| `connectionSpec.id` | 连接规范 `id` 用于流连接。 |

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
| `id` | 的 `id` 新建连接的URL。 这在这里称为 `{CONNECTION_ID}`. |
| `etag` | 分配给连接的标识符，用于指定连接的修订版本。 |

### 已验证的连接

当您需要区分来自可信来源和不可信来源的记录时，应使用经过身份验证的连接。 要通过个人身份信息(PII)发送信息的用户，应在将信息流式传输到Platform时创建经过身份验证的连接。

**API格式**

```http
POST /flowservice/connections
```

**请求**

要创建流连接，必须在POST请求中提供提供商ID和连接规范ID。 提供程序ID为 `521eee4d-8cbe-4906-bb48-fb6bd4450033` 连接规范ID是 `bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`.

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
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
| `auth.params.dataType` | 流连接的数据类型。 此值必须为 `xdm`. |
| `auth.params.name` | 要创建的流连接的名称。 |
| `auth.params.authenticationRequired` | 指定已创建流连接的参数 |
| `connectionSpec.id` | 连接规范 `id` 用于流连接。 |

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
| `id` | 的 `id` 新建连接的URL。 这在这里称为 `{CONNECTION_ID}`. |
| `etag` | 分配给连接的标识符，用于指定连接的修订版本。 |

## 获取流端点URL

创建基本连接后，您现在可以检索流端点URL。

**API格式**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 的 `id` 之前创建的连接的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
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

## 创建源连接 {#source}

创建基本连接后，需要创建源连接。 创建源连接时，您将需要 `id` 值。

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

## 创建目标XDM架构 {#target-schema}

要在Platform中使用源数据，必须创建目标架构以根据您的需求构建源数据。 然后，目标架构用于创建包含源数据的Platform数据集。

通过对 [架构注册表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

有关如何创建目标XDM架构的详细步骤，请参阅 [使用API创建模式](../../../../../xdm/api/schemas.md).

### 创建目标数据集 {#target-dataset}

通过对 [目录服务API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，在有效负载中提供目标架构的ID。

有关如何创建目标数据集的详细步骤，请参阅 [使用API创建数据集](../../../../../catalog/api/create-dataset.md).

## 创建目标连接 {#target}

目标连接表示所摄取数据所登陆目标的连接。 要创建目标连接，必须提供与数据湖关联的固定连接规范ID。 此连接规范ID为： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

现在，您将唯一标识符作为目标数据集的目标架构，并将连接规范ID用于数据湖。 使用这些标识符，您可以使用 [!DNL Flow Service] 用于指定将包含集客源数据的数据集的API。

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
| `xdmSchema` | 的 `$id` 目标XDM架构的URL。 |

**响应**

成功的响应会返回新创建映射的详细信息，包括其唯一标识符(`id`)。 在后续步骤中需要此ID才能创建数据流。

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

## 创建数据流

创建源连接和目标连接后，您现在可以创建数据流。 数据流负责从源中调度和收集数据。 您可以通过执行对的POST请求来创建数据流 `/flows` 端点。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "HTTP API streaming dataflow",
        "description": "HTTP API streaming dataflow",
        "flowSpec": {
            "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "63070871-ec3f-4cb5-af47-cf7abb25e8bb"
        ],
        "targetConnectionIds": [
            "98a2a72e-a80f-49ae-aaa3-4783cc9404c2"
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
| `flowSpec.id` | 的流量规范ID [!DNL HTTP API]. 此ID为： `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
| `sourceConnectionIds` | 的 [源连接ID](#source) 在之前的步骤中检索。 |
| `targetConnectionIds` | 的 [目标连接ID](#target) 在之前的步骤中检索。 |
| `transformations.params.mappingId` | 的 [映射ID](#mapping) 在之前的步骤中检索。 |

**响应**

成功响应会返回HTTP状态201，其中包含新创建的数据流的详细信息，包括其唯一标识符(`id`)。

```json
{
    "id": "ab03bde0-86f2-45c7-b6a5-ad8374f7db1f",
    "etag": "\"1200c123-0000-0200-0000-6091b1730000\""
}
```

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

### 将要摄取到平台的原始数据发布到Platform {#ingest-data}

现在，您已创建流程，接下来可以将JSON消息发送到之前创建的流端点。

**API格式**

```http
POST /collection/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 的 `id` 新建流连接的值。 |

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

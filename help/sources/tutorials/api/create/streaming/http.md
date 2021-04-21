---
keywords: Experience Platform；主页；热门主题；流连接；创建流连接；api指南；教程；创建流连接；流摄取；
solution: Experience Platform
title: 使用API创建流连接
topic-legacy: tutorial
type: Tutorial
description: 本教程将帮助您开始使用流式摄取API，它是Adobe Experience Platform Data Ingestion Service API的一部分。
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 2%

---


# 使用API创建流连接

流服务用于收集和集中来自Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有受支持的源都可从中连接。

本教程使用[!DNL Flow Service] API指导您使用流服务API创建流连接的步骤。

## 入门指南

本指南要求对Adobe Experience Platform的以下组件有充分的了解：

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md):用于组织体验数 [!DNL Platform] 据的标准化框架。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据实时提供统一的消费者用户档案。

以下各节提供了成功调用流化Ingestion API所需了解的其他信息。

### 读取示例API调用

本指南提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中关于如何读取示例API调用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。[

### 收集所需标题的值

要调用[!DNL Platform] API，您必须首先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

- 授权：承载`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个头，该头指定操作将在中执行的沙箱的名称：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙箱的详细信息，请参阅[沙箱概述文档](../../../../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

- 内容类型：application/json

## 创建连接

连接指定源并包含使流与流摄取API兼容所需的信息。 创建连接时，您可以选择创建未验证和已验证的连接。

### 未验证连接

非身份验证连接是您在希望将数据流到平台时可以创建的标准流连接。

**API格式**

```http
POST /flowservice/connections
```

**请求**

要创建流连接，必须在POST请求中提供提供者ID和连接规范ID。 提供程序ID为`521eee4d-8cbe-4906-bb48-fb6bd4450033`，连接规范ID为`bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`。

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
 }
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.sourceId` | 要创建的流连接的ID。 |
| `auth.params.dataType` | 流连接的数据类型。 此值必须为`xdm`。 |
| `auth.params.name` | 要创建的流连接的名称。 |
| `connectionSpec.id` | 用于流连接的连接规范`id`。 |

**响应**

成功的响应返回HTTP状态201，其中包含新创建的连接的详细信息，包括其唯一标识符(`id`)。

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 您新创建的连接的`id`。 此处将称为`{CONNECTION_ID}`。 |
| `etag` | 分配给连接的标识符，指定连接的修订版本。 |

### 已验证的连接

需要区分来自可信和不可信来源的记录时，应使用经过身份验证的连接。 希望使用个人身份信息(PII)发送信息的用户应在将信息流到平台时创建经过身份验证的连接。

**API格式**

```http
POST /flowservice/connections
```

**请求**

要创建流连接，必须在POST请求中提供提供者ID和连接规范ID。 提供程序ID为`521eee4d-8cbe-4906-bb48-fb6bd4450033`，连接规范ID为`bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`。

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
| `auth.params.authenticationRequired` | 指定已创建的流连接的参数 |
| `connectionSpec.id` | 用于流连接的连接规范`id`。 |

**响应**

成功的响应返回HTTP状态201，其中包含新创建的连接的详细信息，包括其唯一标识符(`id`)。

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 您新创建的连接的`id`。 此处将称为`{CONNECTION_ID}`。 |
| `etag` | 分配给连接的标识符，指定连接的修订版本。 |

## 获取流端点URL

创建连接后，您现在可以检索流端点URL。

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

成功的响应返回HTTP状态200，其中包含有关所请求连接的详细信息。 流端点URL是使用连接自动创建的，可使用`inletUrl`值进行检索。

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

## 后续步骤

通过本教程，您创建了一个流式HTTP连接，使您能够使用流式端点将数据引入平台。 有关在UI中创建流连接的说明，请阅读[创建流连接教程](../../../ui/create/streaming/http.md)。

要了解如何将数据流化到平台，请阅读关于[流式时间系列数据](../../../../../ingestion/tutorials/streaming-time-series-data.md)的教程或关于[流式记录数据](../../../../../ingestion/tutorials/streaming-record-data.md)的教程。

## 附录

本节提供有关使用API创建流连接的补充信息。

### 向经过身份验证的流连接发送消息

如果流连接启用了身份验证，则客户端需要向其请求中添加`Authorization`头。

如果`Authorization`标头不存在，或发送了无效/过期的访问令牌，则将返回HTTP 401未授权响应，响应类似如下：

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

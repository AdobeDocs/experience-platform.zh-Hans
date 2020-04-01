---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 创建经过身份验证的流连接
topic: tutorial
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a

---


# 创建经过身份验证的流连接

通过身份验证的数据收集，Adobe Experience Platform服务(如实时客户用户档案和身份)可区分来自可信来源和不可信来源的记录。 要发送个人识别信息(PII)的客户可以通过发送访问令牌作为POST请求的一部分来发送。

## 入门指南

要将流数据开始到Adobe Experience Platform，需要流连接注册。 注册流连接时，您需要提供一些关键详细信息，如流数据源。

在注册流连接后，作为数据生成者，您将拥有一个唯一的URL，可用于向平台流化数据。

本教程还需要了解各种Adobe Experience Platform服务的工作知识。 在开始本教程之前，请查看以下服务的相关文档：

- [体验数据模型(XDM)](../../xdm/home.md):平台组织体验数据的标准化框架。
- [实时客户用户档案](../../profile/home.md):根据来自多个来源的汇总数据实时提供统一的消费者用户档案。

以下各节提供了成功调用流化摄取API所需了解的其他信息。

### 读取示例API调用

本指南提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

- 授权：承载人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

- 内容类型：application/json

## 创建连接

连接指定源并包含使流与流摄取API兼容所需的信息。

**API格式**

```http
POST /flowservice/connections
```

**请求**

>[!NOTE] 必须如示 `providerId` 例所示使用列 `connectionSpec` 出的值和值 **** ，因为它们是您为流摄取创建流连接的API的指定值。

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
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

**响应**

成功的响应会返回HTTP状态201，其中包含新创建的连接的详细信息。

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 您新 `id` 创建的连接的名称。 此处将称为 `{CONNECTION_ID}`。 |
| `etag` | 分配给连接的标识符，用于指定连接的修订版。 |

## 获取数据收集URL

创建连接后，您现在可以检索数据收集URL。

**API格式**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 您 `id` 之前创建的连接的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态200，其中包含有关所请求连接的详细信息。 数据收集URL是使用该连接自动创建的，并且可以使用该值进行检 `inletUrl` 索。

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

现在您已经创建了经过身份验证的流连接，您可以流化时间序列或记录数据，从而允许您在平台内摄取数据。 要了解如何将时间序列数据流化到平台，请转到流 [式时间序列数据教程](./streaming-time-series-data.md)。 要了解如何将记录数据流化到平台，请转到流 [化记录数据教程](./streaming-record-data.md)。

## 附录

本节提供有关经过身份验证的流连接的补充信息。

### 向经过身份验证的流连接发送消息

如果流连接已启用身份验证，则客户端将需要向其请 `Authorization` 求添加头。

如果 `Authorization` 头不存在，或者发送了无效／过期的访问令牌，则将返回HTTP 401未授权响应，响应类似如下：

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

### 使用授权将消息发送到未经身份验证的流连接

如果流连接未启用身份验证，则客户端仍可（可选）将头添加 `Authorization` 到其请求中。

如果 `Authorization` 头不存在，或者发送了无效／过期的访问令牌，则将返回HTTP 401未授权响应，数据仍将发布，但字段将设 `authenticatedRequest` 置为 `false`。

如果标 `Authorization` 题存在且有效，则数据将随字段设置一起 `authenticatedRequest` 发布到 `true`。
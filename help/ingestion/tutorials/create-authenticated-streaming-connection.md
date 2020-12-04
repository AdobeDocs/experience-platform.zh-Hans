---
keywords: Experience Platform;home;popular topics;authenticated streaming connection;streaming connection;create streaming connection;create authenticated streaming connection;streaming ingestion;ingestion;
solution: Experience Platform
title: 创建经过身份验证的流连接
topic: tutorial
type: Tutorial
description: 通过实名数据收集，Adobe Experience Platform服务(如实时客户用户档案和身份)可以区分来自可信来源和不可信来源的记录。
translation-type: tm+mt
source-git-commit: 37356db1666b0c800119b1e254940ad72550848a
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 2%

---


# 创建经过身份验证的流连接

经身份验证的数据收集使Adobe Experience Platform服务(如 [!DNL Real-time Customer Profile] 和) [!DNL Identity]能够区分来自可信来源和不可信来源的记录。 要发送个人身份信息(PII)的客户可以通过作为访问令牌请求的一部分发送POST来发送个人身份信息。

## 入门指南

要向Adobe Experience Platform开始流数据，需要流连接注册。 注册流连接时，您需要提供一些关键详细信息，如流数据源。

注册流连接后，作为数据生成者，您将拥有一个可用于将数据流化到的唯一URL [!DNL Platform]。

本教程还需要掌握Adobe Experience Platform各项服务的工作知识。 在开始本教程之前，请查看以下服务的相关文档：

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):组织体验数据 [!DNL Platform] 的标准化框架。
- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据实时提供统一的消费者用户档案。

以下各节提供了成功调用流式摄取API所需了解的其他信息。

### 读取示例API调用

本指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

- 授权：承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

- 内容类型：application/json

## 创建连接

连接指定源并包含使流与流摄取API兼容所需的信息。

**API格式**

```http
POST /flowservice/connections
```

**请求**

>[!NOTE]
>
>必须如示例 `providerId` 所 `connectionSpec` 示使 **用** 列出的值和值，因为它们是您为流接收创建流连接的API的指定值。

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
| `etag` | 分配给连接的标识符，指定连接的修订版。 |

## 获取数据收集URL

创建连接后，您现在可以检索数据收集URL。

**API格式**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 您之 `id` 前创建的连接的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含有关所请求连接的详细信息。 数据收集URL是使用该连接自动创建的，并且可以使用该值进行 `inletUrl` 检索。

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

现在您已创建经过身份验证的流连接，您可以流式传输时间序列或记录数据，从而在中收集数据 [!DNL Platform]。 要了解如何将时间系列数据流式传 [!DNL Platform]输到，请转 [到流式时间序列数据教程](./streaming-time-series-data.md)。 要了解如何将记录数据流化 [!DNL Platform]到，请转到流 [化记录数据教程](./streaming-record-data.md)。

## 附录

本节提供有关经过身份验证的流连接的补充信息。

### 向经过身份验证的流连接发送消息

如果流连接启用了身份验证，则客户端将需要向其请 `Authorization` 求添加头。

如果头 `Authorization` 不存在，或者发送了无效／过期的访问令牌，则将返回HTTP 401未授权响应，其响应类似如下：

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

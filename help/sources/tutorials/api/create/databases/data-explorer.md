---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API创建Azure Data Explorer连接器
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 1%

---


# 使用Flow Service API创建Azure Data Explorer连接器

>[!NOTE]
>Azure Data Explorer连接器处于测试状态。 功能和文档可能会发生更改。

Flow Service用于在Adobe Experience Platform内收集和集中来自不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用Flow Service API指导您完成将Azure Data Explorer（以下简称“Data Explorer”）连接到Experience Platform的步骤。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md): Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和改进数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用流服务API成功连接到数据资源管理器。

### 收集所需的凭据

要使流服务与数据资源管理器连接，您必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `endpoint` | Data Explorer服务器的端点。 |
| `database` | Data Explorer数据库的名称。 |
| `tenant` | 用于连接到Data Explorer数据库的唯一租户ID。 |
| `servicePrincipalId` | 用于连接到Data Explorer数据库的唯一服务主体ID。 |
| `servicePrincipalKey` | 用于连接到Data Explorer数据库的唯一服务主体键。 |
| `connectionSpec.id` | 创建连接所需的唯一标识符。 数据浏览器的连接规范ID为 `0479cc14-7651-4354-b233-7480606c2ac3`。 |

有关快速入门的详细信息，请参 [阅此数据浏览器文档](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的部分。

### 收集所需标题的值

要调用平台API，您必须先完成身份验证 [教程](../../../../../tutorials/authentication.md)。 完成身份验证教程后，将提供所有Experience Platform API调用中每个所需标头的值，如下所示：

* 授权： 承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源（包括属于流服务的资源）都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* 内容类型： `application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个Data Explorer帐户只需一个连接器，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建数据浏览器连接，其唯一连接规范ID必须作为POST请求的一部分提供。 数据浏览器的连接规范ID为 `0479cc14-7651-4354-b233-7480606c2ac3`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Data Explorer connection",
        "description": "A connection for Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.endpoint` | Data Explorer服务器的端点。 |
| `auth.params.database` | Data Explorer数据库的名称。 |
| `auth.params.tenant` | 用于连接到Data Explorer数据库的唯一租户ID。 |
| `auth.params.servicePrincipalId` | 用于连接到Data Explorer数据库的唯一服务主体ID。 |
| `auth.params.servicePrincipalKey` | 用于连接到Data Explorer数据库的唯一服务主体键。 |
| `connectionSpec.id` | 数据资源管理器连接规范ID: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**响应**

成功的响应会返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## 后续步骤

通过本教程，您已使用Flow Service API创建了一个Data Explorer连接，并获得了该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您将学习如 [何使用流服务API浏览数据库](../../explore/database-nosql.md)。

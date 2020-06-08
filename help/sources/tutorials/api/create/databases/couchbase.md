---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API创建CouchBase连接器
topic: overview
translation-type: tm+mt
source-git-commit: 566db28997dce2c7e1181d140f12adc4250f5e0d
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 2%

---


# 使用Flow Service API创建CouchBase连接器

>[!NOTE]
>CouchBase连接器为测试版。 功能和文档可能会发生更改。

Flow Service用于收集和集中来自不同来源的客户数据，以引入Adobe Experience Platform。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用Flow Service API指导您完成将CouchBase连接到Experience Platform的步骤。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md): Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和改进数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用Flow Service API成功连接到CouchBase。

### 收集所需的凭据

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 用于连接到CouchBase实例的连接字符串。 CouchBase的连接字符串模式为 `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`。 有关获取连接字符串的详细信息，请参 [阅此CouchBase文档](https://docs.couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview)。 |
| `connectionSpec.id` | 创建连接所需的标识符。 CouchBase的固定连接规范ID为 `1fe283f6-9bec-11ea-bb37-0242ac130002`。 |

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

连接指定源并包含该源的凭据。 每个CouchBase帐户只需要一个连接器，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

以下请求创建新的CouchBase连接，该连接由有效负荷中提供的属性进行配置：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "CouchBase test connection",
        "description": "A test connection for a CouchBase source",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                    "connectionString": "Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];"
                }
        },
        "connectionSpec": {
            "id": "1fe283f6-9bec-11ea-bb37-0242ac130002",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.connectionString` | 用于连接到CouchBase帐户的连接字符串。 连接字符串模式为： `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. |
| `connectionSpec.id` | CouchBase连接规范ID: `1fe283f6-9bec-11ea-bb37-0242ac130002`. |

**响应**

成功的响应会返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "54997109-07b5-40b7-9971-0907b5a0b75a",
    "etag": "\"280168f5-0000-0200-0000-5ed72b230000\""
}
```

## 后续步骤

通过本教程，您已使用Flow Service API创建了CouchBase连接，并已获得该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您将学习如 [何使用流服务API浏览数据库](../../explore/database-nosql.md)。

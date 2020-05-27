---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API创建PostgreSQL连接器
topic: overview
translation-type: tm+mt
source-git-commit: 0a2247a9267d4da481b3f3a5dfddf45d49016e61
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 2%

---


# 使用Flow Service API创建PostgreSQL连接器

>[!NOTE]
>PostgreSQL连接器处于测试版中。 功能和文档可能会发生更改。

Flow Service用于在Adobe Experience Platform内收集和集中来自不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用Flow Service API指导您完成将Experience Platform连接到PostgreSQL（以下简称“PSQL”）的步骤。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md): Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和改进数字体验应用程序。

以下各节提供了使用流服务API成功连接到PSQL所需了解的其他信息。

### 收集所需的凭据

要使流服务与PSQL连接，必须提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 与您的PSQL帐户关联的连接字符串。 PSQL连接字符串模式为： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | 用于生成连接的ID。 PSQL的固定连接规范ID为 `74a1c565-4e59-48d7-9d67-7c03b8a13137`。 |

有关获取连接字符串的详细信息，请参 [阅此PSQL文档](https://www.postgresql.org/docs/9.2/app-psql.html)。

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

连接指定源并包含该源的凭据。 每个PSQL帐户只需要一个连接，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建PSQL连接，其唯一连接规范ID必须作为POST请求的一部分提供。 PSQL的连接规范ID为 `74a1c565-4e59-48d7-9d67-7c03b8a13137`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for PostgreSQL",
        "description": "Test connection for PostgreSQL",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| ------------- | --------------- |
| `auth.params.connectionString` | 与您的PSQL帐户关联的连接字符串。 PSQL连接字符串模式为： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | PSQL的连接规范ID为： `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**响应**

成功的响应会返回新创建的基`id`础连接的唯一标识符()。 在下一个教程中浏览PSQL数据库需要此ID。

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## 后续步骤

通过本教程，您已使用Flow Service API创建了PSQL连接，并获得了该连接的唯一ID值。 在下一个教程中，您可以使用此连接ID，因为您将学习 [如何使用流服务API浏览数据库或NoSQL系统](../../explore/database-nosql.md)。

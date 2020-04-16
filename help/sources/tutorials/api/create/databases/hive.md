---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在Azure HDInsights连接器上使用Flow Service API创建Apache Hive
topic: overview
translation-type: tm+mt
source-git-commit: d9792bd87e6e0811e7a165bbde324a99a9cfd5c9

---


# 在Azure HDInsights连接器上使用Flow Service API创建Apache Hive

Flow Service用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用Flow Service API指导您完成将Azure HDInsights上的Apache Hive连接到Experience Platform的步骤。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用Flow Service API成功连接到Hive。

### 收集所需的凭据

要使Flow Service与Hive连接，您必须为以下连接属性提供值：

| 凭证 | 描述 |
| ---------- | ----------- |
| `host` | Hive服务器的IP地址或主机名。 |
| `username` | 用于访问Hive服务器的用户名。 |
| `password` | 与用户对应的口令。 |
| `connectionSpec.id` | 创建连接所需的唯一标识符。 Hive的连接规范ID是： `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f` |

有关快速入门的详细信息，请参 [阅此Hive文档](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../../../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

* 授权：承载人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源（包括属于流服务的资源）都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标题：

* 内容类型： `application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个Hive帐户只需要一个连接，因为它可用于创建多个源连接器以引入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建Hive连接，其唯一的连接规范ID必须作为POST请求的一部分提供。 Hive的连接规范ID是 `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Apache Hive test connection",
        "description": "A test connection for Apache Hive",
        "auth": {
            "specName": "HDInsights Basic Authentication",
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.connectionString` | 与您的Hive帐户关联的连接字符串。 |
| `connectionSpec.id` | Hive连接规范ID: `aac9bbd4-6c01-46ce-b47e-51c6f0f6db3f`. |

**响应**

成功的响应会返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "9f6e4311-e032-4c00-ae43-11e032bc00c7",
    "etag": "\"f4004fb7-0000-0200-0000-5e865c1e0000\""
}
```

## 后续步骤

通过本教程，您使用Flow Service API创建了Hive连接，并获得了该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您将学习如何 [使用Flow Service API浏览数据库](../../explore/database-nosql.md)。

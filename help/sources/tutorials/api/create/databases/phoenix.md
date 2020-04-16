---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API创建Phoenix连接器
topic: overview
translation-type: tm+mt
source-git-commit: c00edf487404e1d08bc86cb6692325f536964af6

---


# 使用Flow Service API创建Phoenix连接器

Flow Service用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用Flow Service API指导您完成将Phoenix数据库连接到Experience Platform的步骤。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用Flow Service API成功连接到Phoenix。

### 收集所需的凭据

为了使Flow Service与Phoenix连接，您必须为以下连接属性提供值：

| 凭证 | 描述 |
| ---------- | ----------- |
| `host` | Phoenix服务器的IP地址或主机名。 |
| `username` | 用于访问Phoenix服务器的用户名。 |
| `password` | 与用户对应的口令。 |
| `port` | Phoenix服务器用于侦听客户端连接的TCP端口。 如果连接到Azure HDInsights，请指定端口为443。 |
| `httpPath` | 与Phoenix服务器对应的部分URL。 如果使用Azure HDInsights群集，请指定/hbasephoenix0。 |
| `enableSsl` | 布尔值。 指定是否使用SSL加密与服务器的连接。 |
| `connectionSpec.id` | 创建连接所需的唯一标识符。 菲尼克斯的连接规范ID是： `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

有关入门的详细信息，请参 [阅这篇菲尼克斯文档](https://python-phoenixdb.readthedocs.io/en/latest/api.html)。

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

连接指定源并包含该源的凭据。 每个Phoenix帐户只需要一个连接，因为它可用于创建多个源连接器以引入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建Phoenix连接，其唯一的连接规范ID必须作为POST请求的一部分提供。 菲尼克斯的连接规范ID是 `102706fb-a5cd-42ee-afe0-bc42f017ff43`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}",
            "port" : {PORT},
            "httpPath" : "{PATH}",
            "enableSsl" : {SSL}
            }
        },
        "connectionSpec": {
            "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.host` | Phoenix服务器的主机。 |
| `auth.params.username` | 与您的Phoenix连接关联的用户名。 |
| `auth.params.password` | 与您的Phoenix连接关联的密码。 |
| `auth.params.port` | 用于Phoenix连接的TCP端口。 |
| `auth.params.httpPath` | Phoenix连接的部分http路径。 |
| `auth.params.enableSsl` | 布尔值，它指定是否使用SSL加密与服务器的连接。 |
| `connectionSpec.id` | Phoenix连接规范ID: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**响应**

成功的响应会返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 后续步骤

通过本教程，您已使用Flow Service API创建了Phoenix连接，并已获得该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您将学习如何 [使用Flow Service API浏览数据库](../../explore/database-nosql.md)。
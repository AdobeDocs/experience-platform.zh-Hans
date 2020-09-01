---
keywords: Experience Platform;home;popular topics;Apache Cassandra;apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: 使用Flow Service API创建Apache Cassandra连接器
topic: overview
description: 本教程使用Flow Service API指导您完成将Apache Cassandra（以下简称“Cassandra”）连接到Experience Platform的步骤。
translation-type: tm+mt
source-git-commit: 25f1dfab07d0b9b6c2ce5227b507fc8c8ecf9873
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---


# 使用API [!DNL Apache Cassandra] 创建连接 [!DNL Flow Service] 器

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使 [!DNL Flow Service] 用API指导您完成将 [!DNL Apache Cassandra] 其连接（以下称为“Cassandra”）的步骤 [!DNL Experience Platform]。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用API成功连接到Cassandra [!DNL Flow Service] 。

### 收集所需的凭据

要连接 [!DNL Flow Service] ，必须 [!DNL Cassandra]为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 服务器的IP地址或主 [!DNL Cassandra] 机名。 |
| `port` | 服务器用于侦 [!DNL Cassandra] 听客户端连接的TCP端口。 The default port is `9042`. |
| `username` | 用于连接到服务器进行身 [!DNL Cassandra] 份验证的用户名。 |
| `password` | 连接到服务器进行身 [!DNL Cassandra] 份验证的口令。 |
| `connectionSpec.id` | 创建连接所需的唯一标识符。 连接规范ID [!DNL Cassandra] 为 `a8f4d393-1a6b-43f3-931f-91a16ed857f4`。 |

有关快速入门的详细信息，请参 [阅此Cassandra文档](https://cassandra.apache.org/doc/latest/operating/security.html#authentication)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../../../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

* 授权：承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有资 [!DNL Experience Platform]源(包括属于这些资源 [!DNL Flow Service]的资源)都隔离到特定虚拟沙箱。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* 内容类型： `application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个帐户只需要一 [!DNL Cassandra] 个连接器，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建连接， [!DNL Cassandra] 其唯一连接规范ID必须作为POST请求的一部分提供。 连接规范ID [!DNL Cassandra] 为 `a8f4d393-1a6b-43f3-931f-91a16ed857f4`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Cassandra test connection",
        "description": "A test connection for Cassandra",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST},
                    "port": "{PORT}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "a8f4d393-1a6b-43f3-931f-91a16ed857f4",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.host` | 服务器的IP地址或主 [!DNL Cassandra] 机名。 |
| `auth.params.port` | 服务器用于侦 [!DNL Cassandra] 听客户端连接的TCP端口。 The default port is `9042`. |
| `auth.params.username` | 用于连接到服务器进行身 [!DNL Cassandra] 份验证的用户名。 |
| `auth.params.password` | 连接到服务器进行身 [!DNL Cassandra] 份验证的口令。 |
| `connectionSpec.id` | 连接 [!DNL Cassandra] 规范ID: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**响应**

成功的响应会返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## 后续步骤

通过本教程，您已使用 [!DNL Cassandra] API创建了 [!DNL Flow Service] 一个连接，并已获得该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您将学习如 [何使用流服务API浏览数据库](../../explore/database-nosql.md)。

---
keywords: Experience Platform；主页；热门主题；Apache Cassandra；Apache cassandra；Cassandra；cassandra
solution: Experience Platform
title: 使用流服务API创建Apache Cassandra Source连接
type: Tutorial
description: 了解如何使用流服务API将Apache Cassandra连接到Adobe Experience Platform。
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 11%

---


# 使用[!DNL Flow Service] API创建[!DNL Apache Cassandra]源连接

[!DNL Flow Service]用于收集和集中Adobe Experience Platform中各种不同来源的客户数据。 该服务提供了一个用户界面和RESTful API，所有受支持的源均可从该API连接。

本教程使用[!DNL Flow Service] API引导您完成将[!DNL Apache Cassandra]（以下称为“Cassandra”）连接到[!DNL Experience Platform]的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到Cassandra所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与[!DNL Cassandra]连接，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | [!DNL Cassandra]服务器的IP地址或主机名。 |
| `port` | [!DNL Cassandra]服务器用于侦听客户端连接的TCP端口。 默认端口为`9042`。 |
| `username` | 用于连接到[!DNL Cassandra]服务器进行身份验证的用户名。 |
| `password` | 用于连接到[!DNL Cassandra]服务器以进行身份验证的密码。 |
| `connectionSpec.id` | 创建连接所需的唯一标识符。 [!DNL Cassandra]的连接规范ID为`a8f4d393-1a6b-43f3-931f-91a16ed857f4`。 |

有关入门的详细信息，请参阅[此Cassandra文档](https://cassandra.apache.org/doc/latest/operating/security.html#authentication)。

### 正在读取示例 API 调用

本教程提供了示例API调用来演示如何格式化请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中有关[如何读取示例API调用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

### 收集所需标头的值

要调用[!DNL Experience Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

* 授权：持有人`{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都被隔离到特定的虚拟沙盒中。 对[!DNL Experience Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* x-sandbox-name： `{SANDBOX_NAME}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要一个额外的媒体类型标头：

* 内容类型： `application/json`

## 创建连接

连接指定源，并包含该源的凭据。 每个[!DNL Cassandra]帐户只需要一个连接器，因为它可用于创建多个源连接器以引入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

为了创建[!DNL Cassandra]连接，必须在POST请求中提供其唯一连接规范ID。 [!DNL Cassandra]的连接规范ID为`a8f4d393-1a6b-43f3-931f-91a16ed857f4`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.host` | [!DNL Cassandra]服务器的IP地址或主机名。 |
| `auth.params.port` | [!DNL Cassandra]服务器用于侦听客户端连接的TCP端口。 默认端口为`9042`。 |
| `auth.params.username` | 用于连接到[!DNL Cassandra]服务器进行身份验证的用户名。 |
| `auth.params.password` | 用于连接到[!DNL Cassandra]服务器以进行身份验证的密码。 |
| `connectionSpec.id` | [!DNL Cassandra]连接规范ID： `a8f4d393-1a6b-43f3-931f-91a16ed857f4`。 |

**响应**

成功的响应返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## 后续步骤

通过学习本教程，您已使用[!DNL Flow Service] API创建了[!DNL Cassandra]连接并获取该连接的唯一ID值。 在学习如何使用流服务API[浏览数据库时，您可以在下一个教程中使用此ID](../../explore/database-nosql.md)。

---
keywords: Experience Platform；主页；热门主题；Apache Cassandra；Apache cassandra；Cassandra；cassandra
solution: Experience Platform
title: 使用流服务API创建Apache Cassandra源连接
type: Tutorial
description: 了解如何使用流服务API将Apache Cassandra连接到Adobe Experience Platform。
source-git-commit: 997423f7bf92469e29c567bd77ffde357413bf9e
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 2%

---


# 创建 [!DNL Apache Cassandra] 源连接使用 [!DNL Flow Service] API

[!DNL Flow Service] 用于从Adobe Experience Platform中各种不同的来源收集客户数据并对其进行集中。 该服务提供了一个用户界面和RESTful API，所有受支持的源均可从此API进行连接。

本教程使用 [!DNL Flow Service] API引导您完成连接的步骤 [!DNL Apache Cassandra] （以下称“Cassandra”） [!DNL Experience Platform].

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下方式构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供您需要了解的其他信息，以便使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接 [!DNL Cassandra]中，必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 的IP地址或主机名 [!DNL Cassandra] 服务器。 |
| `port` | TCP端口， [!DNL Cassandra] 服务器使用来侦听客户端连接。 默认端口为 `9042`. |
| `username` | 用于连接到 [!DNL Cassandra] 服务器进行身份验证。 |
| `password` | 用于连接到 [!DNL Cassandra] 服务器进行身份验证。 |
| `connectionSpec.id` | 创建连接所需的唯一标识符。 的连接规范ID [!DNL Cassandra] 是 `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

有关入门的更多信息，请参阅 [此Cassandra文档](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### 正在读取示例API调用

本教程提供了示例API调用来演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

* 授权：持有者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform]，包括那些属于 [!DNL Flow Service]，与特定的虚拟沙盒隔离。 的所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的媒体类型标头：

* Content-Type: `application/json`

## 创建连接

连接指定源，并包含该源的凭据。 每个只需要一个连接器 [!DNL Cassandra] 帐户，因为它可用于创建多个源连接器以引入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

为了创建 [!DNL Cassandra] 连接，其唯一连接规范ID必须作为POST请求的一部分提供。 的连接规范ID [!DNL Cassandra] 是 `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

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
| `auth.params.host` | 的IP地址或主机名 [!DNL Cassandra] 服务器。 |
| `auth.params.port` | TCP端口， [!DNL Cassandra] 服务器使用来侦听客户端连接。 默认端口为 `9042`. |
| `auth.params.username` | 用于连接到 [!DNL Cassandra] 服务器进行身份验证。 |
| `auth.params.password` | 用于连接到 [!DNL Cassandra] 服务器进行身份验证。 |
| `connectionSpec.id` | 此 [!DNL Cassandra] 连接规范ID： `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**响应**

成功响应将返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中，需要此ID来浏览您的数据。

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## 后续步骤

按照本教程，您已创建了一个 [!DNL Cassandra] 连接使用 [!DNL Flow Service] API并已获得连接的唯一ID值。 在学习如何执行以下操作，您可在下一个教程中使用此ID [使用流服务API浏览数据库](../../explore/database-nosql.md).

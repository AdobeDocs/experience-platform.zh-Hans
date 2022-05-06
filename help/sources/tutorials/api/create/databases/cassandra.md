---
keywords: Experience Platform；主页；热门主题；Apache Cassandra;Apache cassandra;Cassandra;cassandra
solution: Experience Platform
title: 使用流服务API创建Apache Cassandra源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Apache Cassandra连接到Adobe Experience Platform。
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 2%

---


# 创建 [!DNL Apache Cassandra] 源连接使用 [!DNL Flow Service] API

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供了用户界面和RESTful API，所有受支持的源都可从中连接。

本教程使用 [!DNL Flow Service] 用于指导您完成连接步骤的API [!DNL Apache Cassandra] （以下简称“Cassandra”） [!DNL Experience Platform].

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL Cassandra]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 的IP地址或主机名 [!DNL Cassandra] 服务器。 |
| `port` | TCP端口 [!DNL Cassandra] 服务器使用侦听客户端连接。 默认端口为 `9042`. |
| `username` | 用于连接到的用户名 [!DNL Cassandra] 服务器进行身份验证。 |
| `password` | 连接到的密码 [!DNL Cassandra] 服务器进行身份验证。 |
| `connectionSpec.id` | 创建连接所需的唯一标识符。 的连接规范ID [!DNL Cassandra] is `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

有关入门的更多信息，请参阅 [这个卡桑德拉文件](https://cassandra.apache.org/doc/latest/operating/security.html#authentication).

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

* 授权：持有者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform]，包括属于 [!DNL Flow Service]，与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* Content-Type: `application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个 [!DNL Cassandra] 帐户，因为它可用于创建多个源连接器以引入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建 [!DNL Cassandra] 连接时，其唯一连接规范ID必须作为POST请求的一部分提供。 的连接规范ID [!DNL Cassandra] is `a8f4d393-1a6b-43f3-931f-91a16ed857f4`.

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
| `auth.params.port` | TCP端口 [!DNL Cassandra] 服务器使用侦听客户端连接。 默认端口为 `9042`. |
| `auth.params.username` | 用于连接到的用户名 [!DNL Cassandra] 服务器进行身份验证。 |
| `auth.params.password` | 连接到的密码 [!DNL Cassandra] 服务器进行身份验证。 |
| `connectionSpec.id` | 的 [!DNL Cassandra] 连接规范ID: `a8f4d393-1a6b-43f3-931f-91a16ed857f4`. |

**响应**

成功的响应会返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "ce69aa89-1baa-4054-a9aa-891baa605425",
    "etag": "\"5a026e19-0000-0200-0000-5eac76d00000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Cassandra] 使用 [!DNL Flow Service] API，并已获取连接的唯一ID值。 在下一个教程中，您可以使用此ID来了解如何 [使用流服务API浏览数据库](../../explore/database-nosql.md).

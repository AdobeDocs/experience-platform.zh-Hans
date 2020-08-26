---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API创建Phoenix连接器
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 1%

---


# 使用 [!DNL Phoenix] API创建连 [!DNL Flow Service] 接器

>[!NOTE]
>
>连接 [!DNL Phoenix] 器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使 [!DNL Flow Service] 用API指导您完成将数据库连接到 [!DNL Phoenix] 的步骤 [!DNL Experience Platform]。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了成功连接到使用API所需了解的其 [!DNL Phoenix] 他信 [!DNL Flow Service] 息。

### 收集所需的凭据

要连接 [!DNL Flow Service] ，必须 [!DNL Phoenix]为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 服务器的IP地址或主 [!DNL Phoenix] 机名。 |
| `username` | 用于访问服务器的用户 [!DNL Phoenix] 名。 |
| `password` | 与用户对应的口令。 |
| `port` | 服务器用于侦 [!DNL Phoenix] 听客户端连接的TCP端口。 如果连接到 [!DNL Azure] HDInsights，请指定端口为443。 |
| `httpPath` | 与服务器对应的部分 [!DNL Phoenix] URL。 如果使用HDInsights群集，请指 [!DNL Azure] 定/hbasephoenix0。 |
| `enableSsl` | 布尔值。 指定是否使用SSL加密与服务器的连接。 |
| `connectionSpec.id` | 创建连接所需的唯一标识符。 连接规范ID [!DNL Phoenix] 为： `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

有关入门的详细信息，请参 [阅此凤凰文档](https://python-phoenixdb.readthedocs.io/en/latest/api.html)。

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

连接指定源并包含该源的凭据。 每个帐户只需要一 [!DNL Phoenix] 个连接，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建连接， [!DNL Phoenix] 其唯一连接规范ID必须作为POST请求的一部分提供。 连接规范ID [!DNL Phoenix] 为 `102706fb-a5cd-42ee-afe0-bc42f017ff43`。

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
| `auth.params.host` | The host of the [!DNL Phoenix] server. |
| `auth.params.username` | 与您的连接关联的用 [!DNL Phoenix] 户名。 |
| `auth.params.password` | 与您的连接关联的 [!DNL Phoenix] 密码。 |
| `auth.params.port` | 连接的TCP端 [!DNL Phoenix] 口。 |
| `auth.params.httpPath` | 连接的部分http [!DNL Phoenix] 路径。 |
| `auth.params.enableSsl` | 布尔值，指定是否使用SSL加密与服务器的连接。 |
| `connectionSpec.id` | 连接 [!DNL Phoenix] 规范ID: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**响应**

成功的响应会返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 后续步骤

通过本教程，您已使用 [!DNL Phoenix] API创建了 [!DNL Flow Service] 一个连接，并已获得该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您将学习如 [何使用流服务API浏览数据库](../../explore/database-nosql.md)。
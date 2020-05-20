---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API创建HP Vertica连接器
topic: overview
translation-type: tm+mt
source-git-commit: a015d2612bc5a72004e15dc5706c7718617a0af4
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 1%

---


# 使用Flow Service API创建HP Vertica连接器

>[!NOTE]
>HP Vertica连接器处于测试阶段。 功能和文档可能会发生更改。

Flow Service用于在Adobe Experience Platform内收集和集中来自不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用Flow Service API指导您完成将HP Vertica连接到Experience Platform的步骤。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

- [来源](https://docs.adobe.com/content/help/en/experience-platform/source-connectors/home.html): Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务构建、映射和增强传入数据。
- [沙箱](https://docs.adobe.com/content/help/en/experience-platform/sandbox/home.html): Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和改进数字体验应用程序。

以下各节提供了使用Flow Service API成功连接到HP Vertica所需的其他信息。

### 收集所需的凭据

要使Flow Service与HP Vertica连接，您必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 用于连接到HP Vertica实例的连接字符串。 HP Vertica的连接字符串模式是 `Server=<server>;Port=<port>;Database=<database>;UID=<user name>;PWD=<password>` |
| `connectionSpec.id` | 创建连接所需的标识符。 HP Vertica的固定连接规范ID为： `a8b6a1a4-5735-42b4-952c-85dce0ac38b5` |

有关获取连接字符串的详细信息，请参 [阅此HP Vertica文档](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](https://docs.adobe.com/content/help/en/experience-platform/landing/troubleshooting.html#reading-example-api-calls) 用的部分。

### 收集所需标题的值

要调用平台API，您必须先完成身份验证 [教程](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html)。 完成身份验证教程后，将提供所有Experience Platform API调用中每个所需标头的值，如下所示：

- 授权： 承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源（包括源连接器）都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

- 内容类型： `application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个HP Vertica帐户只需要一个连接，因为它可用于创建多个源连接器以引入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建HP Vertica连接，其唯一连接规范ID必须作为POST请求的一部分提供。 HP Vertica的连接规范ID为 `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for HP Vertica",
        "description": "Connection for HP Vertica",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server=<server>;Port=<port>;Database=<database>;UID=<user name>;PWD=<password>"
            }
        },
        "connectionSpec": {
            "id": "a8b6a1a4-5735-42b4-952c-85dce0ac38b5",
            "version": "1.0"
        }
    }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.connectionString` | 与您的HP Vertica帐户关联的连接字符串。 |
| `connectionSpec.id` | HP Vertica连接规范ID: `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`. |

**响应**

成功的响应会返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

## 后续步骤

通过本教程，您已使用Flow Service API创建了HP Vertica连接，并已获得该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您将学习如 [何使用流服务API浏览数据库](../../explore/database-nosql.md)。

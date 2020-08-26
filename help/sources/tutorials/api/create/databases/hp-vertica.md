---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API创建HP Vertica连接器
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 3%

---


# 使用API创 [!DNL Vertica] 建HP连接 [!DNL Flow Service] 器

>[!NOTE]
>
>HP接 [!DNL Vertica] 口为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使 [!DNL Flow Service] 用API指导您完成将HP连接到的 [!DNL Vertica] 步骤 [!DNL Experience Platform]。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

- [来源](https://docs.adobe.com/content/help/en/experience-platform/source-connectors/home.html): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务构建、映射和增强传入数 [!DNL Platform] 据。
- [沙箱](https://docs.adobe.com/content/help/zh-Hans/experience-platform/sandbox/home.html): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用API成 [!DNL Vertica] 功连接到 [!DNL Flow Service] HP。

### 收集所需的凭据

要与HP [!DNL Flow Service] 连接，您 [!DNL Vertica]必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 用于连接到HP实例的连接 [!DNL Vertica] 字符串。 HP的连接字符串模式 [!DNL Vertica] 是 `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |
| `connectionSpec.id` | 创建连接所需的标识符。 HP的固定连接规范ID [!DNL Vertica] 为： `a8b6a1a4-5735-42b4-952c-85dce0ac38b5` |

有关获取连接字符串的详细信息，请参 [阅此HP Vertica文档](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](https://docs.adobe.com/content/help/en/experience-platform/landing/troubleshooting.html#reading-example-api-calls) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

- 授权：承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有资 [!DNL Experience Platform]源（包括源连接器）都隔离到特定虚拟沙箱。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

- 内容类型： `application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个HP帐户只需要一 [!DNL Vertica] 个连接，因为它可用于创建多个源连接器以引入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

要创建HP连接， [!DNL Vertica] 其唯一连接规范ID必须作为POST请求的一部分提供。 HP的连接规范ID [!DNL Vertica] 为 `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`。

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
                "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
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
| `auth.params.connectionString` | 与您的HP帐户关联的连接 [!DNL Vertica] 字符串。 HP的连接字符串模式 [!DNL Vertica] 是： `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | HP连接 [!DNL Vertica] 规范ID: `a8b6a1a4-5735-42b4-952c-85dce0ac38b5`. |

**响应**

成功的响应会返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

## 后续步骤

通过本教程，您已使用API [!DNL Vertica] 创建了一 [!DNL Flow Service] 个HP连接，并已获得该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您将学习如 [何使用流服务API浏览数据库](../../explore/database-nosql.md)。

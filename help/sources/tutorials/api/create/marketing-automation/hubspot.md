---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API创建HubSpot连接器
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 1%

---


# 使用 [!DNL HubSpot] API创建连 [!DNL Flow Service] 接器

>[!NOTE]
>
>连接 [!DNL HubSpot] 器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使 [!DNL Flow Service] 用API指导您完成连接到的 [!DNL Experience Platform] 步骤 [!DNL HubSpot]。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了成功连接到使用API所需了解的其 [!DNL HubSpot] 他信 [!DNL Flow Service] 息。

### 收集所需的凭据

要连接 [!DNL Flow Service] ，必须 [!DNL HubSpot]提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| 客户端ID | 与您的应用程序关联的客户 [!DNL HubSpot] 端ID。 |
| 客户端机密 | 与您的应用程序关联的客户端 [!DNL HubSpot] 机密。 |
| 访问令牌 | 最初验证您的OAuth集成时获得的访问令牌。 |
| 刷新令牌 | 最初验证您的OAuth集成时获取的刷新令牌。 |
| 连接规范ID | 创建连接所需的唯一标识符。 连接规范ID [!DNL HubSpot] 为： `cc6a4487-9e91-433e-a3a3-9cf6626c1806` |

有关快速入门的详细信息，请参阅此 [HubSpot文档](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

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

连接指定源并包含该源的凭据。 每个帐户只需要一 [!DNL HubSpot] 个连接，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```https
POST /connections
```

**请求**

要创建连接， [!DNL HubSpot] 其唯一连接规范ID必须作为POST请求的一部分提供。 连接规范ID [!DNL HubSpot] 为 `cc6a4487-9e91-433e-a3a3-9cf6626c1806`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for hubspot",
        "description": "connection for hubspot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.clientId` | 与您的应用程序关联的客户 [!DNL HubSpot] 端ID。 |
| `auth.params.clientSecret` | 与您的应用程序关联的客户端 [!DNL HubSpot] 机密。 |
| `auth.params.accessToken` | 最初验证您的OAuth集成时获得的访问令牌。 |
| `auth.params.refreshToken` | 最初验证您的OAuth集成时获取的刷新令牌。 |

**响应**

成功的响应会返回新创建的API连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

通过本教程，您已使用 [!DNL HubSpot] API创建了 [!DNL Flow Service] 一个连接，并已获得该连接的唯一ID值。 在下一个教程中，您可以使用此连接ID，因为您将学习如 [何使用Flow Service API探索营销自动化系统](../../explore/marketing-automation.md)。
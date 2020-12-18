---
keywords: Experience Platform;home;popular topics;hubspot;Hubspot
solution: Experience Platform
title: 使用Flow Service API创建HubSpot连接器
topic: overview
type: Tutorial
description: 本教程使用Flow Service API指导您完成将Experience Platform连接到HubSpot的步骤。
translation-type: tm+mt
source-git-commit: 9092c3d672967d3f6f7bf7116c40466a42e6e7b1
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 1%

---


# 使用[!DNL Flow Service] API创建[!DNL HubSpot]连接器

>[!NOTE]
>
>[!DNL HubSpot]接头为测试版。 有关使用测试版标签的连接器的详细信息，请参见[源概述](../../../../home.md#terms-and-conditions)。

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用[!DNL Flow Service] API指导您完成将[!DNL Experience Platform]连接到[!DNL HubSpot]的步骤。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入 [!DNL Platform] 数据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了使用[!DNL Flow Service] API成功连接到[!DNL HubSpot]时需要了解的其他信息。

### 收集所需的凭据

要使[!DNL Flow Service]与[!DNL HubSpot]连接，必须提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| `clientId` | 与[!DNL HubSpot]应用程序关联的客户端ID。 |
| `clientSecret` | 与[!DNL HubSpot]应用程序关联的客户端机密。 |
| `accessToken` | 最初验证您的OAuth集成时获得的访问令牌。 |
| `refreshToken` | 最初验证您的OAuth集成时获取的刷新令牌。 |
| `connectionSpec` | 创建连接所需的唯一标识符。 [!DNL HubSpot]的连接规范ID为：`cc6a4487-9e91-433e-a3a3-9cf6626c1806` |

有关快速入门的详细信息，请参阅此[HubSpot文档](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中的[如何阅读示例API调用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](../../../../../tutorials/authentication.md)。 完成身份验证教程后，将为所有[!DNL Experience Platform] API调用中每个所需标头提供值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都隔离到特定虚拟沙箱。 对[!DNL Platform] API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个[!DNL HubSpot]帐户只需要一个连接，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```https
POST /connections
```

**请求**

要创建[!DNL HubSpot]连接，其唯一连接规范ID必须作为POST请求的一部分提供。 [!DNL HubSpot]的连接规范ID为`cc6a4487-9e91-433e-a3a3-9cf6626c1806`。

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
| `auth.params.clientId` | 与[!DNL HubSpot]应用程序关联的客户端ID。 |
| `auth.params.clientSecret` | 与[!DNL HubSpot]应用程序关联的客户端机密。 |
| `auth.params.accessToken` | 最初验证您的OAuth集成时获得的访问令牌。 |
| `auth.params.refreshToken` | 最初验证您的OAuth集成时获取的刷新令牌。 |

**响应**

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

通过本教程，您已使用[!DNL Flow Service] API创建了[!DNL HubSpot]连接，并获得了该连接的唯一ID值。 在下一个教程中，您可以使用此连接ID，因为您正在学习如何[使用流服务API](../../explore/marketing-automation.md)探索营销自动化系统。
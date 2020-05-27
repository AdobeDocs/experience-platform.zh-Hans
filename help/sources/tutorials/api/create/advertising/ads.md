---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API创建Google AdWords连接器
topic: overview
translation-type: tm+mt
source-git-commit: 00f785577999d2ec3147a3cc2b8edd1028be2471
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 1%

---


# 使用Flow Service API创建Google AdWords连接器

Flow Service用于在Adobe Experience Platform内收集和集中来自不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用Flow Service API指导您完成将Experience Platform连接到Google AdWords的步骤。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md): Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和改进数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用流服务API成功连接到广告。

### 收集所需的凭据

要使流服务与AdWords连接，您必须为以下连接属性提供值：

| **凭据** | **描述** |
| -------------- | --------------- |
| 客户ID | AdWords帐户的客户客户ID。 |
| 开发人员令牌 | 与管理者帐户关联的开发者令牌。 |
| 刷新令牌 | 从Google获取的用于授权访问AdWords的刷新令牌。 |
| 客户端ID | 用于获取刷新令牌的Google应用程序的客户端ID。 |
| 客户端机密 | 用于获取刷新令牌的google应用程序的客户端机密。 |
| 连接规范ID | 创建连接所需的唯一标识符。 Google AdWords的连接规范ID为： `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

有关这些值的详细信息，请参阅此 [Google AdWords文档](https://developers.google.com/adwords/api/docs/guides/authentication)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的部分。

### 收集所需标题的值

要调用平台API，您必须先完成身份验证 [教程](../../../../../tutorials/authentication.md)。 完成身份验证教程后，将提供所有Experience Platform API调用中每个所需标头的值，如下所示：

* 授权： 承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源（包括属于流服务的资源）都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* 内容类型： `application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个Google AdWords帐户只需要一个连接，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```https
POST /connections
```

**请求**

要创建Google AdWords连接，其唯一连接规范ID必须作为POST请求的一部分提供。 Google AdWords的连接规范ID为 `221c7626-58f6-4eec-8ee2-042b0226f03b`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "google-AdWords connection",
        "description": "Connection for google-AdWords",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
                "developerToken": "{DEVELOPER_TOKEN}",
                "authenticationType": "{AUTHENTICATION_TYPE}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.clientCustomerID` | 您的AdWords帐户的客户客户ID。 |
| `auth.params.developerToken` | 您的AdWords帐户的开发人员令牌。 |
| `auth.params.refreshToken` | 您的AdWords帐户的刷新令牌。 |
| `auth.params.clientID` | 您的AdWords帐户的客户端ID。 |
| `auth.params.clientSecret` | AdWords帐户的客户机密码。 |
| `connectionSpec.id` | Google AdWords连接规范ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**响应**

成功的响应会返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

通过本教程，您已使用Flow Service API创建了Google AdWords连接，并已获得该连接的唯一ID值。 在您学习如何使用Flow Service API浏览广告系 [统时，您可以在下一个教程中使用此ID](../../explore/advertising.md)。

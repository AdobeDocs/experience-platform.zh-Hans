---
keywords: Experience Platform;home;popular topics;google adwords;Google AdWords;adwords
solution: Experience Platform
title: 使用Flow Service API创建Google AdWords连接器
topic: overview
type: Tutorial
description: 本教程使用Flow Service API指导您完成将Experience Platform连接到Google AdWords的步骤。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 1%

---


# 使用 [!DNL Google AdWords] API创建连 [!DNL Flow Service] 接器

>[!NOTE]
>
>连接 [!DNL Google AdWords] 器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使 [!DNL Flow Service] 用API指导您完成连接到的 [!DNL Experience Platform] 步骤 [!DNL Google AdWords]。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用API成功连接到广 [!DNL Flow Service] 告。

### 收集所需的凭据

要连接 [!DNL Flow Service] AdWords，您必须为以下连接属性提供值：

| **凭据** | **描述** |
| -------------- | --------------- |
| 客户ID | AdWords帐户的客户客户ID。 |
| 开发人员令牌 | 与管理者帐户关联的开发人员令牌。 |
| 刷新令牌 | 从授权访问AdWords [!DNL Google] 获得的刷新令牌。 |
| 客户端ID | 用于获取刷新 [!DNL Google] 令牌的应用程序的客户端ID。 |
| 客户端机密 | 用于获取刷新 [!DNL Google] 令牌的应用程序的客户端机密。 |
| 连接规范ID | 创建连接所需的唯一标识符。 连接规范ID [!DNL Google AdWords] 为： `d771e9c1-4f26-40dc-8617-ce58c4b53702` |

有关这些值的详细信息，请参阅此 [Google AdWords文档](https://developers.google.com/adwords/api/docs/guides/authentication)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../../../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

* 授权：承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有资 [!DNL Experience Platform]源(包括属于这些资 [!DNL Flow Service]源)都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* 内容类型： `application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个帐户只需要一 [!DNL Google AdWords] 个连接，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```https
POST /connections
```

**请求**

以下请求创建新的AdWords连接，该连接由有效负荷中提供的属性进行配置：


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
| `auth.params.clientCustomerID` | 您帐户的客户客户 [!DNL AdWords] ID。 |
| `auth.params.developerToken` | 您帐户的开发人员 [!DNL AdWords] 令牌。 |
| `auth.params.refreshToken` | 帐户的刷新 [!DNL AdWords] 令牌。 |
| `auth.params.clientID` | 您帐户的客户端 [!DNL AdWords] ID。 |
| `auth.params.clientSecret` | 帐户的客户机 [!DNL AdWords] 密码。 |
| `connectionSpec.id` | 连接 [!DNL Google AdWords] 规范ID: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**响应**

成功的响应会返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

通过本教程，您已使用 [!DNL Google AdWords] API创建了 [!DNL Flow Service] 一个连接，并已获得该连接的唯一ID值。 在您学习如何使用Flow Service API浏览广告系 [统时，您可以在下一个教程中使用此ID](../../explore/advertising.md)。

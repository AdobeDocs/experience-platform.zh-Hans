---
keywords: Experience Platform;home;popular topics;google adwords;Google AdWords;adwords
solution: Experience Platform
title: 使用Flow Service API创建Google AdWords连接器
topic: overview
type: Tutorial
description: 本教程使用Flow Service API指导您完成将Experience Platform连接到Google AdWords的步骤。
translation-type: tm+mt
source-git-commit: 9092c3d672967d3f6f7bf7116c40466a42e6e7b1
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 1%

---


# 使用[!DNL Flow Service] API创建[!DNL Google AdWords]连接器

>[!NOTE]
>
>[!DNL Google AdWords]接头为测试版。 有关使用测试版标签的连接器的详细信息，请参见[源概述](../../../../home.md#terms-and-conditions)。

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用[!DNL Flow Service] API指导您完成将[!DNL Experience Platform]连接到[!DNL Google AdWords]的步骤。

## 入门指南

本指南要求对Adobe Experience Platform的下列部分有工作上的理解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入 [!DNL Platform] 数据。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分为单独的虚 [!DNL Platform] 拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

以下各节提供了使用[!DNL Flow Service] API成功连接到广告时需要了解的其他信息。

### 收集所需的凭据

要使[!DNL Flow Service]与AdWords连接，必须为以下连接属性提供值：

| **凭据** | **描述** |
| -------------- | --------------- |
| 客户ID | AdWords帐户的客户客户ID。 |
| 开发人员令牌 | 与管理者帐户关联的开发人员令牌。 |
| 刷新令牌 | 从[!DNL Google]获取的用于授权访问AdWords的刷新令牌。 |
| 客户端ID | 用于获取刷新令牌的[!DNL Google]应用程序的客户端ID。 |
| 客户端机密 | 用于获取刷新令牌的[!DNL Google]应用程序的客户端机密。 |
| 连接规范ID | 创建连接所需的唯一标识符。 [!DNL Google AdWords]的连接规范ID为：`d771e9c1-4f26-40dc-8617-ce58c4b53702` |

有关这些值的详细信息，请参阅此[Google AdWords文档](https://developers.google.com/adwords/api/docs/guides/authentication)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参见](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)疑难解答指南中关于如何阅读示例API调用[的一节。[!DNL Experience Platform]

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

连接指定源并包含该源的凭据。 每个[!DNL Google AdWords]帐户只需要一个连接，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```https
POST /connections
```

**请求**

要创建[!DNL Google AdWords]连接，其唯一连接规范ID必须作为POST请求的一部分提供。 [!DNL Google AdWords]的连接规范ID为`d771e9c1-4f26-40dc-8617-ce58c4b53702`。

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
| `auth.params.clientCustomerID` | 您[!DNL AdWords]帐户的客户端客户ID。 |
| `auth.params.developerToken` | 您的[!DNL AdWords]帐户的开发人员令牌。 |
| `auth.params.refreshToken` | [!DNL AdWords]帐户的刷新令牌。 |
| `auth.params.clientID` | [!DNL AdWords]帐户的客户端ID。 |
| `auth.params.clientSecret` | [!DNL AdWords]帐户的客户端机密。 |
| `connectionSpec.id` | [!DNL Google AdWords]连接规范ID:`d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

**响应**

成功的响应会返回新创建的连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览数据时需要此ID。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

按照本教程，您已使用[!DNL Flow Service] API创建了[!DNL Google AdWords]连接，并已获得该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您正在学习如何[使用流服务API](../../explore/advertising.md)浏览广告系统。

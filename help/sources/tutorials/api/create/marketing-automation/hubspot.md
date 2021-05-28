---
keywords: Experience Platform；主页；热门主题；Hubspot;Hubspot
solution: Experience Platform
title: 使用流服务API创建HubSpot源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到HubSpot。
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建[!DNL HubSpot]源连接

[!DNL Flow Service] 用于收集和集中Adobe Experience Platform内不同来源的客户数据。该服务提供了用户界面和RESTful API，所有受支持的源都可从中连接。

本教程使用[!DNL Flow Service] API指导您完成将[!DNL Experience Platform]连接到[!DNL HubSpot]的步骤。

## 入门指南

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到[!DNL HubSpot]。

### 收集所需的凭据

要使[!DNL Flow Service]与[!DNL HubSpot]连接，必须提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| `clientId` | 与[!DNL HubSpot]应用程序关联的客户端ID。 |
| `clientSecret` | 与[!DNL HubSpot]应用程序关联的客户端密钥。 |
| `accessToken` | 首次验证OAuth集成时获取的访问令牌。 |
| `refreshToken` | 首次验证OAuth集成时获取的刷新令牌。 |
| `connectionSpec` | 创建连接所需的唯一标识符。 [!DNL HubSpot]的连接规范ID是：`cc6a4487-9e91-433e-a3a3-9cf6626c1806` |

有关入门的更多信息，请参阅此[HubSpot文档](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅Experience Platform疑难解答指南中[如何阅读示例API调用](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一节。

### 收集所需标题的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程可为所有[!DNL Experience Platform] API调用中每个所需标头的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有资源（包括属于[!DNL Flow Service]的资源）都与特定虚拟沙箱隔离。 对[!DNL Platform] API的所有请求都需要一个标头来指定操作将在其中进行的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 创建连接

连接指定源并包含该源的凭据。 每个[!DNL HubSpot]帐户只需要一个连接，因为它可用于创建多个源连接器以引入不同的数据。

**API格式**

```https
POST /connections
```

**请求**

要创建[!DNL HubSpot]连接，必须在POST请求中提供其唯一连接规范ID。 [!DNL HubSpot]的连接规范ID为`cc6a4487-9e91-433e-a3a3-9cf6626c1806`。

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
| `auth.params.clientSecret` | 与[!DNL HubSpot]应用程序关联的客户端密钥。 |
| `auth.params.accessToken` | 首次验证OAuth集成时获取的访问令牌。 |
| `auth.params.refreshToken` | 首次验证OAuth集成时获取的刷新令牌。 |

**响应**

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL HubSpot]连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此连接ID，因为您正在学习如何[使用流量服务API](../../explore/marketing-automation.md)探索营销自动化系统。

---
keywords: Experience Platform；主页；热门主题；Hubspot；Hubspot
solution: Experience Platform
title: 使用流服务API创建HubSpot基本连接
type: Tutorial
description: 了解如何使用流服务API将Adobe Experience Platform连接到HubSpot。
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API创建[!DNL HubSpot]基本连接

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL HubSpot]创建基本连接的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL HubSpot]所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与[!DNL HubSpot]连接，您必须提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| `clientId` | 与您的[!DNL HubSpot]应用程序关联的客户端ID。 |
| `clientSecret` | 与您的[!DNL HubSpot]应用程序关联的客户端密钥。 |
| `accessToken` | 最初验证您的OAuth集成时获得的访问令牌。 |
| `refreshToken` | 最初对您的OAuth集成进行身份验证时获得的刷新令牌。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL HubSpot]的连接规范ID为： `cc6a4487-9e91-433e-a3a3-9cf6626c1806`。 |

有关入门的详细信息，请参阅此[HubSpot文档](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL HubSpot]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL HubSpot]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for HubSpot",
        "description": "connection for HubSpot",
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
| `auth.params.clientId` | 与您的[!DNL HubSpot]应用程序关联的客户端ID。 |
| `auth.params.clientSecret` | 与您的[!DNL HubSpot]应用程序关联的客户端密钥。 |
| `auth.params.accessToken` | 最初验证您的OAuth集成时获得的访问令牌。 |
| `auth.params.refreshToken` | 最初对您的OAuth集成进行身份验证时获得的刷新令牌。 |
| `connectionSpec.id` | [!DNL HubSpot]连接规范ID： `cc6a4487-9e91-433e-a3a3-9cf6626c1806`。 |

**响应**

成功的响应返回新创建的连接，包括其唯一连接标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL HubSpot]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将营销自动化数据引入Experience Platform](../../collect/marketing-automation.md)

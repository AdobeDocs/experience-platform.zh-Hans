---
keywords: Experience Platform；主页；热门主题；Hubspot;Hubspot
solution: Experience Platform
title: 使用流服务API创建HubSpot基连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到HubSpot。
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: 143f3b4a113c6f36cb1bb0c3624c8503f158a16d
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建[!DNL HubSpot]基本连接

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)为[!DNL HubSpot]创建基本连接的步骤。

## 快速入门

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
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL HubSpot]的连接规范ID是：`cc6a4487-9e91-433e-a3a3-9cf6626c1806`。 |

有关入门的更多信息，请参阅此[HubSpot文档](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL HubSpot]身份验证凭据时，向`/connections`端点发出POST请求。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.clientId` | 与[!DNL HubSpot]应用程序关联的客户端ID。 |
| `auth.params.clientSecret` | 与[!DNL HubSpot]应用程序关联的客户端密钥。 |
| `auth.params.accessToken` | 首次验证OAuth集成时获取的访问令牌。 |
| `auth.params.refreshToken` | 首次验证OAuth集成时获取的刷新令牌。 |
| `connectionSpec.id` | [!DNL HubSpot]连接规范ID:`cc6a4487-9e91-433e-a3a3-9cf6626c1806`。 |

**响应**

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL HubSpot]连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此连接ID，因为您正在学习如何[使用流量服务API](../../explore/marketing-automation.md)探索营销自动化系统。

---
keywords: Experience Platform；主页；热门主题；Hubspot;Hubspot
solution: Experience Platform
title: 使用流服务API创建HubSpot基连接
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到HubSpot。
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# 创建 [!DNL HubSpot] 基本连接使用 [!DNL Flow Service] API

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL HubSpot] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到所需了解的其他信息 [!DNL HubSpot] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL HubSpot]，则必须提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| `clientId` | 与 [!DNL HubSpot] 应用程序。 |
| `clientSecret` | 与 [!DNL HubSpot] 应用程序。 |
| `accessToken` | 首次验证OAuth集成时获取的访问令牌。 |
| `refreshToken` | 首次验证OAuth集成时获取的刷新令牌。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL HubSpot] 为： `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

有关入门的更多信息，请参阅此 [HubSpot文档](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL HubSpot] 身份验证凭据作为请求参数的一部分。

**API格式**

```https
POST /connections
```

**请求**

以下请求会为 [!DNL HubSpot]:

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
| `auth.params.clientId` | 与 [!DNL HubSpot] 应用程序。 |
| `auth.params.clientSecret` | 与 [!DNL HubSpot] 应用程序。 |
| `auth.params.accessToken` | 首次验证OAuth集成时获取的访问令牌。 |
| `auth.params.refreshToken` | 首次验证OAuth集成时获取的刷新令牌。 |
| `connectionSpec.id` | 的 [!DNL HubSpot] 连接规范ID: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

**响应**

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL HubSpot] 基本连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/marketing-automation.md)

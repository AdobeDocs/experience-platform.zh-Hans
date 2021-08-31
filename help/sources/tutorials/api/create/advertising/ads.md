---
keywords: Experience Platform；主页；热门主题；Google AdWords;Google AdWords;Adwords
solution: Experience Platform
title: 使用流服务API创建Google AdWords基本连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform连接到Google AdWords。
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建[!DNL Google AdWords]基本连接

>[!NOTE]
>
>[!DNL Google AdWords]连接器处于测试阶段。 有关使用测试版标记的连接器的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用[[!DNL Flow Service]  API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Google AdWords]（以下称“[!DNL AdWords]”）创建基本连接的步骤。

## 入门指南

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到[!DNL AdWords]。

### 收集所需的凭据

要使[!DNL Flow Service]与[!DNL AdWords]连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `clientCustomerId` | [!DNL AdWords]帐户的客户ID。 |
| `developerToken` | 与管理员帐户关联的开发人员令牌。 |
| `refreshToken` | 从[!DNL Google]获取的用于授权访问[!DNL AdWords]的刷新令牌。 |
| `clientId` | 用于获取刷新令牌的[!DNL Google]应用程序的客户端ID。 |
| `clientSecret` | 用于获取刷新令牌的[!DNL Google]应用程序的客户端密钥。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL AdWords]的连接规范ID是：`d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

有关这些值的更多信息，请参阅此[Google AdWords文档](https://developers.google.com/adwords/api/docs/guides/authentication)。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL AdWords]身份验证凭据时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL AdWords]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
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
| `auth.params.clientCustomerID` | [!DNL AdWords]帐户的客户ID。 |
| `auth.params.developerToken` | [!DNL AdWords]帐户的开发人员令牌。 |
| `auth.params.refreshToken` | [!DNL AdWords]帐户的刷新令牌。 |
| `auth.params.clientID` | [!DNL AdWords]帐户的客户端ID。 |
| `auth.params.clientSecret` | [!DNL AdWords]帐户的客户端密钥。 |
| `connectionSpec.id` | [!DNL Google AdWords]连接规范ID:`d771e9c1-4f26-40dc-8617-ce58c4b53702`。 |

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步中需要此ID才能创建源连接。

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL AdWords]基本连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您正在学习如何[使用流量服务API](../../explore/advertising.md)探索广告系统。

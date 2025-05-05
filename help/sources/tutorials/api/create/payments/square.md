---
keywords: Experience Platform；主页；热门主题；方形；方形
title: 使用流服务API创建基于正方形连接
description: 了解如何使用流服务API将Square连接到Adobe Experience Platform。
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API创建[!DNL Square]基本连接

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Square]创建基本连接的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL Square]所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与[!DNL Square]连接，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| --- | --- |
| `host` | [!DNL Square]实例的URL。 |
| `clientId` | 与您的[!DNL Square]帐户关联的客户端ID。 |
| `clientSecret` | 与您的[!DNL Square]帐户关联的客户端密钥。 |
| `accessToken` | 访问令牌用于通过OAuth 2.0身份验证对您的[!DNL Square]帐户进行身份验证。 可从[!DNL Square]获取访问令牌。 |
| `refreshToken` | 刷新令牌用于在当前访问令牌过期后生成新的访问令牌。 可从[!DNL Square]获取刷新令牌。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Square]的连接规范ID为： `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

有关这些凭据以及如何获取这些凭据的更多信息，请参阅OAuth[&#128279;](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens)上的[!DNL Square] 文档。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL Square]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```http
POST /connections
```

**请求**

以下请求为[!DNL Square]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Square Base Connection",
        "description": "Square Base Connection",
        "auth": {
        "specName": "OAuth2 Refresh Code",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            "accessToken": "{ACCESS_TOKEN}"
            "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.host` | [!DNL Square]实例的URL。 |
| `auth.params.clientId` | 与您的[!DNL Square]帐户关联的客户端ID。 |
| `auth.params.clientSecret` | 与您的[!DNL Square]帐户关联的客户端密钥。 |
| `auth.params.accessToken` | 访问令牌用于通过OAuth 2.0身份验证对您的[!DNL Square]帐户进行身份验证。 可从[!DNL Square]获取访问令牌。 |
| `auth.params.refreshToken` | 刷新令牌用于在当前访问令牌过期后生成新的访问令牌。 可从[!DNL Square]获取刷新令牌。 |
| `connectionSpec.id` | [!DNL Square]连接规范ID： `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`。 |

**响应**

成功的响应返回新创建的连接，包括其唯一连接标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## 后续步骤

通过学习本教程，您已使用[!DNL Flow Service] API创建了[!DNL Square]连接并获取该连接的唯一ID值。 在学习如何使用流服务API[浏览支付应用程序时，您可以在下一个教程中使用此ID](../../explore/payments.md)。

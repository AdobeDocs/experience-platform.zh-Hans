---
keywords: Experience Platform；主页；热门主题；方形；方形
title: 使用流服务API创建基本平方连接
description: 了解如何使用流服务API将Square连接到Adobe Experience Platform。
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 1%

---

# 创建 [!DNL Square] 基本连接使用 [!DNL Flow Service] API

基本连接表示源和Adobe Experience Platform之间经过身份验证的连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL Square] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下方式构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接时需要了解的其他信息 [!DNL Square] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接 [!DNL Square]中，必须提供以下连接属性的值：

| 凭据 | 描述 |
| --- | --- |
| `host` | 的URL [!DNL Square] 实例。 |
| `clientId` | 与您的关联的客户端ID [!DNL Square] 帐户。 |
| `clientSecret` | 与您的关联的客户端密钥 [!DNL Square] 帐户。 |
| `accessToken` | 访问令牌用于验证您的 [!DNL Square] 具有OAuth 2.0身份验证的帐户。 访问令牌可从获取 [!DNL Square]. |
| `refreshToken` | 刷新令牌用于在当前访问令牌过期后生成新的访问令牌。 可以从获取刷新令牌 [!DNL Square]. |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的身份验证规范。 的连接规范ID [!DNL Square] 为： `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

有关这些凭据以及如何获取这些凭据的更多信息，请参阅 [[!DNL Square] oauth上的文档](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点同时提供 [!DNL Square] 作为请求参数一部分的身份验证凭据。

**API格式**

```http
POST /connections
```

**请求**

以下请求创建基本连接 [!DNL Square]：

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
| `auth.params.host` | 的URL [!DNL Square] 实例。 |
| `auth.params.clientId` | 与您的关联的客户端ID [!DNL Square] 帐户。 |
| `auth.params.clientSecret` | 与您的关联的客户端密钥 [!DNL Square] 帐户。 |
| `auth.params.accessToken` | 访问令牌用于验证您的 [!DNL Square] 具有OAuth 2.0身份验证的帐户。 访问令牌可从获取 [!DNL Square]. |
| `auth.params.refreshToken` | 刷新令牌用于在当前访问令牌过期后生成新的访问令牌。 可以从获取刷新令牌 [!DNL Square]. |
| `connectionSpec.id` | 此 [!DNL Square] 连接规范ID： `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`. |

**响应**

成功响应将返回新创建的连接，包括其唯一连接标识符(`id`)。 在下一个教程中，需要此ID来浏览您的数据。

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## 后续步骤

按照本教程，您已创建了一个 [!DNL Square] 连接使用 [!DNL Flow Service] API并已获得连接的唯一ID值。 在学习如何执行以下操作，您可在下一个教程中使用此ID [使用流服务API浏览支付应用程序](../../explore/payments.md).

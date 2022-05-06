---
keywords: Experience Platform；主页；热门主题；正方形；正方形
title: 使用流服务API创建正方形基连接
description: 了解如何使用流量服务API将Square连接到Adobe Experience Platform。
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 1%

---

# 创建 [!DNL Square] 基本连接使用 [!DNL Flow Service] API

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Square] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到所需了解的其他信息 [!DNL Square] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL Square]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| --- | --- |
| `host` | 的URL [!DNL Square] 实例。 |
| `clientId` | 与 [!DNL Square] 帐户。 |
| `clientSecret` | 与 [!DNL Square] 帐户。 |
| `accessToken` | 访问令牌用于验证您的 [!DNL Square] 具有OAuth 2.0身份验证的帐户。 访问令牌可从 [!DNL Square]. |
| `refreshToken` | 当您的当前访问令牌过期时，刷新令牌将用于生成新的访问令牌。 可从获取刷新令牌 [!DNL Square]. |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL Square] 为： `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

有关这些凭据以及如何获取这些凭据的更多信息，请参阅 [[!DNL Square] oauth文档](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Square] 身份验证凭据作为请求参数的一部分。

**API格式**

```http
POST /connections
```

**请求**

以下请求会为 [!DNL Square]:

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
| `auth.params.clientId` | 与 [!DNL Square] 帐户。 |
| `auth.params.clientSecret` | 与 [!DNL Square] 帐户。 |
| `auth.params.accessToken` | 访问令牌用于验证您的 [!DNL Square] 具有OAuth 2.0身份验证的帐户。 访问令牌可从 [!DNL Square]. |
| `auth.params.refreshToken` | 当您的当前访问令牌过期时，刷新令牌将用于生成新的访问令牌。 可从获取刷新令牌 [!DNL Square]. |
| `connectionSpec.id` | 的 [!DNL Square] 连接规范ID: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`. |

**响应**

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Square] 使用 [!DNL Flow Service] API，并已获取连接的唯一ID值。 在下一个教程中，您可以使用此ID来了解如何 [使用流量服务API探索支付应用程序](../../explore/payments.md).

---
keywords: Experience Platform；主页；热门主题；PayPal连接器；Paypal；Paypal
solution: Experience Platform
title: 使用流服务API创建PayPal基本连接
type: Tutorial
description: 了解如何使用流服务API将PayPal连接到Adobe Experience Platform。
exl-id: 5e6ca7b4-5e2f-4706-a339-ac159e2e0938
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---

# 创建 [!DNL PayPal] 基本连接使用 [!DNL Flow Service] API

基本连接表示源和Adobe Experience Platform之间经过身份验证的连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL PayPal] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下方式构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接时需要了解的其他信息 [!DNL PayPal] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接 [!DNL PayPal]中，必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 的URL [!DNL PayPal] 实例。 (默认：api.sandbox.paypal.com)。 |
| `clientId` | 与您的关联的客户端ID [!DNL PayPal] 应用程序。 |
| `clientSecret` | 与您的关联的客户端密钥 [!DNL PayPal] 应用程序。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的身份验证规范。 的连接规范ID [!DNL PayPal] 为： `221c7626-58f6-4eec-8ee2-042b0226f03b` |

有关入门指南的更多信息，请参阅 [此PayPal文档](https://developer.paypal.com/docs/api/overview/#get-credentials).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点同时提供 [!DNL PayPal] 作为请求参数一部分的身份验证凭据。

**API格式**

```http
POST /connections
```

**请求**

以下请求创建基本连接 [!DNL PayPal]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Paypal connection",
        "description": "Paypal connection",
        "auth": {
        "specName": "Client-Id-Secret Based Authentication",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            }
        },
        "connectionSpec": {
            "id": "221c7626-58f6-4eec-8ee2-042b0226f03b",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.host` | 的URL [!DNL PayPal] 实例。 |
| `auth.params.clientId` | 与您的关联的客户端ID [!DNL PayPal] 实例。 |
| `auth.params.clientSecret` | 与您的关联的客户端密钥 [!DNL PayPal] 实例。 |
| `connectionSpec.id` | 此 [!DNL PayPal] 连接规范ID： `221c7626-58f6-4eec-8ee2-042b0226f03b`. |

**响应**

成功响应将返回新创建的连接，包括其唯一连接标识符(`id`)。 在下一个教程中，需要此ID来浏览您的数据。

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## 后续步骤

按照本教程，您已创建了一个 [!DNL PayPal] 基本连接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [使用创建数据流以将支付数据带入Platform [!DNL Flow Service] API](../../collect/payments.md)

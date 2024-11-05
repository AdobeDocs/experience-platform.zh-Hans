---
keywords: Experience Platform；主页；热门主题；PayPal连接器；Paypal；Paypal
solution: Experience Platform
title: 使用流服务API创建PayPal基本连接
type: Tutorial
description: 了解如何使用流服务API将PayPal连接到Adobe Experience Platform。
exl-id: 5e6ca7b4-5e2f-4706-a339-ac159e2e0938
source-git-commit: 0e3fee4d78646b1d1d6730495358b3ced4127f4e
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API创建[!DNL PayPal]基本连接

>[!IMPORTANT]
>
>[!DNL PayPal]源将于2025年5月底弃用。 作为替代方法，您可以使用[[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md)源。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL PayPal]创建基本连接的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL PayPal]所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与[!DNL PayPal]连接，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | [!DNL PayPal]实例的URL。 (默认： api.sandbox.paypal.com)。 |
| `clientId` | 与您的[!DNL PayPal]应用程序关联的客户端ID。 |
| `clientSecret` | 与您的[!DNL PayPal]应用程序关联的客户端密钥。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL PayPal]的连接规范ID为： `221c7626-58f6-4eec-8ee2-042b0226f03b` |

有关入门的详细信息，请参阅[此PayPal文档](https://developer.paypal.com/docs/api/overview/#get-credentials)。

### 使用平台API

有关如何成功调用平台API的信息，请参阅[平台API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供[!DNL PayPal]身份验证凭据作为POST参数的一部分时，向`/connections`端点请求请求。

**API格式**

```http
POST /connections
```

**请求**

以下请求为[!DNL PayPal]创建基本连接：

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
| `auth.params.host` | [!DNL PayPal]实例的URL。 |
| `auth.params.clientId` | 与您的[!DNL PayPal]实例关联的客户端ID。 |
| `auth.params.clientSecret` | 与您的[!DNL PayPal]实例关联的客户端密钥。 |
| `connectionSpec.id` | [!DNL PayPal]连接规范ID： `221c7626-58f6-4eec-8ee2-042b0226f03b`。 |

**响应**

成功的响应返回新创建的连接，包括其唯一连接标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL PayPal]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将付款数据带入Platform](../../collect/payments.md)

---
keywords: Experience Platform；主页；热门主题；PayPal连接器；Paypal;Paypal
solution: Experience Platform
title: 使用流服务API创建PayPal基连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将PayPal连接到Adobe Experience Platform。
exl-id: 5e6ca7b4-5e2f-4706-a339-ac159e2e0938
source-git-commit: 6b6bd67e70267e81c144c37549b0dcba20534eb6
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建[!DNL PayPal]基本连接

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)为[!DNL PayPal]创建基本连接的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到[!DNL PayPal]。

### 收集所需的凭据

要使[!DNL Flow Service]与[!DNL PayPal]连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | [!DNL PayPal]实例的URL。 (默认：api.sandbox.paypal.com)。 |
| `clientId` | 与[!DNL PayPal]应用程序关联的客户端ID。 |
| `clientSecret` | 与[!DNL PayPal]应用程序关联的客户端密钥。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL PayPal]的连接规范ID是：`221c7626-58f6-4eec-8ee2-042b0226f03b` |

有关入门的详细信息，请参阅[此PayPal文档](https://developer.paypal.com/docs/api/overview/#get-credentials)。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL PayPal]身份验证凭据时，向`/connections`端点发出POST请求。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.clientId` | 与[!DNL PayPal]实例关联的客户端ID。 |
| `auth.params.clientSecret` | 与[!DNL PayPal]实例关联的客户端密钥。 |
| `connectionSpec.id` | [!DNL PayPal]连接规范ID:`221c7626-58f6-4eec-8ee2-042b0226f03b`。 |

**响应**

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL PayPal]连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您正在学习如何[使用流量服务API](../../explore/payments.md)探索支付应用程序。

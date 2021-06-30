---
keywords: Experience Platform；主页；热门主题；Shopify;Shopify；电子商务
solution: Experience Platform
title: 使用流程服务API创建Shopify连接器基本连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Shopify连接到Adobe Experience Platform。
exl-id: 36086c7f-813e-4fc5-9778-f9d55aba03b2
source-git-commit: e8c6620a6d2447a577bd56192030ff4353c62c62
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API创建[!DNL Shopify]基本连接

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用[[!DNL Flow Service]  API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)为[!DNL Shopify]（以下称“[!DNL Shopify]”）创建基本连接的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Sources]](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到[!DNL Shopify]。

### 收集所需的凭据

要使[!DNL Flow Service]与[!DNL Shopify]连接，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | [!DNL Shopify]服务器的端点。 |
| `accessToken` | [!DNL Shopify]用户帐户的访问令牌。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL Shopify]的连接规范ID是：`4f63aa36-bd48-4e33-bb83-49fbcd11c708`。 |

有关入门的更多信息，请参阅此[Shopify身份验证文档](https://shopify.dev/concepts/about-apis/authentication)。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL Shopify]身份验证凭据时，向`/connections`端点发出POST请求。

**API格式**

```http
POST /connections
```

**请求**

以下请求为[!DNL Shopify]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Shopify source",
        "description": "Shopify source",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "host": "{HOST}",
                "accessToken": "{ACCESS_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
            "version": "1.0"
        }
    }
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.host` | [!DNL Shopify]服务器的端点。 |
| `auth.params.accessToken` | [!DNL Shopify]用户帐户的访问令牌。 |
| `connectionSpec.id` | [!DNL Shopify]连接规范ID:`4f63aa36-bd48-4e33-bb83-49fbcd11c708`。 |

**响应**

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
    "etag": "\"d600d3ae-0000-0200-0000-5fa99a3d0000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL Shopify]连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此ID，因为您正在学习如何使用流服务API](../../explore/ecommerce.md)浏览电子商务连接。[

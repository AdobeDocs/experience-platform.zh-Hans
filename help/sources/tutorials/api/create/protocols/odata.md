---
keywords: Experience Platform；主页；热门主题；通用OData；通用ODATA
solution: Experience Platform
title: 使用流服务API创建通用OData基本连接
type: Tutorial
description: 了解如何使用流服务API将Generic OData连接到Adobe Experience Platform。
exl-id: 45b302cb-1a43-4fab-a8a2-cb4e1ee129f9
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 5%

---

# 使用[!DNL Flow Service] API创建[!DNL Generic OData]基本连接

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Generic OData]创建基本连接的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL Generic OData]所需了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与[!DNL Generic OData]连接，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `url` | [!DNL Generic OData]服务的根URL。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Generic Generic OData]的连接规范ID为： `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`。 |

有关入门的详细信息，请参阅[此 [!DNL Generic OData] 文档](https://www.odata.org/getting-started/basic-tutorial/)。

### 使用平台API

有关如何成功调用平台API的信息，请参阅[平台API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供[!DNL Generic OData]身份验证凭据作为POST参数的一部分时，向`/connections`端点请求请求。

**API格式**

```http
POST /connections
```

**请求**

以下请求为[!DNL Generic OData]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Protocols",
        "description": "A test connection for a Protocols source",
        "auth": {
            "specName": "Anonymous Authentication",
        "params": {
            "url":  "{URL}"
            }
        },
        "connectionSpec": {
            "id": "8e6b41a8-d998-4545-ad7d-c6a9fff406c3",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.url` | [!DNL Generic OData]服务器的主机。 |
| `connectionSpec.id` | [!DNL Generic OData]连接规范ID： `8e6b41a8-d998-4545-ad7d-c6a9fff406c3`。 |

**响应**

成功的响应返回新创建的连接，包括其唯一连接标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
    "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Generic REST OData]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将协议数据引入平台](../../collect/protocols.md)

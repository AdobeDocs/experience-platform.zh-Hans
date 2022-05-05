---
keywords: Experience Platform；主页；热门主题；Shopify;Shopify；电子商务
solution: Experience Platform
title: 使用流程服务API创建Shopify连接器基本连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Shopify连接到Adobe Experience Platform。
exl-id: 36086c7f-813e-4fc5-9778-f9d55aba03b2
source-git-commit: 17055f76800deadacf435970a691cec79c9f1d17
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 2%

---

# 创建 [!DNL Shopify] 基本连接使用 [!DNL Flow Service] API

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Shopify] (以下简称“[!DNL Shopify]“)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Sources]](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接到所需了解的其他信息 [!DNL Shopify] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL Shopify]，则必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 您的 [!DNL Shopify] 服务器。 |
| `accessToken` | 您的 [!DNL Shopify] 用户帐户。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL Shopify] 为： `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. |

有关入门的更多信息，请参阅此 [Shopify身份验证文档](https://shopify.dev/concepts/about-apis/authentication).

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Shopify] 身份验证凭据作为请求参数的一部分。

**API格式**

```http
POST /connections
```

**请求**

以下请求会为 [!DNL Shopify]:

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
| `auth.params.host` | 的端点 [!DNL Shopify] 服务器。 |
| `auth.params.accessToken` | 您的 [!DNL Shopify] 用户帐户。 |
| `connectionSpec.id` | 的 [!DNL Shopify] 连接规范ID: `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. |

**响应**

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
    "etag": "\"d600d3ae-0000-0200-0000-5fa99a3d0000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Shopify] 基本连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/ecommerce.md)

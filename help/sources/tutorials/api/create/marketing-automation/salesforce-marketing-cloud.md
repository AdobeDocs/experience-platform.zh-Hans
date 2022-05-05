---
keywords: Experience Platform；主页；热门主题；Salesforce Marketing Cloud;SalesforceMarketing Cloud
solution: Experience Platform
title: 使用流服务API创建SalesforceMarketing Cloud库连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform与SalesforceMarketing Cloud连接。
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: c0d750ef61ad2e295568cccabca5c52a758997c2
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 1%

---

# 创建 [!DNL Salesforce Marketing Cloud] 基本连接使用 [!DNL Flow Service] API

>[!NOTE]
>
>的 [!DNL Salesforce Marketing Cloud] 来源为测试版。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标记的源的详细信息。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Salesforce Marketing Cloud] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可分隔单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

以下部分提供了成功连接到时需要了解的其他信息 [!DNL Salesforce Marketing Cloud] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL Salesforce Marketing Cloud]，则必须提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 应用程序的主机服务器。 这通常是您的子域。 **注意：** 在输入 `host` 值时，您只需指定子域，而不需要指定整个URL。 例如，如果您的主机URL为 `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`，则只需输入 `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` 作为您的主机值。 |
| `clientId` | 与 [!DNL Salesforce Marketing Cloud] 应用程序。 |
| `clientSecret` | 与 [!DNL Salesforce Marketing Cloud] 应用程序。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL Salesforce Marketing Cloud] 为： `ea1c2a08-b722-11eb-8529-0242ac130003`. |

有关入门的更多信息，请参阅此 [[!DNL Salesforce Marketing Cloud] 文档](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向 `/connections` 提供 [!DNL Salesforce Marketing Cloud] 身份验证凭据作为请求正文的一部分。

**API格式**

```https
POST /connections
```

**请求**

以下请求会为 [!DNL Salesforce Marketing Cloud]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Marketing Cloud base connection",
        "description": "Salesforce Marketing Cloud base connection",
        "auth": {
            "specName": "Client-Id-Secret Based Authentication",
            "params": {
                "host": "{HOST}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}"
            }
        },
        "connectionSpec": {
            "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.clientId` | 与 [!DNL Salesforce Marketing Cloud] 应用程序。 |
| `auth.params.clientSecret` | 与 [!DNL Salesforce Marketing Cloud] 应用程序。 |
| `connectionSpec.id` | 的 [!DNL Salesforce Marketing Cloud] 连接规范ID: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**响应**

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Salesforce Marketing Cloud] 基本连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/marketing-automation.md)

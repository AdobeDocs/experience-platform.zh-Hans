---
keywords: Experience Platform；主页；热门主题；Salesforce Marketing Cloud;SalesforceMarketing Cloud
solution: Experience Platform
title: 使用流服务API创建SalesforceMarketing Cloud库连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服务API将Adobe Experience Platform与SalesforceMarketing Cloud连接。
source-git-commit: 56458ed6e74a76e2787ab3b9f1409b11556bdee2
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建[!DNL Salesforce Marketing Cloud]基本连接

>[!NOTE]
>
>[!DNL Salesforce Marketing Cloud]源位于测试版中。 有关使用测试版标记的源的详细信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)为[!DNL Salesforce Marketing Cloud]创建基本连接的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

以下部分提供了使用[!DNL Flow Service] API成功连接到[!DNL Salesforce Marketing Cloud]时需要了解的其他信息。

### 收集所需的凭据

要使[!DNL Flow Service]与[!DNL Salesforce Marketing Cloud]连接，必须提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 应用程序的主机服务器。 这通常是您的子域。 |
| `clientId` | 与[!DNL Salesforce Marketing Cloud]应用程序关联的客户端ID。 |
| `clientSecret` | 与[!DNL Salesforce Marketing Cloud]应用程序关联的客户端密钥。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL Salesforce Marketing Cloud]的连接规范ID是：`cea1c2a08-b722-11eb-8529-0242ac130003`。 |

有关入门的更多信息，请参阅此[[!DNL Salesforce Marketing Cloud] 文档](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求正文中提供[!DNL Salesforce Marketing Cloud]身份验证凭据时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL Salesforce Marketing Cloud]创建基本连接：

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
            "id": "cea1c2a08-b722-11eb-8529-0242ac130003",
            "version": "1.0"
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.clientId` | 与[!DNL Salesforce Marketing Cloud]应用程序关联的客户端ID。 |
| `auth.params.clientSecret` | 与[!DNL Salesforce Marketing Cloud]应用程序关联的客户端密钥。 |
| `connectionSpec.id` | [!DNL Salesforce Marketing Cloud]连接规范ID:`cea1c2a08-b722-11eb-8529-0242ac130003`。 |

**响应**

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL Salesforce Marketing Cloud]连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此连接ID，因为您正在学习如何[使用流量服务API](../../explore/marketing-automation.md)探索营销自动化系统。

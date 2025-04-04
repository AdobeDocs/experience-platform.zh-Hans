---
title: 使用流服务API创建Salesforce Marketing Cloud基本连接
description: 了解如何使用流量服务API对Salesforce Marketing Cloud帐户进行Experience Platform身份验证。
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API创建[!DNL Salesforce Marketing Cloud]基本连接

>[!WARNING]
>
>[!DNL Salesforce Marketing Cloud]源将于2025年6月底弃用。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>)为[!DNL Salesforce Marketing Cloud]创建基本连接的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

以下部分提供了使用[!DNL Flow Service] API成功连接到[!DNL Salesforce Marketing Cloud]时需要了解的其他信息。

### 收集所需的凭据

为了使[!DNL Flow Service]与[!DNL Salesforce Marketing Cloud]连接，您必须提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 应用程序的主机服务器。 这通常是您的子域。 **注意：**&#x200B;在输入`host`值时，需要指定`{subdomain}.rest.marketingcloudapis.com`。 例如，如果您的主机URL是`https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`，则必须输入`acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/`作为主机值。 |
| `clientId` | 与您的[!DNL Salesforce Marketing Cloud]应用程序关联的客户端ID。 |
| `clientSecret` | 与您的[!DNL Salesforce Marketing Cloud]应用程序关联的客户端密钥。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Salesforce Marketing Cloud]的连接规范ID为： `ea1c2a08-b722-11eb-8529-0242ac130003`。 |

有关入门的详细信息，请参阅此[[!DNL Salesforce Marketing Cloud] 文档](<https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm>)。

## 创建基本连接

>[!IMPORTANT]
>
>[!DNL Salesforce Marketing Cloud]源集成当前不支持自定义对象摄取。

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL Salesforce Marketing Cloud]身份验证凭据作为请求正文的一部分时，向`/connections`端点发出POST请求。

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Marketing Cloud base connection",
      "description": "Salesforce Marketing Cloud base connection",
      "auth": {
          "specName": "Client-Id-Secret Based Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "acme-salesforce-marketing-cloud",
              "clientSecret": "xxxx"
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
| `auth.params.clientId` | 与您的[!DNL Salesforce Marketing Cloud]应用程序关联的客户端ID。 |
| `auth.params.clientSecret` | 与您的[!DNL Salesforce Marketing Cloud]应用程序关联的客户端密钥。 |
| `connectionSpec.id` | [!DNL Salesforce Marketing Cloud]连接规范ID： `ea1c2a08-b722-11eb-8529-0242ac130003`。 |

**响应**

成功的响应返回新创建的连接，包括其唯一连接标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Salesforce Marketing Cloud]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将营销自动化数据引入Experience Platform](../../collect/marketing-automation.md)

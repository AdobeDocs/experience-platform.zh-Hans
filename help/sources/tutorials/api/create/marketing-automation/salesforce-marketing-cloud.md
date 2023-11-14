---
title: 使用流服务API创建SalesforceMarketing Cloud基本连接
description: 了解如何使用流服务API根据Experience Platform验证您的SalesforceMarketing Cloud帐户。
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 997a9dc70145a8cfd5d6da20ba788a4610e5c257
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 4%

---

# 创建 [!DNL Salesforce Marketing Cloud] 基本连接使用 [!DNL Flow Service] API

>[!IMPORTANT]
>
>当前不支持自定义对象摄取 [!DNL Salesforce Marketing Cloud] 源集成。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL Salesforce Marketing Cloud] 使用 [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

以下部分提供了成功连接时需要了解的其他信息 [!DNL Salesforce Marketing Cloud] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接 [!DNL Salesforce Marketing Cloud]中，您必须提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 应用程序的主机服务器。 这通常是您的子域。 **注意：** 输入时 `host` 值，您只需指定子域，而无需指定整个URL。 例如，如果您的主机URL为 `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`，则只需输入 `acme-ab12c3d4e5fg6hijk7lmnop8qrst` 作为主机值。 |
| `clientId` | 与您的关联的客户端ID [!DNL Salesforce Marketing Cloud] 应用程序。 |
| `clientSecret` | 与您的关联的客户端密钥 [!DNL Salesforce Marketing Cloud] 应用程序。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 的连接规范ID [!DNL Salesforce Marketing Cloud] 为： `ea1c2a08-b722-11eb-8529-0242ac130003`. |

有关入门的更多信息，请参阅此 [[!DNL Salesforce Marketing Cloud] 文档](<https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm>).

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点，同时提供 [!DNL Salesforce Marketing Cloud] 作为请求正文一部分的身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求为创建基本连接 [!DNL Salesforce Marketing Cloud]：

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
| `auth.params.clientId` | 与您的关联的客户端ID [!DNL Salesforce Marketing Cloud] 应用程序。 |
| `auth.params.clientSecret` | 与您的关联的客户端密钥 [!DNL Salesforce Marketing Cloud] 应用程序。 |
| `connectionSpec.id` | 此 [!DNL Salesforce Marketing Cloud] 连接规范ID： `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**响应**

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## 后续步骤

在本教程之后，您已创建一个 [!DNL Salesforce Marketing Cloud] 基本连接使用 [!DNL Flow Service] API。 您可以在下列教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [使用创建数据流以将营销自动化数据引入Platform [!DNL Flow Service] API](../../collect/marketing-automation.md)

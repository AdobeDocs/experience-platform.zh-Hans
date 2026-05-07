---
title: 使用流服务API创建Salesforce Service Cloud Source连接
description: 了解如何使用Flow Service API将Adobe Experience Platform连接到Salesforce Service Cloud。
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: b9a9b00114b3c1159a14b7e39484d250fa7563ba
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 5%

---

# 使用[!DNL Flow Service] API创建[!DNL Salesforce Service Cloud]源连接

基本连接表示源和Adobe Experience Platform之间的已验证连接。

阅读本教程以了解如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Salesforce Service Cloud]创建基本连接。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个[!DNL Experience Platform]实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL Salesforce Service Cloud]所需了解的其他信息。

### 收集所需的凭据

有关检索凭据的更多信息，请阅读[身份验证指南](../../../../connectors/customer-success/salesforce-service-cloud.md#credentials)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL Salesforce Service Cloud]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```http
POST /connections
```

**请求**

以下请求使用OAuth 2客户端凭据为[!DNL Salesforce Service Cloud]创建基本连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "description": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "apiVersion": "60.0"
        }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `auth.params.environmentUrl` | [!DNL Salesforce Service Cloud]实例的URL。 |
| `auth.params.clientId` | 与您的[!DNL Salesforce Service Cloud]帐户关联的客户端ID。 |
| `auth.params.clientSecret` | 与您的[!DNL Salesforce Service Cloud]帐户关联的客户端密钥。 |
| `auth.params.apiVersion` | 您正在使用的[!DNL Salesforce Service Cloud]实例的REST API版本。 |
| `connectionSpec.id` | [!DNL Salesforce Service Cloud]连接规范ID： `cb66ab34-8619-49cb-96d1-39b37ede86ea`。 |

**响应**

成功的响应将返回您新创建的基本连接及其唯一ID。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Salesforce Service Cloud]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将客户成功数据引入Experience Platform](../../collect/customer-success.md)

---
title: 使用流服务API创建Salesforce基本连接
description: 了解如何使用Flow Service API将Adobe Experience Platform连接到Salesforce帐户。
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 7d450ba3357389a2934f187e4838e534d698dd4a
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API创建[!DNL Salesforce]基本连接

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Salesforce]创建基本连接的步骤。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了使用[!DNL Flow Service] API成功将[!DNL Platform]连接到[!DNL Salesforce]帐户所需了解的其他信息。

### 收集所需的凭据

[!DNL Salesforce]源支持基本身份验证和OAuth2客户端凭据。

>[!BEGINTABS]

>[!TAB 基本身份验证]

要使用基本身份验证将您的[!DNL Salesforce]帐户连接到[!DNL Flow Service]，请提供以下凭据的值：

| 凭据 | 描述 |
| --- | --- |
| `environmentUrl` | [!DNL Salesforce]源实例的URL。 |
| `username` | [!DNL Salesforce]用户帐户的用户名。 |
| `password` | [!DNL Salesforce]用户帐户的密码。 |
| `securityToken` | [!DNL Salesforce]用户帐户的安全令牌。 |
| `apiVersion` | 可选)您正在使用的[!DNL Salesforce]实例的REST API版本。 API版本的值必须使用小数格式设置。 例如，如果您使用的是API版本`52`，则必须以`52.0`的形式输入值。 如果此字段留空，则Experience Platform将自动使用最新可用版本。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Salesforce]的连接规范ID为： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`。 |

有关入门的详细信息，请访问[此Salesforce文档](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)。

>[!TAB OAuth 2客户端凭据]

要使用OAuth 2客户端凭据将您的[!DNL Salesforce]帐户连接到[!DNL Flow Service]，请提供以下凭据的值：

| 凭据 | 描述 |
| --- | --- |
| `environmentUrl` | [!DNL Salesforce]源实例的URL。 |
| `clientId` | 在OAuth2身份验证中，客户端ID与客户端密钥结合使用。 客户端ID和客户端密钥共同使您的应用程序能够代表您的帐户运行，方法是向[!DNL Salesforce]标识您的应用程序。 |
| `clientSecret` | 客户端密钥与客户端ID结合使用，作为OAuth2身份验证的一部分。 客户端ID和客户端密钥共同使您的应用程序能够代表您的帐户运行，方法是向[!DNL Salesforce]标识您的应用程序。 |
| `apiVersion` | 您正在使用的[!DNL Salesforce]实例的REST API版本。 API版本的值必须使用小数格式设置。 例如，如果您使用的是API版本`52`，则必须以`52.0`的形式输入值。 如果此字段留空，则Experience Platform将自动使用最新可用版本。 此值对于OAuth2客户端凭据身份验证是必需的。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Salesforce]的连接规范ID为： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`。 |

有关为[!DNL Salesforce]使用OAuth的更多信息，请阅读有关OAuth授权流程](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5)的[[!DNL Salesforce] 指南。

>[!ENDTABS]

### 使用平台API

有关如何成功调用平台API的信息，请参阅[平台API快速入门](../../../../../landing/api-guide.md)指南。

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向`/connections`端点发出POST请求，并在请求正文中提供您的[!DNL Salesforce]身份验证凭据。

**API格式**

```http
POST /connections
```

**请求**

>[!BEGINTABS]

>[!TAB 基本身份验证]

以下请求使用基本身份验证为[!DNL Salesforce]创建基本连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `auth.params.environmentUrl` | [!DNL Salesforce]实例的URL。 |
| `auth.params.username` | 与您的[!DNL Salesforce]帐户关联的用户名。 |
| `auth.params.password` | 与您的[!DNL Salesforce]帐户关联的密码。 |
| `auth.params.securityToken` | 与您的[!DNL Salesforce]帐户关联的安全令牌。 |
| `connectionSpec.id` | [!DNL Salesforce]连接规范ID： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`。 |

>[!TAB OAuth 2客户端凭据]

以下请求使用OAuth 2客户端凭据为[!DNL Salesforce]创建基本连接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account",
      "description": "Salesforce account using OAuth 2",
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
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `auth.params.environmentUrl` | [!DNL Salesforce]实例的URL。 |
| `auth.params.clientId` | 与您的[!DNL Salesforce]帐户关联的客户端ID。 |
| `auth.params.clientSecret` | 与您的[!DNL Salesforce]帐户关联的客户端密钥。 |
| `auth.params.apiVersion` | 您正在使用的[!DNL Salesforce]实例的REST API版本。 |
| `connectionSpec.id` | [!DNL Salesforce]连接规范ID： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`。 |

>[!ENDTABS]

**响应**

成功的响应将返回您新创建的基本连接及其唯一ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Salesforce]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [创建数据流以使用 [!DNL Flow Service] API将CRM数据引入平台](../../collect/crm.md)

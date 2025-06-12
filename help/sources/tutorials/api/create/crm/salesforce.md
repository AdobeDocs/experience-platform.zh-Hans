---
title: 使用流服务API将Salesforce连接到Experience Platform
description: 了解如何使用流服务API将Adobe Experience Platform连接到Salesforce帐户。
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: eab6303a3b420d4622185316922d242a4ce8a12d
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API将[!DNL Salesforce]连接到Experience Platform

阅读本指南，了解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)将您的[!DNL Salesforce]源帐户连接到Adobe Experience Platform。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 将[!DNL Salesforce]连接到[!DNL Azure]上的Experience Platform {#azure}

有关如何将[!DNL Salesforce]源连接到[!DNL Azure]上的Experience Platform的信息，请阅读以下步骤。

### 收集所需的凭据

>[!WARNING]
>
>[!DNL Salesforce]源的基本身份验证将于2026年1月被弃用。 您必须移至OAuth 2客户端凭据身份验证，才能继续使用该源并将数据从[!DNL Salesforce]帐户摄取到Experience Platform。

[!DNL Salesforce]源支持基本身份验证和OAuth2客户端凭据。

>[!BEGINTABS]

>[!TAB 基本身份验证]

要使用基本身份验证将您的[!DNL Salesforce]帐户连接到[!DNL Flow Service]，请提供以下凭据的值：

| 凭据 | 描述 |
| --- | --- |
| `environmentUrl` | [!DNL Salesforce]源实例的URL。 `environmentUrl`的格式为`https://[domain].my.salesforce.com`。 |
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
| `environmentUrl` | [!DNL Salesforce]源实例的URL。 `environmentUrl`的格式为`https://[domain].my.salesforce.com` |
| `clientId` | 在OAuth2身份验证中，客户端ID与客户端密钥结合使用。 客户端ID和客户端密钥共同使您的应用程序能够代表您的帐户运行，方法是向[!DNL Salesforce]标识您的应用程序。 |
| `clientSecret` | 客户端密钥与客户端ID结合使用，作为OAuth2身份验证的一部分。 客户端ID和客户端密钥共同使您的应用程序能够代表您的帐户运行，方法是向[!DNL Salesforce]标识您的应用程序。 |
| `apiVersion` | 您正在使用的[!DNL Salesforce]实例的REST API版本。 API版本的值必须使用小数格式设置。 例如，如果您使用的是API版本`52`，则必须以`52.0`的形式输入值。 如果此字段留空，则Experience Platform将自动使用最新可用版本。 此值对于OAuth2客户端凭据身份验证是必需的。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 [!DNL Salesforce]的连接规范ID为： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`。 |

有关为[!DNL Salesforce]使用OAuth的更多信息，请阅读有关OAuth授权流程](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5)的[[!DNL Salesforce] 指南。

>[!ENDTABS]

### 在[!DNL Azure]的Experience Platform中为[!DNL Salesforce]创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接并将您的[!DNL Salesforce]帐户连接到[!DNL Azure]上的Experience Platform，请对`/connections`端点发出POST请求，并在请求正文中提供您的[!DNL Salesforce]身份验证凭据。

**API格式**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 基本身份验证]

+++请求

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

+++

+++响应

成功的响应将返回您新创建的基本连接及其唯一ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!TAB OAuth 2客户端凭据]

+++请求

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

+++


+++响应

成功的响应将返回您新创建的基本连接及其唯一ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

>[!ENDTABS]

## 将[!DNL Salesforce]连接到Amazon Web Services (AWS)上的Experience Platform {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../../../landing/multi-cloud.md)。

有关如何将[!DNL Salesforce]源连接到AWS上的Experience Platform的信息，请阅读以下步骤。

### 先决条件

有关如何设置您的[!DNL Salesforce]帐户以便能够连接到AWS上的Experience Platform的信息，请阅读[[!DNL Salesforce] 概述](../../../../connectors/crm/salesforce.md#aws)。

### 在AWS上的Experience Platform上为[!DNL Salesforce]创建基本连接

要创建基本连接并将您的[!DNL Salesforce]帐户连接到AWS上的Experience Platform，请对`/connections`端点发出POST请求，并为您的凭据提供相应的值。

**API格式**

```http
POST /connections
```

**请求**

+++选择以查看请求

以下请求在AWS上的Experience Platform中为[!DNL Salesforce]源创建基本连接。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Salesforce account on AWS",
      "description": "ACME Salesforce account on AWS",
      "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params":
            "jwtToken": "{JWT_TOKEN},
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

有关如何检索[!DNL Salesforce] `jwtToken`的信息，请阅读[上的指南，了解如何设置 [!DNL Salesforce] 源以连接到AWS](../../../../connectors/crm/salesforce.md#aws)上的Experience Platform。

+++

**响应**

+++选择以查看响应

成功的响应将返回您新创建的基本连接及其唯一ID。

```json
{
    "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

+++

### 验证连接状态

要验证连接状态，请向`/connections`端点发出GET请求，并提供在创建步骤中生成的基本连接ID。

**API格式**

```http
GET /connections
```

**请求**

+++选择以查看请求

以下请求检索基本连接ID的信息： `3e908d3f-c390-482b-9f44-43d3d4f2eb82`。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/3e908d3f-c390-482b-9f44-43d3d4f2eb82' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
```

+++

**响应**

>[!BEGINTABS]

>[!TAB 正在初始化]

+++选择以查看响应示例

以下响应显示处于`initializing`状态时基本连接ID的信息： `3e908d3f-c390-482b-9f44-43d3d4f2eb82`。

```json
{
  "items": [
    {
      "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
      "createdAt": 1736506325115,
      "updatedAt": 1736506325717,
      "createdBy": "acme@techacct.adobe.com",
      "updatedBy": "acme@techacct.adobe.com",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "JWT Token Auth Authentication E2E-1736506322",
      "description": "Base Connection for salesforce E2E",
      "connectionSpec": {
        "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
        "version": "1.0"
      },
      "state": "initializing",
      "auth": {
        "specName": "OAuth2 JWT Token Credential",
        "params": {
          "jwtToken": "{JWT_TOKEN}",
          "clientId": "{CLIENT_ID}",
          "clientSecret": "{CLIENT_SECRET}",
          "instanceUrl": "https://acme-enterprise-3126.my.salesforce.com"
        }
      }
    }
  }
]
```

+++

>[!TAB 已启用]

+++选择以查看响应示例

以下响应显示处于`enabled`状态时基本连接ID的信息： `3e908d3f-c390-482b-9f44-43d3d4f2eb82`。

```json
{
  "items": [
      {
        "id": "3e908d3f-c390-482b-9f44-43d3d4f2eb82",
        "createdAt": 1736506325115,
        "updatedAt": 1736506413299,
        "createdBy": "acme@techacct.adobe.com",
        "updatedBy": "acme@AdobeID",
        "createdClient": "{CREATED_CLIENT}",
        "updatedClient": "acme",
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "imsOrgId": "{ORG_ID}",
        "name": "JWT Token Auth Authentication E2E-1736506322",
        "description": "Base Connection for salesforce E2E",
        "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
        },
        "state": "enabled",
        "auth": {
          "specName": "OAuth2 JWT Token Credential",
          "params": {
            "jwtToken": "{JWT_TOKEN}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}",
            "instanceUrl": "https://adb8-dev-ed.develop.my.salesforce.com",
            "orgId": "00DdL000001iPRxUAM"
          }
        },
        "version": "\"6d27f305-40be-41c3-97d4-a701827c34df\"",
        "etag": "\"6d27f305-40be-41c3-97d4-a701827c34df\""
    }
  ]
}
```

+++

>[!ENDTABS]

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Salesforce]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [创建数据流以使用 [!DNL Flow Service] API将CRM数据引入Experience Platform](../../collect/crm.md)

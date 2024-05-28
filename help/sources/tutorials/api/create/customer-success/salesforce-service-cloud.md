---
title: 使用流服务API创建Salesforce Service云源连接
description: 了解如何使用流服务API将Adobe Experience Platform连接到Salesforce Service Cloud。
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 3%

---

# 创建 [!DNL Salesforce Service Cloud] 源连接使用 [!DNL Flow Service] API

基本连接表示源和Adobe Experience Platform之间的已验证连接。

阅读本教程，了解如何为创建基本连接 [!DNL Salesforce Service Cloud] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供成功连接时需要了解的其他信息 [!DNL Salesforce Service Cloud] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

此 [!DNL Salesforce Service Cloud] 源支持基本身份验证和OAuth2客户端凭据。

>[!BEGINTABS]

>[!TAB 基本身份验证]

连接您的 [!DNL Salesforce Service Cloud] 帐户至 [!DNL Flow Service] 使用基本身份验证，提供以下凭据的值：

| 凭据 | 描述 |
| --- | --- |
| `environmentUrl` | 的URL [!DNL Salesforce Service Cloud] 源实例。 |
| `username` | 的用户名 [!DNL Salesforce Service Cloud] 用户帐户。 |
| `password` | 的密码 [!DNL Salesforce Service Cloud] 用户帐户。 |
| `securityToken` | 的安全令牌 [!DNL Salesforce Service Cloud] 用户帐户。 |
| `apiVersion` | （可选） REST API版本的 [!DNL Salesforce Service Cloud] 您正在使用的实例。 API版本的值必须使用小数格式设置。 例如，如果您使用的是API版本 `52`，则必须输入值，如下所示 `52.0`. 如果此字段留空，Experience Platform将自动使用最新可用版本。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 的连接规范ID [!DNL Salesforce Service Cloud] 为： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

有关入门的更多信息，请访问 [此Salesforce文档](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

>[!TAB OAuth 2客户端凭据]

连接您的 [!DNL Salesforce Service Cloud] 帐户至 [!DNL Flow Service] 使用OAuth 2客户端凭据，提供以下凭据的值：

| 凭据 | 描述 |
| --- | --- |
| `environmentUrl` | 的URL [!DNL Salesforce Service Cloud] 源实例。 |
| `clientId` | 在OAuth2身份验证中，客户端ID与客户端密钥结合使用。 客户端ID和客户端密钥共同允许您的应用程序代表您的帐户运行，方法是将您的应用程序标识到 [!DNL Salesforce Service Cloud]. |
| `clientSecret` | 客户端密钥与客户端ID结合使用，作为OAuth2身份验证的一部分。 客户端ID和客户端密钥共同允许您的应用程序代表您的帐户运行，方法是将您的应用程序标识到 [!DNL Salesforce Service Cloud]. |
| `apiVersion` | 的REST API版本 [!DNL Salesforce Service Cloud] 您正在使用的实例。 API版本的值必须使用小数格式设置。 例如，如果您使用的是API版本 `52`，则必须输入值，如下所示 `52.0`. 如果此字段留空，Experience Platform将自动使用最新可用版本。 此值对于OAuth2客户端凭据身份验证是必需的。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 的连接规范ID [!DNL Salesforce Service Cloud] 为： `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

有关将OAuth用于 [!DNL Salesforce Service Cloud]，阅读 [[!DNL Salesforce Service Cloud] OAuth授权流指南](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点，同时提供 [!DNL Salesforce Service Cloud] 作为请求参数一部分的身份验证凭据。

**API格式**

```http
POST /connections
```

**请求**

>[!BEGINTABS]

>[!TAB 基本身份验证]

以下请求为创建基本连接 [!DNL Salesforce Service Cloud] 使用基本身份验证：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (basic auth)",
      "description": "Salesforce Service Cloud account for ACME data (basic auth)",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "username": "acme-salesforce-service-cloud",
            "password": "xxxx",
            "securityToken": "xxxx"
        }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| 参数 | 描述 |
| ---| --- |
| `auth.params.environmentUrl` | 的URL [!DNL Salesforce Service Cloud] 实例。 |
| `auth.params.username` | 与您的关联的用户名 [!DNL Salesforce Service Cloud] 帐户。 |
| `auth.params.password` | 与您的关联的密码 [!DNL Salesforce Service Cloud] 帐户。 |
| `auth.params.securityToken` | 与您的关联的安全令牌 [!DNL Salesforce Service Cloud] 帐户。 |
| `connectionSpec.id` | 此 [!DNL Salesforce Service Cloud] 连接规范ID： `cb66ab34-8619-49cb-96d1-39b37ede86ea` |

>[!TAB OAuth2客户端凭据]

以下请求为创建基本连接 [!DNL Salesforce Service Cloud] 使用OAuth 2客户端凭据：

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
| `auth.params.environmentUrl` | 的URL [!DNL Salesforce Service Cloud] 实例。 |
| `auth.params.clientId` | 与您的关联的客户端ID [!DNL Salesforce Service Cloud] 帐户。 |
| `auth.params.clientSecret` | 与您的关联的客户端密钥 [!DNL Salesforce Service Cloud] 帐户。 |
| `auth.params.apiVersion` | 的REST API版本 [!DNL Salesforce Service Cloud] 您正在使用的实例。 |
| `connectionSpec.id` | 此 [!DNL Salesforce Service Cloud] 连接规范ID： `cb66ab34-8619-49cb-96d1-39b37ede86ea`. |

>[!ENDTABS]

**响应**

成功的响应将返回您新创建的基本连接及其唯一ID。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 后续步骤

在本教程之后，您已创建一个 [!DNL Salesforce Service Cloud] 基本连接使用 [!DNL Flow Service] API。 您可以在下列教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [使用创建数据流以将客户成功数据引入Platform [!DNL Flow Service] API](../../collect/customer-success.md)

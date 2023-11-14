---
keywords: Experience Platform；主页；热门主题；通用REST；通用Rest
solution: Experience Platform
title: 使用流服务API创建通用REST API基本连接
type: Tutorial
description: 了解如何使用流服务API将通用REST API连接到Adobe Experience Platform。
exl-id: 6b414868-503e-49d5-8f4a-5b2fc003dab0
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 2%

---

# 使用创建常规REST API基本连接 [!DNL Flow Service] API

>[!NOTE]
>
>此 [!DNL Generic REST API] 源为测试版。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用Beta标记的连接器的更多信息。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL Generic REST API] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接 [!DNL Generic REST API]，您必须提供所选身份验证类型的有效凭据。 [!DNL Generic REST API] 支持OAuth 2刷新代码和基本身份验证。 有关两种受支持的身份验证类型的凭据的信息，请参见下表。

#### OAuth 2刷新代码

| 凭据 | 描述 |
| --- | --- |
| `host` | 您向其发出请求的源的主机URL。 该值为必填，不能使用绕过 `requestParameterOverride`. |
| `authorizationTestUrl` | （可选）创建基本连接时，授权测试URL用于验证凭据。 如果未提供，则会在源连接创建步骤中自动检查凭据。 |
| `clientId` | （可选）与您的用户帐户关联的客户端ID。 |
| `clientSecret` | （可选）与您的用户帐户关联的客户端密钥。 |
| `accessToken` | 用于访问应用程序的主要身份验证凭据。 访问令牌表示应用程序的授权，用于访问用户数据的特定方面。 该值为必填，不能使用绕过 `requestParameterOverride`. |
| `refreshToken` | （可选）当访问令牌过期时，用于生成新访问令牌的令牌。 |
| `expirationDate` | （可选）定义访问令牌的过期日期的隐藏值。 |
| `accessTokenUrl` | （可选）用于获取访问令牌的URL端点。 |
| `requestParameterOverride` | （可选）一个属性，它允许您指定要覆盖的凭据参数。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 的连接规范ID [!DNL Generic REST API] 为： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

#### 基本身份验证

| 凭据 | 描述 |
| --- | --- |
| `host` | 您向其发出请求的源的主机URL。 |
| `username` | 与您的用户帐户对应的用户名。 |
| `password` | 与您的用户帐户对应的密码。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 的连接规范ID [!DNL Generic REST API] 为： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

[!DNL Generic REST API] 支持基本身份验证和OAuth 2刷新代码。 有关如何使用任一身份验证类型进行身份验证的指导，请参阅以下示例。

### 创建 [!DNL Generic REST API] 使用OAuth 2刷新代码的基础连接

POST要使用OAuth 2刷新代码创建基本连接ID，请向 `/connections` 端点，同时提供OAuth 2凭据。

**API格式**

```http
POST /connections
```

**请求**

以下请求为创建基本连接 [!DNL Generic REST API]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Generic REST API base connection with OAuth 2 refresh code",
      "description": "Generic REST API base connection with OAuth 2 refresh code",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "oAuth2RefreshCode",
          "params": {
              "host": "{HOST}",
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `name` | 基础连接的名称。 确保基本连接的名称是描述性的，因为您可以使用此名称查找有关基本连接的信息。 |
| `description` | （可选）可包含的资产，用于提供有关基本连接的更多信息。 |
| `connectionSpec.id` | 与关联的连接规范ID [!DNL Generic REST API]. 此固定ID为： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | 用于向Platform验证源的身份验证类型。 |
| `auth.params.host` | 用于连接到 [!DNL Generic REST API] 源。 |
| `auth.params.accessToken` | 用于对源进行身份验证的相应访问令牌。 基于OAuth的身份验证需要此项。 |

**响应**

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下个教程中，需要此ID才能浏览您的数据。

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### 创建 [!DNL Generic REST API] 使用基本身份验证的基本连接

创建 [!DNL Generic REST API] POST基本连接使用基本身份验证，向 `/connections` 端点 [!DNL Flow Service] API，同时提供基本的身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求为创建基本连接 [!DNL Generic REST API]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
      "name": "Generic REST API base connection with basic authentication",
      "description": "Generic REST API base connection with basic authentication",
      "connectionSpec": {
          "id": "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
          "version": "1.0"
      },
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 基础连接的名称。 确保基本连接的名称是描述性的，因为您可以使用此名称查找有关基本连接的信息。 |
| `description` | （可选）可包含的资产，用于提供有关基本连接的更多信息。 |
| `connectionSpec.id` | 与关联的连接规范ID [!DNL Generic REST API]. 此固定ID为： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | 您用来将源连接到Platform的身份验证类型。 |
| `auth.params.host` | 用于连接到 [!DNL Generic REST API] 源。 |
| `auth.params.username` | 与您的对应的用户名 [!DNL Generic REST API] 源。 这是基本身份验证所必需的。 |
| `auth.params.password` | 与您的对应的密码 [!DNL Generic REST API] 源。 这是基本身份验证所必需的。 |

**响应**

成功的响应会返回新创建的基本连接，包括其唯一连接标识符(`id`)。 在下一步中浏览源的文件结构和内容时，需要此ID。

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## 后续步骤

在本教程之后，您已创建一个 [!DNL Generic REST API] 基本连接使用 [!DNL Flow Service] API。 您可以在下列教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [使用创建数据流以将协议数据引入Platform [!DNL Flow Service] API](../../collect/protocols.md)

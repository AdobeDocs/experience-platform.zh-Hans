---
keywords: Experience Platform；主页；热门主题；一般REST；一般REST
solution: Experience Platform
title: 使用流服务API创建通用REST API基连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流服务API将通用REST API连接到Adobe Experience Platform。
exl-id: 6b414868-503e-49d5-8f4a-5b2fc003dab0
source-git-commit: 1f2ae53e5503618b7ac12628923b30c457fd17e2
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 1%

---

# 使用创建通用REST API基连接 [!DNL Flow Service] API

>[!NOTE]
>
>的 [!DNL Generic REST API] 来源为测试版。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用测试版标签的连接器的更多信息。

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成为 [!DNL Generic REST API] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

### 收集所需的凭据

为 [!DNL Flow Service] 连接 [!DNL Generic REST API]，则必须为您选择的身份验证类型提供有效凭据。 [!DNL Generic REST API] 支持OAuth 2刷新代码和基本身份验证。 有关两种受支持身份验证类型的凭据的信息，请参阅下表。

#### OAuth 2刷新代码

| 凭据 | 描述 |
| --- | --- |
| `host` | 您请求的源的主机URL。 此值是必需的，无法使用 `requestParameterOverride`. |
| `authorizationTestUrl` | （可选）创建基本连接时，授权测试URL用于验证凭据。 如果未提供，则在创建源连接步骤期间会自动检查凭据。 |
| `clientId` | （可选）与您的用户帐户关联的客户端ID。 |
| `clientSecret` | （可选）与您的用户帐户关联的客户端密钥。 |
| `accessToken` | 用于访问应用程序的主身份验证凭据。 访问令牌表示应用程序访问用户数据特定方面的授权。 此值是必需的，无法使用 `requestParameterOverride`. |
| `refreshToken` | （可选）在访问令牌过期时用于生成新访问令牌的令牌。 |
| `expirationDate` | （可选）用于定义访问令牌到期日期的隐藏值。 |
| `accessTokenUrl` | （可选）用于获取访问令牌的URL端点。 |
| `requestParameterOverride` | （可选）用于指定要覆盖的凭据参数的属性。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL Generic REST API] 为： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

#### 基本身份验证

| 凭据 | 描述 |
| --- | --- |
| `host` | 您请求的源的主机URL。 |
| `username` | 与您的用户帐户对应的用户名。 |
| `password` | 与您的用户帐户对应的密码。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 的连接规范ID [!DNL Generic REST API] 为： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

[!DNL Generic REST API] 支持基本身份验证和OAuth 2刷新代码。 有关如何使用这两种身份验证类型进行身份验证的指导，请参阅以下示例。

### 创建 [!DNL Generic REST API] 使用OAuth 2刷新代码的基本连接

要使用OAuth 2刷新代码创建基本连接ID，请向 `/connections` 端点。

**API格式**

```http
POST /connections
```

**请求**

以下请求会为 [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | 基本连接的名称。 确保基本连接的名称具有描述性，因为您可以使用此名称查找有关基本连接的信息。 |
| `description` | （可选）可包含的属性，用于提供有关基本连接的更多信息。 |
| `connectionSpec.id` | 与关联的连接规范ID [!DNL Generic REST API]. 此固定ID是： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | 用于向平台验证源的验证类型。 |
| `auth.params.host` | 用于连接到的根URL [!DNL Generic REST API] 来源。 |
| `auth.params.accessToken` | 用于验证源的相应访问令牌。 基于OAuth的身份验证需要此设置。 |

**响应**

成功的响应会返回新创建的连接，包括其唯一连接标识符(`id`)。 在下一个教程中探索数据时需要此ID。

```json
{
  "id": "a5c6b647-e784-4b58-86b6-47e784ab580b",
  "etag": "\"7b01056a-0000-0200-0000-5e8a4f5b0000\""
}
```

### 创建 [!DNL Generic REST API] 基本连接使用基本身份验证

创建 [!DNL Generic REST API] 基本连接使用基本身份验证，向POST请求 `/connections` 端点 [!DNL Flow Service] API，同时提供基本身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求会为 [!DNL Generic REST API]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | 基本连接的名称。 确保基本连接的名称具有描述性，因为您可以使用此名称查找有关基本连接的信息。 |
| `description` | （可选）可包含的属性，用于提供有关基本连接的更多信息。 |
| `connectionSpec.id` | 与关联的连接规范ID [!DNL Generic REST API]. 此固定ID是： `4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62`. |
| `auth.specName` | 用于将源连接到平台的身份验证类型。 |
| `auth.params.host` | 用于连接到的根URL [!DNL Generic REST API] 来源。 |
| `auth.params.username` | 与您的 [!DNL Generic REST API] 来源。 基本身份验证需要此功能。 |
| `auth.params.password` | 与您的 [!DNL Generic REST API] 来源。 基本身份验证需要此功能。 |

**响应**

成功的响应会返回新创建的基本连接，包括其唯一连接标识符(`id`)。 在下一步中，需要此ID才能浏览源的文件结构和内容。

```json
{
    "id": "9601747c-6874-4c02-bb00-5732a8c43086",
    "etag": "\"3702dabc-0000-0200-0000-615b5b5a0000\""
}
```

## 后续步骤

通过阅读本教程，您已创建 [!DNL Generic REST API] 基本连接使用 [!DNL Flow Service] API。 在以下教程中，您可以使用此基本连接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流，以使用 [!DNL Flow Service] API](../../collect/protocols.md)

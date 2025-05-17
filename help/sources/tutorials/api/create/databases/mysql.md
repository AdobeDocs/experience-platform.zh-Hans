---
title: 使用流服务API将MySQL连接到Experience Platform
description: 了解如何使用API将MySQL数据库连接到Experience Platform。
exl-id: 273da568-84ed-4a3d-bfea-0f5b33f1551a
source-git-commit: 659af23c6d05f184b745e13ab8545941f3892e7e
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API将[!DNL MySQL]连接到Experience Platform

阅读本指南，了解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)将您的[!DNL MySQL]帐户连接到Adobe Experience Platform。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL MySQL]所需了解的其他信息。

### 收集所需的凭据

有关身份验证的信息，请阅读[[!DNL MySQL] 概述](../../../../connectors/databases/mysql.md#prerequisites)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请阅读[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 将[!DNL MySQL]连接到Azure上的Experience Platform {#azure}

有关如何将您的[!DNL MySQL]帐户连接到Azure上的Experience Platform的信息，请阅读以下步骤。

### 在Azure上的Experience Platform上为[!DNL MySQL]创建基础连接 {#azure-base}

基本连接可将您的源链接到Experience Platform，以存储身份验证详细信息、连接状态和唯一ID。 使用此ID浏览源文件并标识要摄取的特定项目，包括其数据类型和格式。

**API格式**

```https
POST /connections
```

要创建基本连接ID，请向`/connections`端点发出POST请求，并在请求参数中提供[!DNL MySQL]身份验证凭据。

>[!BEGINTABS]

>[!TAB 基于连接字符串的身份验证]

**请求**

以下请求使用基于连接字符串的身份验证为[!DNL MySQL]创建基本连接。

+++查看请求示例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Connection String,
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `auth.params.connectionString` | 与您的帐户关联的[!DNL MySQL]连接字符串。 [!DNL MySQL]连接字符串模式为： `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 |
| `connectionSpec.id` | [!DNL MySQL]连接规范ID： `26d738e0-8963-47ea-aadf-c60de735468a`。 |

+++

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。

+++查看响应示例

```json
{
    "id": "1a444165-3439-4c16-8441-653439dc166a",
    "etag": "\"5b04c219-0000-0200-0000-5e179c8f0000\""
}
```

+++

>[!TAB 基本身份验证]

**请求**

以下请求使用基本身份验证为[!DNL MySQL]源创建基本连接。

+++查看请求示例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL Base Connection to Experience Platform",
      "description": "Via Basic Authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSLMODE}"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `auth.params.server` | [!DNL MySQL]数据库的名称或IP。 |
| `auth.params.database` | 数据库的名称。 |
| `auth.params.username` | 与数据库对应的用户名。 |
| `auth.params.password` | 与数据库对应的密码。 |
| `auth.params.sslMode` | 在数据传输期间对数据进行加密的方法。 |
| `connectionSpec.id` | [!DNL MySQL]连接规范ID为： `26d738e0-8963-47ea-aadf-c60de735468a`。 |

+++

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。

+++查看响应示例

```json
{
    "id": "025d4158-4113-403b-b551-e81724d3880c",
    "etag": "\"ae004437-0000-0200-0000-67ee107e0000\""
}
```

+++

>[!ENDTABS]

## 将[!DNL MySQL]连接到Amazon Web Services上的Experience Platform {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../../../landing/multi-cloud.md)。

有关如何将您的[!DNL MySQL]帐户连接到AWS上的Experience Platform的信息，请阅读以下步骤。

### 在AWS上的Experience Platform上为[!DNL MySQL]创建基本连接 {#aws-base}

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL MySQL]创建基本连接以连接到AWS上的Experience Platform。

+++查看请求示例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MySQL on Experience Platform AWS",
      "description": "MySQL on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "database": "{DATABASE}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "sslMode": "{SSLMODE}"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `auth.params.server` | [!DNL MySQL]数据库的名称或IP。 |
| `auth.params.database` | 数据库的名称。 |
| `auth.params.username` | 与数据库对应的用户名。 |
| `auth.params.password` | 与数据库对应的密码。 |
| `auth.params.sslMode` | 在数据传输期间对数据进行加密的方法。 |
| `connectionSpec.id` | [!DNL MySQL]连接规范ID为： `26d738e0-8963-47ea-aadf-c60de735468a`。 |

+++

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。

+++查看响应示例

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## 为[!DNL MySQL]数据创建数据流

现在您已成功连接[!DNL MySQL]数据库，您现在可以[创建数据流并将数据库中的数据摄取到Experience Platform](../../collect/database-nosql.md)。
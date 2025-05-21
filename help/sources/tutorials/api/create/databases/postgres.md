---
title: 使用流服务API将PostgreSQL连接到Experience Platform
description: 了解如何使用API将 [!DNL PostgreSQL] 数据库连接到Experience Platform。
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: f4200ca71479126e585ac76dd399af4092fdf683
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API将[!DNL PostgreSQL]连接到Experience Platform

阅读本指南，了解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)将您的[!DNL PostgreSQL]数据库连接到Adobe Experience Platform。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL PostgreSQL]所需了解的其他信息。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请阅读[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

### 收集所需的凭据

有关身份验证的更多信息，请阅读[[!DNL PostgreSQL] 概述](../../../../connectors/databases/postgres.md)。

### 为连接字符串启用SSL加密

您可以为[!DNL PostgreSQL]连接字符串启用SSL加密，方法是使用以下属性附加连接字符串：

| 属性 | 描述 | 示例 |
| --- | --- | --- |
| `EncryptionMethod` | 允许您对[!DNL PostgreSQL]数据启用SSL加密。 | <uL><li>`EncryptionMethod=0`（已禁用）</li><li>`EncryptionMethod=1`（已启用）</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | 在应用`EncryptionMethod`时验证[!DNL PostgreSQL]数据库发送的证书。 | <uL><li>`ValidationServerCertificate=0`（已禁用）</li><li>`ValidationServerCertificate=1`（已启用）</li></ul> |

以下是附加了SSL加密的[!DNL PostgreSQL]连接字符串的示例： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`。

## 将[!DNL PostgreSQL]连接到Azure上的Experience Platform {#azure}

请阅读以下步骤，了解如何将您的[!DNL PostgreSQL]帐户连接到Azure上的Experience Platform。

### 创建基本连接 {#azure-base}

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL PostgreSQL]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB 基于帐户密钥的身份验证]

**请求**

以下请求使用基于帐户密钥的身份验证为[!DNL PostgreSQL]创建基本连接：

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via connection string",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| ------------- | --------------- |
| `auth.params.connectionString` | 与您的[!DNL PostgreSQL]帐户关联的连接字符串。 [!DNL PostgreSQL]连接字符串模式为： `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`。 |
| `connectionSpec.id` | [!DNL PostgreSQL]连接规范ID： `74a1c565-4e59-48d7-9d67-7c03b8a13137`。 |

+++

**响应**

成功的响应返回新创建的基本连接的唯一标识符(`id`)。

+++查看响应示例

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

+++

>[!TAB 基本身份验证]

**请求**

以下请求使用基本身份验证为[!DNL PostgreSQL]创建基本连接：

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "3306",
              "database": "postgresql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "Allow"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| ---| --- |
| `auth.params.server` | [!DNL PostgreSQL]数据库的名称或IP地址。 |
| `auth.params.port` | 数据库服务器的端口号。 |
| `auth.params.database` | [!DNL PostgreSQL]数据库的名称。 |
| `auth.params.username` | 与您的[!DNL PostgreSQL]数据库身份验证关联的用户名。 |
| `auth.params.password` | 与您的[!DNL PostgreSQL]数据库身份验证关联的密码。 |
| `auth.params.sslMode` | 在数据传输期间对数据进行加密的方法。 可用值包括： `Disable`、`Allow`、`Prefer`、`Verify Ca`和`Verify Full`。 |
| `connectionSpec.id` | [!DNL PostgreSQL]连接规范ID： `74a1c565-4e59-48d7-9d67-7c03b8a13137`。 |

+++

**响应**

成功的响应返回新创建的基本连接的唯一标识符(`id`)。

+++查看响应示例

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

>[!ENDTABS]

## 将[!DNL PostgreSQL]连接到Amazon Web Services上的Experience Platform {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../../../landing/multi-cloud.md)。

有关如何将[!DNL PostgreSQL]数据库连接到AWS上的Experience Platform的信息，请阅读以下步骤。

### 创建基本连接 {#aws-base}

要创建基本连接ID，请在提供您的[!DNL PostgreSQL]身份验证凭据作为请求参数的一部分时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL PostgreSQL]创建基本连接以连接到AWS上的Experience Platform。

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
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "3306",
              "database": "postgresql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "false"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| ---| --- |
| `auth.params.server` | [!DNL PostgreSQL]数据库的名称或IP地址。 |
| `auth.params.port` | 数据库服务器的端口号。 |
| `auth.params.database` | [!DNL PostgreSQL]数据库的名称。 |
| `auth.params.username` | 与您的[!DNL PostgreSQL]数据库身份验证关联的用户名。 |
| `auth.params.password` | 与您的[!DNL PostgreSQL]数据库身份验证关联的密码。 |
| `sslMode` | 一个布尔值，它控制是否强制使用SSL，具体取决于您的服务器支持。 此配置默认为`false`。 |
| `connectionSpec.id` | [!DNL PostgreSQL]连接规范ID： `74a1c565-4e59-48d7-9d67-7c03b8a13137`。 |

+++

**响应**

成功的响应返回新创建的基本连接的唯一标识符(`id`)。

+++查看响应示例

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

## 后续步骤

现在，您已在[!DNL PostgreSQL]数据库与Experience Platform之间创建了连接，接下来可以继续操作步骤，并将[!DNL PostgreSQL]数据导入Experience Platform。 有关详细信息，请阅读以下文档：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将数据库数据引入Experience Platform](../../collect/database-nosql.md)

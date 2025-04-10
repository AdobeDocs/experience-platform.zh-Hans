---
title: 使用流服务API将MariaDB连接到Experience Platform
description: 了解如何使用API将您的MariaDB帐户连接到Experience Platform。
exl-id: 9b7ff394-ca55-4ab4-99ef-85c80b04a6df
source-git-commit: d5d47f9ca3c01424660fe33f8310586a70a32875
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API将[!DNL MariaDB]连接到Experience Platform

阅读本指南，了解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)将您的[!DNL MariaDB]帐户连接到Adobe Experience Platform。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL MariaDB]所需了解的其他信息。

### 收集所需的凭据

有关身份验证的信息，请阅读[[!DNL MariaDB] 概述](../../../../connectors/databases/mariadb.md#prerequisites)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请阅读[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 将[!DNL MariaDB]连接到Azure上的Experience Platform {#azure}

有关如何将您的[!DNL MariaDB]帐户连接到Azure上的Experience Platform的信息，请阅读以下步骤。

### 在Azure上的Experience Platform上为[!DNL MariaDB]创建基础连接 {#azure-base}

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

**API格式**

```https
POST /connections
```

要创建基本连接ID，请向`/connections`端点发出POST请求，并为您的[!DNL MariaDB]帐户提供适当的身份验证凭据。

>[!BEGINTABS]

>[!TAB 基于连接字符串的身份验证]

**请求**

以下请求使用基于连接字符串的身份验证为[!DNL MariaDB]源创建基本连接。

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
    "name": "MariaDB connection",
    "description": "MariaDB connection",
    "auth": {
        "specName": "Connection String Based Authentication",
        "params": {
            "connectionString": "Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}"
        }
    },
    "connectionSpec": {
        "id": "3000eb99-cd47-43f3-827c-43caf170f015",
        "version": "1.0"
    }
}'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.connectionString` | 与您的[!DNL MariaDB]身份验证关联的连接字符串。 [!DNL MariaDB]连接字符串模式为： `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 |
| `connectionSpec.id` | [!DNL MariaDB]连接规范ID为： `3000eb99-cd47-43f3-827c-43caf170f015`。 |

+++

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。

+++查看响应示例

```json
{
    "id": "be3a2d71-1fb6-4fea-ba2d-711fb61fea50",
    "etag": "\"02002624-0000-0200-0000-5e41f7040000\""
}
```

+++

>[!TAB 基本身份验证]

**请求**

以下请求使用基本身份验证为[!DNL MariaDB]源创建基本连接。

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
      "name": "MariaDB on Experience Platform using basic auth",
      "description": "MariaDB on Experience Platform using basic auth",
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
          "id": "3000eb99-cd47-43f3-827c-43caf170f015",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `auth.params.server` | [!DNL MariaDB]数据库的名称或IP。 |
| `auth.params.database` | 数据库的名称。 |
| `auth.params.username` | 与数据库对应的用户名。 |
| `auth.params.password` | 与数据库对应的密码。 |
| `auth.params.sslMode` | 在数据传输期间对数据进行加密的方法。 |
| `connectionSpec.id` | [!DNL MariaDB]连接规范ID为： `3000eb99-cd47-43f3-827c-43caf170f015`。 |

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

>[!ENDTABS]

## 将[!DNL MariaDB]连接到Amazon Web Services上的Experience Platform {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../../../landing/multi-cloud.md)。

有关如何将您的[!DNL MariaDB]帐户连接到AWS上的Experience Platform的信息，请阅读以下步骤。

### 在AWS上的Experience Platform上为[!DNL MariaDB]创建基本连接 {#aws-base}

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL MariaDB]创建基本连接以连接到AWS上的Experience Platform。

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
      "name": "MariaDB on Experience Platform AWS",
      "description": "MariaDB on Experience Platform AWS",
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
          "id": "3000eb99-cd47-43f3-827c-43caf170f015",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `auth.params.server` | [!DNL MariaDB]数据库的名称或IP。 |
| `auth.params.database` | 数据库的名称。 |
| `auth.params.username` | 与数据库对应的用户名。 |
| `auth.params.password` | 与数据库对应的密码。 |
| `auth.params.sslMode` | 在数据传输期间对数据进行加密的方法。 |
| `connectionSpec.id` | [!DNL MariaDB]连接规范ID为： `3000eb99-cd47-43f3-827c-43caf170f015`。 |

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


## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL MariaDB]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将数据库数据引入Experience Platform](../../collect/database-nosql.md)

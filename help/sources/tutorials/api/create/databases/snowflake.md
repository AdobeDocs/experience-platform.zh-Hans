---
title: 使用流服务API将Snowflake连接到Experience Platform
description: 了解如何使用流服务API将Adobe Experience Platform连接到Snowflake。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: 7ccb8f7c6cfe6e3d030e79bc03ea0136003e5dfa
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API将[!DNL Snowflake]连接到Experience Platform

>[!IMPORTANT]
>
>[!DNL Snowflake]源在源目录中可供已购买Real-Time Customer Data Platform Ultimate的用户使用。

阅读本指南，了解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)将您的[!DNL Snowflake]源帐户连接到Adobe Experience Platform。

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform]允许从各种源摄取数据，同时允许您使用[!DNL Experience Platform]服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供将单个[!DNL Experience Platform]实例划分为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

以下部分提供了使用[!DNL Flow Service] API成功连接到[!DNL Snowflake]时需要了解的其他信息。

### 收集所需的凭据

有关身份验证的信息，请阅读[[!DNL Snowflake] 概述](../../../../connectors/databases/snowflake.md#prerequisites)。

## 将[!DNL Snowflake]连接到Azure上的Experience Platform {#azure}

有关如何将[!DNL Snowflake]源连接到Azure上的Experience Platform的信息，请阅读以下步骤。

>[!NOTE]
>
>必须将`PREVENT_UNLOAD_TO_INLINE_URL`标志设置为`FALSE`，以允许将数据从[!DNL Snowflake]数据库卸载到Experience Platform。

### 在Azure上的Experience Platform上为[!DNL Snowflake]创建基本连接 {#azure-base}

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在提供您的[!DNL Snowflake]身份验证凭据作为请求正文的一部分时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB 使用加密私钥的密钥对身份验证]

+++请求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with encrypted private key",
      "description": "Snowflake base connection with encrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "privateKeyPassphrase": "abcd1234",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.account` | [!DNL Snowflake]帐户的名称。 |
| `auth.params.username` | 与您的[!DNL Snowflake]帐户关联的用户名。 |
| `auth.params.database` | 将从其中提取数据的[!DNL Snowflake]数据库。 |
| `auth.params.privateKey` | [!DNL Snowflake]帐户的[!DNL Base64-]编码加密私钥。 |
| `auth.params.privateKeyPassphrase` | 与您的私钥对应的密码。 |
| `auth.params.warehouse` | 您正在使用的[!DNL Snowflake]仓库。 |
| `connectionSpec.id` | [!DNL Snowflake]连接规范ID： `b2e08744-4f1a-40ce-af30-7abac3e23cf3`。 |

+++

+++响应

成功的响应返回新创建的连接的详细信息，包括其唯一标识符(`id`)。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!TAB 使用未加密私钥的密钥对身份验证]

+++请求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with unencrypted private key",
      "description": "Snowflake base connection with unencrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.account` | [!DNL Snowflake]帐户的名称。 |
| `auth.params.username` | 与您的[!DNL Snowflake]帐户关联的用户名。 |
| `auth.params.database` | 将从其中提取数据的[!DNL Snowflake]数据库。 |
| `auth.params.privateKey` | [!DNL Snowflake]帐户的[!DNL Base64-]编码未加密私钥。 |
| `auth.params.warehouse` | 您正在使用的[!DNL Snowflake]仓库。 |
| `connectionSpec.id` | [!DNL Snowflake]连接规范ID： `b2e08744-4f1a-40ce-af30-7abac3e23cf3`。 |

+++

+++响应

成功的响应返回新创建的连接的详细信息，包括其唯一标识符(`id`)。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

>[!ENDTABS]

## 将[!DNL Snowflake]连接到Amazon Web Services (AWS)上的Experience Platform {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../../../landing/multi-cloud.md)。

有关如何将[!DNL Snowflake]源连接到AWS上的Experience Platform的信息，请阅读以下步骤。

### 在AWS的Experience Platform上为[!DNL Snowflake]创建基本连接 {#aws-base}

**API格式**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 基本身份验证]

以下请求为[!DNL Snowflake]创建基本连接，以便将数据摄取到AWS上的Experience Platform：

+++请求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection for Experience Platform on AWS",
      "description": "Snowflake base connection for Experience Platform on AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme.snowflakecomputing.com",
              "port": "443",
              "username": "acme-cj123",
              "password": "{PASSWORD}",
              "database": "ACME_DB",
              "warehouse": "COMPUTE_WH",
              "schema": "{SCHEMA}"
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `auth.params.host` | 您的[!DNL Snowflake]帐户连接到的主机URL。 |
| `auth.params.port` | [!DNL Snowflake]通过Internet连接到服务器时使用的端口号。 |
| `auth.params.username` | 与您的[!DNL Snowflake]帐户关联的用户名。 |
| `auth.params.database` | 将从其中提取数据的[!DNL Snowflake]数据库。 |
| `auth.params.password` | 与您的[!DNL Snowflake]帐户关联的密码。 |
| `auth.params.warehouse` | 您正在使用的[!DNL Snowflake]仓库。 |
| `auth.params.schema` | 与您的[!DNL Snowflake]数据库关联的架构的名称。 您必须确保要为其授予数据库访问权限的用户也具有此架构的访问权限。 |

+++

+++响应

成功的响应返回新创建的连接的详细信息，包括其唯一标识符(`id`)。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++

>[!TAB 使用未加密私钥的密钥对身份验证]

+++请求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection with unencrypted private key",
      "description": "Snowflake base connection with unencrypted private key",
      "auth": {
        "specName": "KeyPair Authentication",
        "params": {
            "account": "acme-snowflake123",
            "username": "acme-cj123",
            "database": "ACME_DB",
            "privateKey": "{BASE_64_ENCODED_PRIVATE_KEY}",
            "warehouse": "COMPUTE_WH"
        }
    },
    "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
    }
  }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `auth.params.account` | [!DNL Snowflake]帐户的名称。 |
| `auth.params.username` | 与您的[!DNL Snowflake]帐户关联的用户名。 |
| `auth.params.database` | 将从其中提取数据的[!DNL Snowflake]数据库。 |
| `auth.params.privateKey` | [!DNL Snowflake]帐户的[!DNL Base64-]编码未加密私钥。 |
| `auth.params.warehouse` | 您正在使用的[!DNL Snowflake]仓库。 |
| `connectionSpec.id` | [!DNL Snowflake]连接规范ID： `b2e08744-4f1a-40ce-af30-7abac3e23cf3`。 |

+++


+++响应

成功的响应返回新创建的连接的详细信息，包括其唯一标识符(`id`)。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700d77b-0000-0200-0000-5e3b41a10000\""
}
```

+++

>[!ENDTABS]

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Snowflake]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将数据库数据引入Experience Platform](../../collect/database-nosql.md)

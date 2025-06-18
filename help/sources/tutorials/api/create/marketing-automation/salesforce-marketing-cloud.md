---
title: 使用流服务API将Salesforce Marketing Cloud连接到Experience Platform
description: 了解如何使用API将您的Salesforce Marketing Cloud帐户连接到Experience Platform。
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 0c0a58df4beae499008e52c118b40bed86ff0596
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API将[!DNL Salesforce Marketing Cloud]连接到Experience Platform

>[!WARNING]
>
>[!DNL Salesforce Marketing Cloud]源将于2026年1月被弃用。 作为替代方案，将在今年晚些时候发布新的信息源。 发布新源后，您必须计划在2026年1月底之前通过创建新帐户连接和数据流迁移到新源。

阅读本指南，了解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)将您的[!DNL Salesforce Marketing Cloud]帐户连接到Adobe Experience Platform。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL Azure Synapse Analytics]所需了解的其他信息。


### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

以下部分提供了使用[!DNL Flow Service] API成功连接到[!DNL Salesforce Marketing Cloud]时需要了解的其他信息。

### 收集所需的凭据

有关身份验证的信息，请阅读[[!DNL Salesforce Marketing Cloud] 身份验证概述](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请阅读[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 将[!DNL Salesforce Marketing Cloud]连接到[!DNL Azure]上的Experience Platform

请阅读以下内容，了解如何创建基本连接并将您的[!DNL Salesforce Marketing Cloud]帐户连接到[!DNL Azure]上的Experience Platform。

### 创建基本连接 {#azure-base}

>[!IMPORTANT]
>
>[!DNL Salesforce Marketing Cloud]源集成当前不支持自定义对象摄取。

**基本连接**&#x200B;存储将源系统链接到Adobe Experience Platform的密钥信息。 这包括：

* 您来源的身份验证凭据
* 连接的当前状态
* 唯一的&#x200B;**基本连接ID**

**基本连接ID**&#x200B;允许您浏览和浏览源中的文件，帮助您识别要摄取的项及其数据类型和格式。

要创建基本连接ID，请向`/connections`端点发送POST请求，包括请求参数中的[!DNL Salesforce Marketing Cloud]身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL Salesforce Marketing Cloud]创建基本连接。

+++查看示例请求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Salesforce Marketing Cloud base connection for Azure",
    "description": "Salesforce Marketing Cloud base connection for Azure",
    "auth": {
      "specName": "Client-Id-Secret Based Authentication",
      "params": {
        "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst",
        "clientId": "acme-salesforce-marketing-cloud",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

| 属性 | 描述 |
| --- | --- |
| `auth.params.host` |
| `auth.params.clientId` | 与您的[!DNL Salesforce Marketing Cloud]应用程序关联的客户端ID。 |
| `auth.params.clientSecret` | 与您的[!DNL Salesforce Marketing Cloud]应用程序关联的客户端密钥。 |
| `connectionSpec.id` | [!DNL Salesforce Marketing Cloud]连接规范ID： `ea1c2a08-b722-11eb-8529-0242ac130003`。 |

+++

+++查看示例响应

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++

## 将[!DNL Salesforce Marketing Cloud]连接到Amazon Web Services上的Experience Platform {#aws}

>[!AVAILABILITY]
>
>本节适用于在Amazon Web Services (AWS)上运行的Experience Platform的实施。 在AWS上运行的Experience Platform当前仅对有限数量的客户可用。 要了解有关支持的Experience Platform基础架构的更多信息，请参阅[Experience Platform multi-cloud概述](../../../../../landing/multi-cloud.md)。

有关如何将您的[!DNL Salesforce Marketing Cloud]帐户连接到AWS上的Experience Platform的信息，请阅读以下步骤。

### 创建基本连接 {#aws-base}

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL Salesforce Service Cloud]创建基本连接以连接到AWS上的Experience Platform。

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
    "name": "Salesforce Marketing Cloud base connection for AWS",
    "description": "Salesforce Marketing Cloud base connection for AWS",
    "auth": {
      "specName": "OAuth2 Client Credential",
      "params": {
        "subdomain": "mc563885gzs27c5t9-63k636ttgm",
        "clientId": "3a1b2c3d4e5f67890123456789abcdef",
        "clientSecret": "xxxx"
      }
    },
    "connectionSpec": {
      "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
      "version": "1.0"
    }
  }'
```

+++

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。

+++查看响应示例

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

+++


## 为[!DNL Salesforce Marketing Cloud]数据创建数据流

现在您已成功连接[!DNL Salesforce Marketing Cloud]帐户，您现在可以[创建数据流并将营销自动化提供商中的数据摄取到Experience Platform](../../collect/marketing-automation.md)。
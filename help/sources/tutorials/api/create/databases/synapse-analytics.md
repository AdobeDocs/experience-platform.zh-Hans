---
title: 使用流服务API将Azure Synapse Analytics连接到Experience Platform
description: 了解如何使用API将您的Azure Synapse Analytics帐户连接到Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 8944ac3f-366d-49c8-882f-11cd0ea766e4
source-git-commit: b8497ede7f90717ed23bcd10b7abe51de18e08a5
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API将[!DNL Azure Synapse Analytics]连接到Experience Platform

>[!IMPORTANT]
>
>[!DNL Azure Synapse Analytics]源在源目录中可供已购买Real-Time Customer Data Platform Ultimate的用户使用。

阅读本指南，了解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)将您的[!DNL Azure Synapse Analytics]帐户连接到Adobe Experience Platform。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供使用[!DNL Flow Service] API成功连接到[!DNL Azure Synapse Analytics]所需了解的其他信息。

### 收集所需的凭据

有关身份验证的信息，请阅读[[!DNL Azure Synapse Analytics] 概述](../../../../connectors/databases/synapse-analytics.md#prerequisites)。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请参阅[Experience Platform API快速入门](../../../../../landing/api-guide.md)指南。

## 将[!DNL Azure Synapse Analytics]连接到Experience Platform

请阅读以下内容，了解如何创建基本连接并将[!DNL Azure Synapse Analytics]帐户连接到Experience Platform。

### 创建基本连接

**基本连接**&#x200B;存储将源系统链接到Adobe Experience Platform的密钥信息。 这包括：

* 您来源的身份验证凭据
* 连接的当前状态
* 唯一的&#x200B;**基本连接ID**

**基本连接ID**&#x200B;允许您浏览和浏览源中的文件，帮助您识别要摄取的项及其数据类型和格式。

要创建基本连接ID，请向`/connections`端点发送POST请求，包括请求参数中的[!DNL Azure Synapse Analytics]身份验证凭据。

**API格式**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB 基于连接字符串的身份验证]

**请求**

以下请求使用基于连接字符串的身份验证为[!DNL Azure Synapse Analytics]创建基本连接。

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
      "name": "Connection for Azure Synapse Analytics",
      "description": "Connection for Azure Synapse Analytics",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
          }
      },
      "connectionSpec": {
          "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
          "version": "1.0"
      }
  }'
```

| 参数 | 描述 |
| --------- | ----------- |
| `auth.params.connectionString` | 用于连接到[!DNL Azure Synapse Analytics]的连接字符串。 [!DNL Azure Synapse Analytics]连接字符串模式为`Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`。 |
| `connectionSpec.id` | [!DNL Azure Synapse Analytics]连接规范ID为： `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`。 |

+++

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。

+++查看示例响应

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!TAB 基于服务主体密钥的身份验证]

以下请求使用基于服务主体密钥的身份验证为[!DNL Azure Synapse Analytics]创建基本连接。

**请求**

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
    "name": "Connection for Azure Synapse Analytics",
    "description": "Connection for Azure Synapse Analytics",
    "auth": {
      "specName": "Service Principal Key Based Authentication",
      "params": {
        "server": "yourworkspace.sql.azuresynapse.net",
        "database": "SalesDW",
        "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "servicePrincipalId": "e7b8c1f2-1234-4c9a-9f3e-abcdef123456",
        "servicePrincipalKey": "~XyZ1234abcDEF5678..."
      }
    },
    "connectionSpec": {
      "id": "a49bcc7d-8038-43af-b1e4-5a7a089a7d79",
      "version": "1.0"
    }
  }'
```

| 凭据 | 描述 |
| --- | --- |
| `auth.params.server` | [!DNL Azure Synapse Analytics] SQL端点的完全限定域名。 |
| `auth.params.database` | [!DNL Azure Synapse Analytics]工作区中特定数据库的名称。 |
| `auth.params.tenant` | 与您的[!DNL Azure]订阅关联的[!DNL Azure Active Directory]租户ID。 |
| `auth.params.servicePrincipalId` | [!DNL Azure Active Directory]应用程序的客户端ID。 |
| `auth.params.servicePrincipalKey` | 与服务主体关联的客户端密钥或密码。 |
| `connectSpec.id` | 连接规范ID [!DNL Azure Synapse Analytics]。 |

+++

**响应**

成功的响应返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。

+++查看示例响应

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

+++

>[!ENDTABS]

## 后续步骤

通过完成本教程，您已使用[!DNL Flow Service] API创建了[!DNL Azure Synapse Analytics]基本连接。 您可以在下列教程中使用此基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将数据库数据引入Experience Platform](../../collect/database-nosql.md)

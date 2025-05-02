---
title: 使用流服务API将Azure数据库连接到Experience Platform
description: 了解如何使用API将Azure Databricks连接到Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta 版" type="Informative"
exl-id: c3974bab-8e67-49a1-b1a5-d453cf7bfd1d
source-git-commit: 30f1c16084b3049fae45e26db0eed03888d35516
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API将[!DNL Azure Databricks]连接到Experience Platform

>[!IMPORTANT]
>
>[!DNL Azure Databricks]源在源目录中可供已购买Real-Time CDP Ultimate的用户使用。

阅读本指南，了解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)将您的[!DNL Azure Databricks]帐户连接到Adobe Experience Platform。

## 快速入门

本指南要求您对Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 使用Experience Platform API

有关如何成功调用Experience Platform API的信息，请阅读[如何开始使用Experience Platform API](../../../../../landing/api-guide.md)的指南。

### 配置必备项设置

请阅读[[!DNL Databricks] 概述](../../../../connectors/databases/databricks.md)，了解在将帐户连接到Experience Platform之前必须完成的先决条件配置。

### 收集所需的凭据

提供以下凭据的值以将[!DNL Databricks]连接到Experience Platform。

| 凭据 | 描述 |
| --- | --- |
| `domain` | [!DNL Databricks]工作区的URL。 例如：`https://adb-1234567890123456.7.azuredatabricks.net`。 |
| `clusterId` | [!DNL Databricks]中集群的ID。 此群集必须已经是现有的群集，并且应该是一个交互式群集。 |
| `accessToken` | 用于验证您的[!DNL Databricks]帐户的访问令牌。 您可以使用[!DNL Databricks]工作区生成访问令牌。 |
| `database` | 增量湖中数据库的名称。 |
| `connectionSpec.Id` | 连接规范ID返回源的连接器属性，包括与创建基础连接和源连接相关的身份验证规范。 [!DNL Databricks]的连接规范ID为`e9d7ec6b-0873-4e57-ad21-b3a7c65e310b`。 |

## 创建基本连接

基本连接会保留源与Experience Platform之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请向`/connections`端点发出POST请求，并为您的[!DNL Databricks]帐户提供适当的身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求使用访问令牌身份验证为[!DNL Databricks]源创建基本连接。

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
    "name": "Databricks connection to Experience Platform",
    "description": "A Databricks base connection to Experience Platform",
    "auth": {
        "specName": "Access Token Authentication",
        "params": {
          "domain": "https://adb-1234567890123456.7.azuredatabricks.net",
          "clusterId": "xxxx",
          "accessToken": "xxxx",
          "database": "acme-db"
        }
    },
    "connectionSpec": {
        "id": "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b",
        "version": "1.0"
    }
}'
```

| 属性 | 描述 |
| --- | --- |
| `auth.params.domain` | [!DNL Databricks]工作区的URL。 |
| `auth.params.clusterId` | [!DNL Databricks]中集群的ID。 此群集必须已经是现有的群集，并且应该是一个交互式群集 |
| `auth.params.accessToken` | 用于验证您的[!DNL Databricks]帐户的访问令牌。 |
| `auth.params.database` | 增量湖中数据库的名称。 |
| `connectionSpec.id` | [!DNL Databricks]连接规范ID。 |

+++

**响应**

成功的响应将返回您新创建的连接，包括基本连接ID。

+++查看响应示例

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## 后续步骤

通过学习本教程，您已成功在[!DNL Databricks]帐户与Experience Platform之间创建了连接。 您可以在下列教程中使用新生成的基本连接ID：

* [使用 [!DNL Flow Service] API浏览数据表的结构和内容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API创建数据流以将数据库数据引入Experience Platform](../../collect/database-nosql.md)

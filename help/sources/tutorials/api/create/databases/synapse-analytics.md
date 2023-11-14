---
title: 使用流服务API创建Azure synapseAnalytics基本连接
description: 了解如何使用流服务API将Azure synapse Analytics连接到Adobe Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 8944ac3f-366d-49c8-882f-11cd0ea766e4
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 4%

---

# 创建 [!DNL Azure Synapse Analytics] 基本连接使用 [!DNL Flow Service] API

>[!IMPORTANT]
>
>此 [!DNL Azure Synapse Analytics] 源目录中的源可供已购买Real-time Customer Data Platform Ultimate的用户使用。

基本连接表示源和Adobe Experience Platform之间的已验证连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL Azure Synapse Analytics] (以下简称“[!DNL Synapse]&quot;)使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下内容构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个文件夹进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供成功连接时需要了解的其他信息 [!DNL Synapse] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接 [!DNL Synapse]中，您必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 用于连接的连接字符串 [!DNL Synapse]. 此 [!DNL Synapse] 连接字符串模式为 `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 的连接规范ID [!DNL Synapse] 为： `a49bcc7d-8038-43af-b1e4-5a7a089a7d79` |

有关获取连接字符串的详细信息，请参阅 [此Synapse文档](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure?toc=%2Fazure%2Fsynapse-analytics%2Fsql-data-warehouse%2Ftoc.json&amp;bc=%2Fazure%2Fsynapse-analytics%2Fsql-data-warehouse%2Fbreadcrumb%2Ftoc.json&amp;tabs=azure-powershell).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点，同时提供 [!DNL Synapse] 作为请求参数一部分的身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求为创建基本连接 [!DNL Synapse]：

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
| `auth.params.connectionString` | 用于连接的连接字符串 [!DNL Synapse]. 此 [!DNL Synapse] 连接字符串模式为 `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |
| `connectionSpec.id` | 此 [!DNL Synapse] 连接规范ID为： `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. |

**响应**

成功的响应会返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下个教程中，浏览您的数据库时需要此ID。

```json
{
    "id": "6bc13a3b-3546-455f-813a-3b3546a55fb1",
    "etag": "\"3500866c-0000-0200-0000-5e83afa30000\""
}
```

## 后续步骤

在本教程之后，您已创建一个 [!DNL Synapse] 基本连接使用 [!DNL Flow Service] API。 您可以在下列教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流以使用将数据库数据引入Platform [!DNL Flow Service] API](../../collect/database-nosql.md)

---
title: 使用流服务API创建Microsoft SQL Server基本连接
type: Tutorial
description: 了解如何使用流服务API将Adobe Experience Platform连接到Microsoft SQL Server。
exl-id: 00455a61-c8c1-42f4-a962-fc16f7370cbd
source-git-commit: 1828dd76e9ff317f97e9651331df3e49e44efff5
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 5%

---

# 创建 [!DNL Microsoft] SQL Server基本连接使用 [!DNL Flow Service] API

基本连接表示源和Adobe Experience Platform之间的已验证连接。

阅读本教程，了解如何为创建基本连接 [!DNL Microsoft SQL Server] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对 Adobe Experience Platform 的以下组件有一定了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

以下部分提供成功连接时需要了解的其他信息 [!DNL Microsoft SQL Server] 使用 [!DNL Flow Service] API。

### 收集所需的凭据 {#gather-required-credentials}

为了连接到 [!DNL Microsoft SQL Server]中，您必须提供以下连接属性：

| 凭据 | 描述 | 示例 |
| --- | --- | --- |
| `connectionString` | 与您的关联的连接字符串 [!DNL Microsoft SQL Server] 帐户。 您的连接字符串模式取决于您是使用服务器名称还是实例名称作为数据源：<ul><li>使用服务器名的连接字符串： `Data Source={SERVER_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};`</li><li>使用实例名称的连接字符串：`Data Source={INSTANCE_NAME};Initial Catalog={DATABASE};Integrated Security=False;User ID={USER_ID};Password={PASSWORD};` | `Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword` |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的验证规范。 的连接规范ID [!DNL Microsoft SQL Server] 是 `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

有关获取连接字符串的详细信息，请参阅此 [[!DNL Microsoft SQL Server] 文档](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留您的源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点，同时提供 [!DNL Microsoft SQL Server] 作为请求参数一部分的身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求为创建基本连接 [!DNL Microsoft SQL Server]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for sql-server",
      "description": "Base connection for sql-server",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Data Source=mssqlserver.database.windows.net;Initial Catalog=mssqlserver_e2e_db;Integrated Security=False;User ID=mssqluser;Password=mssqlpassword"
          }
      },
      "connectionSpec": {
          "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
          "version": "1.0"
  }'
```

| 属性 | 描述 |
| --- | --- |
| `auth.params.connectionString` | 与您的关联的连接字符串 [!DNL Microsoft SQL Server] 帐户。 阅读以下部分： [正在收集所需的凭据](#gather-required-credentials) 以了解更多信息。 |
| `connectionSpec.id` | 此 [!DNL Microsoft SQL Server] 连接规范ID为： `1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`. |

**响应**

成功的响应会返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下个教程中，浏览您的数据库时需要此ID。

```json
{
    "id": "0b8224e4-0de8-4293-8224-e40de80293c6",
    "etag": "\"5802c519-0000-0200-0000-5e4d89520000\""
}
```

## 后续步骤

在本教程之后，您已创建一个 [!DNL Microsoft SQL Server] 基本连接使用 [!DNL Flow Service] API。 您可以在下列教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [创建数据流以使用将数据库数据引入Platform [!DNL Flow Service] API](../../collect/database-nosql.md)
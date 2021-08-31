---
keywords: Experience Platform；主页；热门主题；Microsoft SQL;Microsoft SQL;SQL Server;SQL Server
solution: Experience Platform
title: 使用流服务API创建SQL Server基连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流服务API将Adobe Experience Platform连接到Microsoft SQL Server。
exl-id: 00455a61-c8c1-42f4-a962-fc16f7370cbd
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API创建[!DNL Microsoft] SQL Server基连接

基本连接表示源与Adobe Experience Platform之间经过验证的连接。

本教程将指导您完成使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)为[!DNL Microsoft SQL Server]创建基本连接的步骤。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [来源](../../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单独虚 [!DNL Platform] 拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

以下部分提供了您需要了解的其他信息，以便您能够使用[!DNL Flow Service] API成功连接到[!DNL Microsoft SQL Server]。

### 收集所需的凭据

要连接到[!DNL Microsoft SQL Server]，必须提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 与您的[!DNL Microsoft SQL Server]帐户关联的连接字符串。 [!DNL Microsoft SQL Server]连接字符串模式为：`Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`。 |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基连接和源连接相关的验证规范。 [!DNL Microsoft SQL Server]的连接规范ID为`1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`。 |

有关获取连接字符串的详细信息，请参阅此[[!DNL Microsoft SQL Server] 文档](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server)。

### 使用Platform API

有关如何成功调用Platform API的信息，请参阅[Platform API入门指南](../../../../../landing/api-guide.md)。

## 创建基本连接

基本连接保留了源和平台之间的信息，包括源的身份验证凭据、连接的当前状态和唯一基本连接ID。 基本连接ID允许您从源中浏览和导航文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

要创建基本连接ID，请在请求参数中提供[!DNL Microsoft SQL Server]身份验证凭据时，向`/connections`端点发出POST请求。

**API格式**

```https
POST /connections
```

**请求**

以下请求为[!DNL Microsoft SQL Server]创建基本连接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for sql-server",
        "description": "Base connection for sql-server",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};"
            }
        },
        "connectionSpec": {
            "id": "1f372ff9-38a4-4492-96f5-b9a4e4bd00ec",
            "version": "1.0"
    }'
```

| 属性 | 描述 |
| --------- | ----------- |
| `auth.params.connectionString` | 与您的[!DNL Microsoft SQL Server]帐户关联的连接字符串。 [!DNL Microsoft SQL Server]连接字符串模式为：`Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`。 |
| `connectionSpec.id` | [!DNL Microsoft SQL Server]连接规范ID为：`1f372ff9-38a4-4492-96f5-b9a4e4bd00ec`。 |

**响应**

成功的响应返回新创建连接的详细信息，包括其唯一标识符(`id`)。 在下一个教程中浏览数据库时需要此ID。

```json
{
    "id": "0b8224e4-0de8-4293-8224-e40de80293c6",
    "etag": "\"5802c519-0000-0200-0000-5e4d89520000\""
}
```

## 后续步骤

在本教程中，您已使用[!DNL Flow Service] API创建了[!DNL Microsoft SQL Server]连接，并获取了该连接的唯一ID值。 在下一个教程中，您可以使用此连接ID，因为您正在学习如何使用流服务API](../../explore/database-nosql.md)来浏览数据库或NoSQL系统。[

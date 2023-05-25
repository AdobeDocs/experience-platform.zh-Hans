---
keywords: Experience Platform；主页；热门主题；MariaDB；mariadb
solution: Experience Platform
title: 使用流服务API创建MariaDB基本连接
type: Tutorial
description: 了解如何使用Flow Service API将Adobe Experience Platform连接到MariaDB。
exl-id: 9b7ff394-ca55-4ab4-99ef-85c80b04a6df
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 2%

---

# 创建 [!DNL MariaDB] 基本连接使用 [!DNL Flow Service] API

基本连接表示源和Adobe Experience Platform之间经过身份验证的连接。

本教程将指导您完成创建基本连接的步骤。 [!DNL MariaDB] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下方式构建、标记和增强传入数据： [!DNL Platform] 服务。
* [沙盒](../../../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下部分提供了成功连接时需要了解的其他信息 [!DNL MariaDB] 使用 [!DNL Flow Service] API。

### 收集所需的凭据

为了 [!DNL Flow Service] 以连接 [!DNL MariaDB]，您必须提供以下连接属性：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 与您的关联的连接字符串 [!DNL MariaDB] 身份验证。 此 [!DNL MariaDB] 连接字符串模式为： `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | 连接规范返回源的连接器属性，包括与创建基础连接和源连接相关的身份验证规范。 的连接规范ID [!DNL MariaDB] 是 `3000eb99-cd47-43f3-827c-43caf170f015`. |

有关获取连接字符串的更多信息，请参阅此 [[!DNL MariaDB] 文档](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

### 使用平台API

有关如何成功调用Platform API的信息，请参阅 [Platform API快速入门](../../../../../landing/api-guide.md).

## 创建基本连接

基本连接会保留源和平台之间的信息，包括源的身份验证凭据、连接的当前状态以及唯一的基本连接ID。 基本连接ID允许您浏览和浏览源中的文件，并标识要摄取的特定项目，包括有关其数据类型和格式的信息。

POST要创建基本连接ID，请向 `/connections` 端点同时提供 [!DNL MariaDB] 作为请求参数一部分的身份验证凭据。

**API格式**

```https
POST /connections
```

**请求**

以下请求创建基本连接 [!DNL MariaDB]：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for maria-db",
        "description": "Test connection for maria-db",
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
| `auth.params.connectionString` | 与您的关联的连接字符串 [!DNL MariaDB] 身份验证。 此 [!DNL MariaDB] 连接字符串模式为： `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | 此 [!DNL MariaDB] 连接规范ID为： `3000eb99-cd47-43f3-827c-43caf170f015`. |

**响应**

成功响应将返回新创建的基本连接的详细信息，包括其唯一标识符(`id`)。 在下一步中浏览数据库时需要此ID。

```json
{
    "id": "be3a2d71-1fb6-4fea-ba2d-711fb61fea50",
    "etag": "\"02002624-0000-0200-0000-5e41f7040000\""
}
```

## 后续步骤

按照本教程，您已创建了一个 [!DNL MariaDB] 基本连接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本连接ID：

* [使用浏览数据表的结构和内容 [!DNL Flow Service] API](../../explore/tabular.md)
* [使用创建数据流以将数据库数据引入Platform [!DNL Flow Service] API](../../collect/database-nosql.md)

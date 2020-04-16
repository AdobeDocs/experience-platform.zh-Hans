---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API创建PostgreSQL连接器
topic: overview
translation-type: tm+mt
source-git-commit: aa9e1e5ab345978e6f4727affb741ef69435e703

---


# 使用Flow Service API创建PostgreSQL连接器

Flow Service用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用Flow Service API指导您完成将Experience Platform连接到PostgreSQL（以下简称“PSQL”）的步骤。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供了使用Flow Service API成功连接到PSQL时需要了解的其他信息。

### 收集所需的凭据

要使Flow Service与PSQL连接，必须提供以下连接属性：

| 凭证 | 描述 |
| ---------- | ----------- |
| `connectionString` | 与您的PSQL帐户关联的连接字符串。 |

有关快速入门的详细信息，请参阅此 [PSQL文档](https://www.postgresql.org/docs/9.2/app-psql.html)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../../../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

* 授权：承载人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源（包括属于流服务的资源）都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标题：

* 内容类型： `application/json`

## 查找连接规范

要创建PSQL连接，流服务中必须存在一组PSQL连接规范。 将平台连接到PSQL的第一步是检索这些规范。

**API格式**

每个可用源都有其自己唯一的连接规范集，用于描述连接器属性，如身份验证要求。 向端点发送GET请求将返 `/connectionSpecs` 回所有可用源的连接规范。 您还可以包含查询，以 `property=name=="postgre-sql"` 获取专用于PSQL的信息。

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="postgre-sql"
```

**请求**

以下请求检索PSQL的连接规范。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="postgre-sql"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回PSQL的连接规范，包括其唯一标识符(`id`)。 下一步中需要此ID才能创建基本连接。

```json
{
    "items": [
        {
            "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
            "name": "postgre-sql",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for PostgreSQL",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to PostgreSQL",
                        "properties": {
                            "connectionString": {
                                "type": "string",
                                "description": "An ODBC connection string to connect to Azure Database for PostgreSQL.",
                                "format": "password"
                            }
                        },
                        "required": [
                            "connectionString"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## 创建基本连接

基本连接指定一个源并包含该源的凭据。 每个PSQL帐户只需要一个基本连接，因为它可用于创建多个源连接器以导入不同的数据。

**API格式**

```http
POST /connections
```

**请求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Base connection for PostgreSQL",
        "description": "Base connection for PostgreSQL",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "{CONNECTION_STRING}"
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
| `auth.params.connectionString` | 与您的PSQL帐户关联的连接字符串。 |
| `connectionSpec.id` | 在上一步 `id` 中检索的PSQL帐户的连接规范。 |

**响应**

成功的响应会返回新创建的基本连接`id`的唯一标识符()。 在下一个教程中浏览PSQL数据库时需要此ID。

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## 后续步骤

通过本教程，您使用Flow Service API创建了一个PSQL基本连接，并获得了该连接的唯一ID值。 在下一个教程中，您可以使用此基本连接ID，因为您将学习如 [何使用Flow Service API浏览数据库或NoSQL系统](../../explore/database-nosql.md)。

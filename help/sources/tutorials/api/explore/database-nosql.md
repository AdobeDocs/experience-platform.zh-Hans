---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API浏览数据库
topic: overview
translation-type: tm+mt
source-git-commit: c4162d88a688ce2028de08b63e7b7eab954a0e29

---


# 使用Flow Service API浏览数据库

Flow Service用于在Adobe Experience Platform内收集和集中来自不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用Flow Service API来浏览第三方数据库的内容和文件结构。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../home.md): Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../sandboxes/home.md): Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和改进数字体验应用程序。

以下各节提供您需要了解的其他信息，以便使用流服务API成功连接到第三方数据库。

### 收集所需的凭据

本教程要求您与要从中获取数据的第三方数据库建立有效连接。 有效连接涉及数据库的连接规范ID和连接ID。 有关创建数据库连接和检索这些值的详细信息，请参阅源连接 [器概述](./../../../home.md#database)。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑 [难解答指南中有关如何阅读示例API调](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用的部分。

### 收集所需标题的值

要调用平台API，您必须先完成身份验证 [教程](../../../../tutorials/authentication.md)。 完成身份验证教程后，将提供所有Experience Platform API调用中每个所需标头的值，如下所示：

* 授权： 承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源（包括属于流服务的资源）都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* 内容类型： `application/json`

## 浏览数据表

使用数据库的连接ID，您可以通过执行GET请求来浏览数据表。 使用以下调用查找要检查或引入平台的表的路径。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 数据库连接的ID。 |

**请求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/54c22133-3a01-4d3b-8221-333a01bd3b03/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会从数据库返回一组表。 查找要引入平台的表并记下其属 `path` 性，因为您需要在下一步中提供它来检查其结构。

```json
[
    {
        "type": "table",
        "name": "test1.Mytable",
        "path": "test1.Mytable",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "test1.austin_demo",
        "path": "test1.austin_demo",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## 检查表的结构

要从查询库检查表的结构，请在指定表的路径作为数据参数时执行GET请求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 数据库连接的ID。 |
| `{TABLE_PATH}` | 表的路径。 |

**请求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/54c22133-3a01-4d3b-8221-333a01bd3b03/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回指定表的结构。 有关每个表列的详细信息位于数组元素 `columns` 中。

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "TestID",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Name",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    }
}
```

## 后续步骤

通过本教程，您探索了数据库，找到了要引入平台的表的路径，并获取了有关其结构的信息。 您可以在下一个教程中使用此信 [息从数据库收集数据并将其引入平台](../collect/database-nosql.md)。
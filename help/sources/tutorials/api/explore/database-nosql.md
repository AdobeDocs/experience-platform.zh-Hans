---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API浏览数据库或NoSQL系统
topic: overview
translation-type: tm+mt
source-git-commit: 4c34ecdaeb4a0df1faf2dd54e8a264b9126f20b4

---


# 使用Flow Service API浏览数据库或NoSQL系统

Flow Service用于收集和集中Adobe Experience Platform内不同来源的客户数据。 该服务提供用户界面和RESTful API，所有支持的源都可从中连接。

本教程使用Flow Service API浏览数据库或NoSQL系统。

## 入门指南

本指南需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../sandboxes/home.md):Experience Platform提供虚拟沙箱，将单个Platform实例分为单独的虚拟环境，以帮助开发和发展数字体验应用程序。

以下各节提供了使用Flow Service API成功连接到数据库或NoSQL系统时需要了解的其他信息。

### 获取基本连接

要使用Platform API浏览数据库或NoSQL系统，您必须拥有有效的基本连接ID。 如果您还没有数据库或要使用的NoSQL系统的基本连接，则可以通过以下教程创建一个：

* [Amazon Redshift](../create/databases/redshift.md)
* [Azure HDInsights上的Apache Spark ](../create/databases/spark.md)
* [Azure Synapse Analytics](../create/databases/synapse-analytics.md)
* [Azure表存储](../create/databases/ats.md)
* [Google BigQuery](../create/databases/bigquery.md)
* [蜂巢](../create/databases/hive.md)
* [MariaDB](../create/databases/mariadb.md)
* [MySQL](../create/databases/mysql.md)
* [凤凰城](../create/databases/phoenix.md)
* [PostgreSQL](../create/databases/postgres.md)
* [SQL Server](../create/databases/sql-server.md)

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

* 授权：承载人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源（包括属于Flow Service的资源）都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的媒体类型标题：

* 内容类型： `application/json`

## 浏览数据表

使用数据库或NoSQL系统的基本连接，您可以通过执行GET请求来浏览数据表。 使用以下调用查找要检查或收录到平台中的表的路径。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 数据库或NoSQL基连接的ID。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/54c22133-3a01-4d3b-8221-333a01bd3b03/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会从数据库或NoSQL系统返回一组表。 查找要引入平台的表并记下其属性，因为您需要在下一 `path` 步中提供它以检查其结构。

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

要从数据库或NoSQL系统检查表的结构，请在将表的路径指定为查询参数时执行GET请求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 数据库或NoSQL基连接的ID。 |
| `{TABLE_PATH}` | 表的路径。 |

**请求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/54c22133-3a01-4d3b-8221-333a01bd3b03/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回指定表的结构。 有关每个表列的详细信息位于数组的元素 `columns` 中。

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

通过本教程，您探索了数据库或NoSQL系统，找到了要收录到平台中的表的路径，并获取了有关其结构的信息。 您可以在下一个教程中使用此信息从 [数据库或NoSQL系统收集数据并将其引入平台](../collect/database-nosql.md)。
---
keywords: Experience Platform；主页；热门主题；第三方数据库；数据库流服务
solution: Experience Platform
title: 使用流服务API浏览数据库
description: 本教程使用流服务API来探索第三方数据库的内容和文件结构。
exl-id: 94935492-a7be-48dc-8089-18476590bf98
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 2%

---

# 使用 [!DNL Flow Service] API

本教程使用 [!DNL Flow Service] 用于探索第三方数据库的内容和文件结构的API。

## 快速入门

本指南要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供分区单个沙箱的虚拟沙箱 [!DNL Platform] 实例迁移到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

以下各节提供了您需要了解的其他信息，以便使用 [!DNL Flow Service] API。

### 收集所需的凭据

本教程要求您与要从中摄取数据的第三方数据库建立有效连接。 有效连接涉及数据库的连接规范ID和连接ID。 有关创建数据库连接和检索这些值的详细信息，请参阅 [源连接器概述](./../../../home.md#database).

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有E[!DNL xperience Platform] API调用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有资源 [!DNL Experience Platform]，包括属于 [!DNL Flow Service]，与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的媒体类型标头：

* `Content-Type: application/json`

## 浏览数据表

使用数据库的连接ID，您可以通过执行GET请求来浏览数据表。 使用以下调用查找要检查或摄取到的表的路径 [!DNL Platform].

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 参数 | 描述 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 数据库源的连接ID。 |

**请求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会从数据库中返回一个表数组。 找你想进去的桌子 [!DNL Platform] 并注意 `path` 资产，因为您需要在下一步中提供该资产以检查其结构。

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

## Inspect表的结构

要从GET库中检查表的结构，请在将表的路径指定为查询参数时执行数据请求。

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
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回指定表的结构。 有关每个表列的详细信息位于 `columns` 数组。

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

通过阅读本教程，您探索了数据库，找到了要摄取到的表的路径 [!DNL Platform]，并获取了有关其结构的信息。 在下一个教程中，您可以在 [从数据库中收集数据并将其导入平台](../collect/database-nosql.md).

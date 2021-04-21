---
keywords: Experience Platform；主页；热门主题；查询服务；api指南；查询;查询;查询服务；
solution: Experience Platform
title: 查询API端点
topic-legacy: queries
description: 以下各节将演练您可以使用查询 Service API中的/查询端点进行的调用。
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 2%

---

# 查询端点

## 示例API调用

以下各节将演练您可以使用[!DNL Query Service] API中的`/queries`端点进行的调用。 每个调用都包括常规API格式、显示所需标头的示例请求和示例响应。

### 检索列表查询

您可以通过向`/queries`端点发出列表请求，检索IMS组织的所有查询的GET。

**API格式**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:(可&#x200B;*选*)添加到配置响应中返回结果的请求路径的参数。可以包含多个参数，用&amp;符号(`&`)分隔。 以下列出了可用参数。

**查询参数**

以下是列出列表的可用查询参数的查询。 所有这些参数都是可选的。 调用此端点时不使用参数将检索组织可用的所有查询。

| 参数 | 描述 |
| --------- | ----------- |
| `orderby` | 指定对结果排序所依据的字段。 支持的字段为`created`和`updated`。 例如，`orderby=created`将按升序创建结果排序。 在创建前添加`-`(`orderby=-created`)将按降序对创建的项目进行排序。 |
| `limit` | 指定页面大小限制以控制页面中包含的结果数。 (*默认值：20*) |
| `start` | 使用从零开始的编号来偏移响应列表。 例如，`start=2`将返回从第三个列出的列表开始的查询。 (*默认值：0*) |
| `property` | 根据字段筛选结果。 过滤器&#x200B;**必须**&#x200B;为HTML转义。 多组过滤器用逗号分隔。 支持的字段有`created`、`updated`、`state`和`id`。 支持的运算符的列表为`>`（大于）、`<`（小于）、`>=`（大于或等于）、`<=`（小于或等于）、`==`（等于）、`!=`（不等于）和`~`（包含）。 例如，`id==6ebd9c2d-494d-425a-aa91-24033f3abeec`将返回具有指定ID的所有查询。 |
| `excludeSoftDeleted` | 指示是否应包括已软删除的查询。 例如，`excludeSoftDeleted=false`将&#x200B;**包括**&#x200B;软删除查询。 (*布尔值，默认值：true*) |
| `excludeHidden` | 指示是否应显示非用户驱动的查询。 将此值设置为false将&#x200B;**包括**&#x200B;非用户驱动查询，如CURSOR定义、FETCH或元数据查询。 (*布尔值，默认值：true*) |

**请求**

以下请求将检索为您的IMS组织创建的最新查询。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态200，并将指定IMS组织的列表查询为JSON。 以下响应返回为您的IMS组织创建的最新查询。

```json
{
    "queries": [
        {
            "isInsertInto": false,
            "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
            "state": "SUCCESS",
            "rowCount": 0,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
            "elapsedTime": 28,
            "updated": "2019-12-06T22:00:17.390Z",
            "client": "Adobe Query Service UI",
            "userId": "{USER_ID}",
            "created": "2019-12-06T22:00:17.362Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "GET"
                },
                "soft_delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/queries/9957bd7f-2244-4fd5-91bc-077d7df1d8e5",
                    "method": "PATCH",
                    "body": "{ \"op\": \"soft_delete\"}"
                },
                "referenced_datasets": [
                    {
                        "id": "5b2bdd32230d4401de87397c",
                        "href": "https://platform.adobe.io/data/foundation/catalog/dataSets/5b2bdd32230d4401de87397c"
                    }
                ]
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-12-06T22:00:17.362Z",
        "next": "2019-08-01T00:14:21.748Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-08-01T00:14:21.748Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries?orderby=-created&start=2019-12-06T22:00:17.362Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

### 创建查询

可以通过向`/queries`端点发出POST请求来创建新查询。

**API格式**

```http
POST /queries
```

**请求**

以下请求将创建一个新查询，由有效负荷中提供的值进行配置：

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query"
        "description": "Sample Description"
    }  
```

| 属性 | 描述 |
| -------- | ----------- |
| `dbName` | 要为其创建SQL查询的数据库的名称。 |
| `sql` | 要创建的SQL查询。 |
| `name` | SQL查询的名称。 |
| `description` | SQL查询的说明。 |

**响应**

成功的响应会返回HTTP状态202（已接受），其中包含您新创建的查询的详细信息。 查询完成激活并成功运行后，`state`将从`SUBMITTED`更改为`SUCCESS`。

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>可以使用`_links.cancel`的值[取消创建的查询](#cancel-a-query)。

### 按ID检索查询

您可以通过向`/queries`端点发出GET请求并在请求路径中提供查询的`id`值来检索有关特定查询的详细信息。

**API格式**

```http
GET /queries/{QUERY_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{QUERY_ID}` | 要检索的查询的`id`值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含有关指定查询的详细信息。

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    },
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "4d64cd49-cf8f-463a-a182-54bccb9954fc",
    "elapsedTime": 0,
    "updated": "2020-01-08T21:47:46.865Z",
    "client": "API",
    "userId": "{USER_ID}",
    "created": "2020-01-08T21:47:46.865Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

>[!NOTE]
>
>可以使用`_links.cancel`的值[取消创建的查询](#cancel-a-query)。

### 取消查询

您可以请求删除指定查询，方法是向`/queries`端点发出PATCH请求，并在请求路径中提供查询的`id`值。

**API格式**

```http
PATCH /queries/{QUERY_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{QUERY_ID}` | 要取消的查询的`id`值。 |


**请求**

此API请求使用JSON修补程序语法来处理其负载。 有关JSON修补程序工作原理的更多信息，请阅读API基础文档。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `op` | 要取消查询，必须使用值`cancel `设置op参数。 |

**响应**

成功的响应返回HTTP状态202（已接受），并显示以下消息：

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```

---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 查询服务开发人员指南
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# 查询

## 示例API调用

以下各节将介绍您可以使用查询服务API `/queries` 中的端点进行的调用。 每个调用包括常规API格式、显示所需标题的示例请求和示例响应。

### 检索一列表查询

您可以通过向端点发出GET请求，检索IMS组织的所有查询的列表 `/queries` 信息。

**API格式**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:(可&#x200B;*选*)添加到请求路径的参数，用于配置在响应中返回的结果。 可以包括多个参数，由&amp;符号(`&`)分隔。 以下列出了可用参数。

**查询参数**

以下是列出列表的可用查询参数查询。 所有这些参数都是可选的。 调用此端点时不带参数将检索组织的所有可用查询。

| 参数 | 描述 |
| --------- | ----------- |
| `orderby` | 指定对结果排序的字段。 支持的字段有 `created` 和 `updated`。 例如，将 `orderby=created` 按创建的升序对结果进行排序。 在创建 `-` 之前(`orderby=-created`)添加项目将按降序排序。 |
| `limit` | 指定页面大小限制，以控制包含在页面中的结果数。 (*Default value: 20*) |
| `start` | 使用从零开始的编号来偏移响应列表。 例如，将 `start=2` 返回一个从列出的第三个列表开始的查询。 (*Default value: 0*) |
| `property` | 根据字段筛选结果。 过滤器 **必须** HTML转义。 逗号用于组合多组过滤器。 支持的字段 `created`有、 `updated`、 `state`和 `id`。 支持的操作符的列表 `>` 为（大于）、 `<` （小于）、 `>=` （大于或等于）、 `<=` （小于或等于）、 `==` （等于）、 `!=` （不等于）和 `~` （包含）。 例如，将 `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` 返回具有指定ID的所有查询。 |
| `excludeSoftDeleted` | 指示是否应包括已软删除的查询。 例如，将包 `excludeSoftDeleted=false` 含 **软删除** 的查询。 (*Boolean，默认值：true*) |
| `excludeHidden` | 指示是否应显示非用户驱动的查询。 将此值设置为false将包 **括非用户驱动的查询** ，如CURSOR定义、FETCH或元数据查询。 (*Boolean，默认值：true*) |

**请求**

以下请求将检索为IMS组织创建的最新查询。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态200，并将指定IMS组织的列表查询为JSON。 以下响应会返回为IMS组织创建的最新查询。

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

您可以通过向端点发出POST请求来创建新查询 `/queries` 。

**API格式**

```http
POST /queries
```

**请求**

以下请求将创建一个新查询，其配置由有效负荷中提供的值进行：

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

成功的响应会返回HTTP状态202（已接受），其中包含您新创建的查询的详细信息。 查询完成激活并成功运行后，该将 `state` 从更改 `SUBMITTED` 为 `SUCCESS`。

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

>[!NOTE] 您可以使用的值取 `_links.cancel` 消 [创建的查询](#cancel-a-query)。

### 按ID检索查询

您可以通过向端点发出GET请求并在请求路径中提供查询值来检索有关 `/queries` 特定查询的 `id` 详细信息。

**API格式**

```http
GET /queries/{QUERY_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{QUERY_ID}` | 要 `id` 检索的查询的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态200，其中包含有关指定查询的详细信息。

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

>[!NOTE] 您可以使用的值取 `_links.cancel` 消 [创建的查询](#cancel-a-query)。

### 取消查询

您可以通过向端点发出PATCH请求并在请求路径中提供查询值来请 `/queries``id` 求删除指定的查询。

**API格式**

```http
PATCH /queries/{QUERY_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{QUERY_ID}` | 要 `id` 取消的查询的值。 |


**请求**

此API请求使用JSON修补程序语法处理其有效负荷。 有关JSON修补程序工作原理的更多信息，请阅读API基础知识文档。

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
| `op` | 要取消查询，必须使用值设置op参数 `cancel `。 |

**响应**

成功的响应会返回HTTP状态202（已接受），并显示以下消息：

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```

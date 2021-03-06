---
keywords: Experience Platform；主页；热门主题；查询服务；API指南；查询；查询；查询服务；
solution: Experience Platform
title: 查询API端点
topic-legacy: queries
description: 以下各节介绍了可以使用查询服务API中的/querys端点进行的调用。
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 2%

---

# 查询端点

## API调用示例

以下部分将介绍您可以使用 `/queries` 的端点 [!DNL Query Service] API。 每个调用都包含常规API格式、显示所需标头的示例请求以及示例响应。

### 检索查询列表

您可以通过向 `/queries` 端点。

**API格式**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:(*可选*)参数已添加到请求路径，用于配置响应中返回的结果。 可以包含多个参数，这些参数之间用与号(`&`)。 以下列出了可用参数。

**查询参数**

以下是用于列出查询的可用查询参数列表。 所有这些参数都是可选的。 对此端点进行无参数调用将检索适用于贵组织的所有查询。

| 参数 | 描述 |
| --------- | ----------- |
| `orderby` | 指定对结果排序所依据的字段。 支持的字段包括 `created` 和 `updated`. 例如， `orderby=created` 将按创建的结果进行升序排序。 添加 `-` 创建之前(`orderby=-created`)将按创建的项目进行降序排序。 |
| `limit` | 指定页面大小限制以控制页面中包含的结果数。 (*默认值：20*) |
| `start` | 使用从零开始的编号来偏移响应列表。 例如， `start=2` 将返回从第三个列出的查询开始的列表。 (*默认值：0*) |
| `property` | 根据字段筛选结果。 过滤器 **必须** HTML转义。 可使用逗号组合多组过滤器。 支持的字段包括 `created`, `updated`, `state`和 `id`. 支持的运算符列表包括 `>` （大于）， `<` （小于）， `>=` （大于或等于）， `<=` （小于或等于）， `==` （等于）， `!=` （不等于）和 `~` （包含）。 例如， `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` 将返回具有指定ID的所有查询。 |
| `excludeSoftDeleted` | 指示是否应包含已软删除的查询。 例如， `excludeSoftDeleted=false` will **包含** 软删除的查询。 (*布尔值，默认值：true*) |
| `excludeHidden` | 指示是否应显示非用户驱动的查询。 将此值设置为false将会 **包含** 非用户驱动的查询，如CURSOR定义、FETCH或元数据查询。 (*布尔值，默认值：true*) |

**请求**

以下请求可检索为IMS组织创建的最新查询。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含指定IMS组织的查询列表(JSON)。 以下响应会返回为IMS组织创建的最新查询。

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

您可以通过向 `/queries` 端点。

**API格式**

```http
POST /queries
```

**请求**

以下请求会创建一个新查询，该查询由有效负载中提供的值配置：

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

| 属性 | 描述 |
| -------- | ----------- |
| `dbName` | 要为其创建SQL查询的数据库的名称。 |
| `sql` | 要创建的SQL查询。 |
| `name` | SQL查询的名称。 |
| `description` | SQL查询的描述。 |

**响应**

成功响应会返回HTTP状态202（已接受），其中包含新创建查询的详细信息。 查询激活完成并成功运行后， `state` 将从 `SUBMITTED` to `SUCCESS`.

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
>您可以使用 `_links.cancel` to [取消创建的查询](#cancel-a-query).

### 按ID检索查询

您可以通过向 `/queries` 端点和提供查询的 `id` 值。

**API格式**

```http
GET /queries/{QUERY_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{QUERY_ID}` | 的 `id` 要检索的查询的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含有关指定查询的详细信息。

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
>您可以使用 `_links.cancel` to [取消创建的查询](#cancel-a-query).

### 取消查询

您可以通过向 `/queries` 端点和提供查询的 `id` 值。

**API格式**

```http
PATCH /queries/{QUERY_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{QUERY_ID}` | 的 `id` 要取消的查询的值。 |


**请求**

此API请求的有效负载使用JSON修补程序语法。 有关JSON修补程序工作方式的更多信息，请阅读API基础知识文档。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json',
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
   "op": "cancel"  
 }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `op` | 要取消查询，必须使用值设置op参数 `cancel `. |

**响应**

成功响应会通过以下消息返回HTTP状态202（已接受）：

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```

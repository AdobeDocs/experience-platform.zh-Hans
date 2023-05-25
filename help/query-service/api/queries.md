---
keywords: Experience Platform；主页；热门主题；查询服务；API指南；查询；查询；查询服务；
solution: Experience Platform
title: 查询API端点
description: 以下部分将指导您使用查询服务API中的/queries端点进行的调用。
exl-id: d6273e82-ce9d-4132-8f2b-f376c6712882
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 2%

---

# 查询端点

## 示例API调用

以下部分将介绍您可以使用进行的调用 `/queries` 中的端点 [!DNL Query Service] API。 每个调用包括常规API格式、显示所需标头的示例请求和示例响应。

### 检索查询列表

您可以通过向以下网站发出GET请求，检索贵组织的所有查询列表： `/queries` 端点。

**API格式**

```http
GET /queries
GET /queries?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`：(*可选*)参数添加到请求路径，用于配置响应中返回的结果。 可以包含多个参数，以&amp;符号(`&`)。 下面列出了可用的参数。

**查询参数**

以下是列出查询的可用查询参数列表。 所有这些参数都是可选的。 在不使用参数的情况下对此端点进行调用将检索对您的组织可用的所有查询。

| 参数 | 描述 |
| --------- | ----------- |
| `orderby` | 指定排序结果所依据的字段。 支持的字段包括 `created` 和 `updated`. 例如， `orderby=created` 将按创建的结果以升序排序。 添加 `-` 创建前(`orderby=-created`)将按创建的对项目进行降序排序。 |
| `limit` | 指定页面大小限制，以控制页面中包含的结果数。 (*默认值：20*) |
| `start` | 使用从零开始的编号来偏移响应列表。 例如， `start=2` 将返回从列出的第三个查询开始的列表。 (*默认值： 0*) |
| `property` | 根据字段筛选结果。 过滤器 **必须** 被HTML逃跑了。 逗号用于组合多组过滤器。 支持的字段包括 `created`， `updated`， `state`、和 `id`. 支持的运算符列表包括 `>` （大于）， `<` （小于）， `>=` （大于或等于）， `<=` （小于或等于）， `==` （等于）， `!=` （不等于），并且 `~` （包含）。 例如， `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` 将返回具有指定ID的所有查询。 |
| `excludeSoftDeleted` | 指示是否应包含已软删除的查询。 例如， `excludeSoftDeleted=false` 将 **include** 软删除的查询。 (*布尔值，默认值： true*) |
| `excludeHidden` | 指示是否应显示非用户驱动的查询。 将此值设置为false将会 **include** 非用户驱动查询，如CURSOR定义、FETCH或元数据查询。 (*布尔值，默认值： true*) |
| `isPrevLink` | 此 `isPrevLink` 查询参数用于分页。 API调用的结果使用它们的 `created` 时间戳和 `orderby` 属性。 导航结果页面时， `isPrevLink` 向后分页时设置为true。 这会反转查询的顺序。 请参阅“下一个”和“上一个”链接作为示例。 |

**请求**

以下请求将检索为您的组织创建的最新查询。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries?limit=1 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含以JSON格式表示的指定组织的查询列表。 以下响应返回为您的组织创建的最新查询。

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

您可以通过向以下对象发出POST请求来创建新查询： `/queries` 端点。

**API格式**

```http
POST /queries
```

**请求**

以下请求使用有效负载中提供的SQL语句创建新查询：

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "queryParameters": {
            user_id : {USER_ID}
            }
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

下面的请求示例使用现有查询模板ID创建新查询。

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/queries \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
        "dbName": "prod:all",
        "templateID": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
        "name": "Sample Query",
        "description": "Sample Description"
    }  
```

| 属性 | 描述 |
| -------- | ----------- |
| `dbName` | 正在为其创建SQL查询的数据库名称。 |
| `sql` | 要创建的SQL查询。 |
| `name` | SQL查询的名称。 |
| `description` | SQL查询的说明。 |
| `queryParameters` | 键值配对，用于替换SQL语句中的任何参数化值。 仅此为必填项 **如果** 您在提供的SQL中使用参数替换。 将不对这些键值对执行任何值类型检查。 |
| `templateId` | 预先存在的查询的唯一标识符。 您可以提供此语句而不是SQL语句。 |
| `insertIntoParameters` | （可选）如果定义了此属性，则此查询将转换为INSERT INTO查询。 |
| `ctasParameters` | （可选）如果定义了此属性，则此查询将转换为CTAS查询。 |

**响应**

成功的响应会返回HTTP状态202（已接受）以及新创建查询的详细信息。 激活完查询并成功运行后， `state` 将更改 `SUBMITTED` 到 `SUCCESS`.

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
>您可以使用 `_links.cancel` 到 [取消您创建的查询](#cancel-a-query).

### 按ID检索查询

您可以通过向以下网站发出GET请求，检索有关特定查询的详细信息： `/queries` 端点并提供查询的 `id` 请求路径中的值。

**API格式**

```http
GET /queries/{QUERY_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{QUERY_ID}` | 此 `id` 要检索的查询的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/queries/4d64cd49-cf8f-463a-a182-54bccb9954fc \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>您可以使用 `_links.cancel` 到 [取消您创建的查询](#cancel-a-query).

### 取消或软删除查询

您可以通过向以下对象发出PATCH请求，请求取消或软删除指定的查询： `/queries` 端点并提供查询的 `id` 请求路径中的值。

**API格式**

```http
PATCH /queries/{QUERY_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{QUERY_ID}` | 此 `id` 要对其执行操作的查询的值。 |


**请求**

此API请求对其有效负载使用JSON修补程序语法。 有关JSON修补程序如何工作的更多信息，请阅读API基础知识文档。

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
| `op` | 要对资源执行的操作的类型。 接受的值包括 `cancel` 和 `soft_delete`. 要取消查询，必须使用值设置op参数 `cancel `. 请注意，软删除操作会阻止在GET请求时返回查询，但不会将其从系统中删除。 |

**响应**

成功的响应返回HTTP状态202 （已接受），并显示以下消息：

```json
{
    "message": "Query cancel request received",
    "statusCode": 202
}
```

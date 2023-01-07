---
keywords: Experience Platform；主页；热门主题；查询服务；查询模板；API指南；模板；查询服务；
solution: Experience Platform
title: 查询模板API端点
description: 本指南详细介绍了您可以使用查询服务API进行的各种查询模板API调用。
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 3%

---

# 查询模板端点

## API调用示例

以下部分介绍了您可以使用 [!DNL Query Service] API。 每个调用都包含常规API格式、显示所需标头的示例请求以及示例响应。

请参阅 [UI查询模板文档](../ui/query-templates.md) 有关通过Experience PlatformUI创建模板的信息。

### 检索查询模板列表

您可以通过向 `/query-templates` 端点。

**API格式**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*可选*)参数已添加到请求路径，用于配置响应中返回的结果。 可以包含多个参数，这些参数之间用与号(`&`)。 以下列出了可用参数。 |

**查询参数**

以下是用于列出查询模板的可用查询参数列表。 所有这些参数都是可选的。 调用此端点时不使用任何参数，将检索适用于贵组织的所有查询模板。

| 参数 | 描述 |
| --------- | ----------- |
| `orderby` | 指定对结果排序所依据的字段。 支持的字段包括 `created` 和 `updated`. 例如， `orderby=created` 将按创建的结果进行升序排序。 添加 `-` 创建之前(`orderby=-created`)将按创建的项目进行降序排序。 |
| `limit` | 指定页面大小限制以控制页面中包含的结果数。 (*默认值：20*) |
| `start` | 使用从零开始的编号来偏移响应列表。 例如， `start=2` 将返回从第三个列出的查询开始的列表。 (*默认值：0*) |
| `property` | 根据字段筛选结果。 过滤器 **必须** HTML转义。 可使用逗号组合多组过滤器。 支持的字段包括 `name` 和 `userId`. 唯一支持的运算符是 `==` （等于）。 例如， `name==my_template` 将返回名为的所有查询模板 `my_template`. |

**请求**

以下请求可检索为IMS组织创建的最新查询模板。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含指定IMS组织的查询模板列表。 以下响应会返回为IMS组织创建的最新查询模板。

```json
{
    "templates": [
        {
            "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n",
            "name": "Test",
            "id": "f7cb5155-29da-4b95-8131-8c5deadfbe7f",
            "updated": "2019-11-21T21:50:01.469Z",
            "userId": "{USER_ID}",
            "created": "2019-11-21T21:50:01.469Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "DELETE"
                },
                "update": {
                    "href": "https://platform.adobe.io/data/foundation/query/query-templates/f7cb5155-29da-4b95-8131-8c5deadfbe7f",
                    "method": "PUT",
                    "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
                }
            }
        }
    ],
    "_page": {
        "orderby": "-created",
        "start": "2019-11-21T21:50:01.469Z",
        "next": "2019-11-21T21:50:01.469Z",
        "count": 1
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates?orderby=-created&start=2019-11-21T21:50:01.469Z&isPrevLink=true"
        }
    },
    "version": 1
}
```

>[!NOTE]
>
>您可以使用 `_links.delete` to [删除查询模板](#delete-a-specified-query-template).

### 创建查询模板

您可以通过向 `/query-templates` 端点。

**API格式**

```http
POST /query-templates
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "sql": "SELECT * FROM accounts;",
        "name": "Sample query template"
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `sql` | 要创建的SQL查询。 |
| `name` | 查询模板的名称。 |

**响应**

成功响应会返回HTTP状态202（已接受），其中包含新创建查询模板的详细信息。

```json
{
    "sql": "SELECT * FROM accounts;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>您可以使用 `_links.delete` to [删除查询模板](#delete-a-specified-query-template).

### 检索指定的查询模板

您可以通过向 `/query-templates/{TEMPLATE_ID}` 端点和在请求路径中提供查询模板的ID。

**API格式**

```http
GET /query-templates/{TEMPLATE_ID}
```

| 属性 | 描述 |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | 的 `id` 要检索的查询模板的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含您指定查询模板的详细信息。

```json
{
    "sql": "SELECT * FROM accounts;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:20:09.670Z",
    "userId": "A5A562D15E1645480A495CE1@techacct.adobe.com",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>您可以使用 `_links.delete` to [删除查询模板](#delete-a-specified-query-template).

### 更新指定的查询模板

您可以通过向 `/query-templates/{TEMPLATE_ID}` 端点和在请求路径中提供查询模板的ID。

**API格式**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 的 `id` 要检索的查询模板的值。 |

**请求**

>[!NOTE]
>
>PUT请求需要填写sql和name字段，并将 **覆盖** 查询模板的当前内容。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template"
 }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `sql` | 要更新的SQL查询。 |
| `name` | 计划查询的名称。 |

**响应**

成功响应会返回HTTP状态202（已接受），其中包含您指定查询模板的更新信息。

```json
{
    "sql": "SELECT * FROM accounts LIMIT 20;",
    "name": "Sample query template",
    "id": "0094d000-9062-4e6a-8fdb-05606805f08f",
    "updated": "2020-01-09T00:29:20.028Z",
    "lastUpdatedBy": "{USER_ID}",
    "userId": "{USER_ID}",
    "created": "2020-01-09T00:20:09.670Z",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "DELETE"
        },
        "update": {
            "href": "https://platform.adobe.io/data/foundation/query/query_templates/0094d000-9062-4e6a-8fdb-05606805f08f",
            "method": "PUT",
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>您可以使用 `_links.delete` to [删除查询模板](#delete-a-specified-query-template).

### 删除指定的查询模板

您可以通过向 `/query-templates/{TEMPLATE_ID}` 和在请求路径中提供查询模板的ID。

**API格式**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 的 `id` 要检索的查询模板的值。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会通过以下消息返回HTTP状态202（已接受）。

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```

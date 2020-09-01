---
keywords: Experience Platform;home;popular topics;query service;query templates;api guide;templates;Query service;
solution: Experience Platform
title: 查询服务开发人员指南
topic: query templates
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 3%

---


# 查询模板

## 示例API调用

现在，您已经了解要使用哪些标头，便可开始调用 [!DNL Query Service] API。 以下各节将介绍您可以使用API进行的各种API [!DNL Query Service] 调用。 每个调用都包括常规API格式、显示所需标头的示例请求和示例响应。

### 检索列表查询模板

您可以通过向端点发出列表请求，为IMS组织检索所有查询模板的GET `/query-templates` 符。

**API格式**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (可&#x200B;*选*)添加到请求路径的参数，这些参数配置在响应中返回的结果。 可以包括多个参数，用和号(`&`)分隔。 以下列出了可用参数。 |

**查询参数**

以下是列出列表模板的可用查询参数的查询。 所有这些参数都是可选的。 调用此端点时，无参数将检索组织可用的所有查询模板。

| 参数 | 描述 |
| --------- | ----------- |
| `orderby` | 指定对结果进行排序的字段。 支持的字段 `created` 有 `updated`。 例如，将 `orderby=created` 按创建的升序对结果进行排序。 添加创 `-` 建前(`orderby=-created`)将按降序创建项排序。 |
| `limit` | 指定页面大小限制以控制页面中包含的结果数。 (*Default value: 20*) |
| `start` | 使用从零开始的编号，偏移响应列表。 例如，将 `start=2` 返回从第三个列出的列表开始的查询。 (*Default value: 0*) |
| `property` | 根据字段筛选结果。 过滤器 **必须** 为HTML转义。 逗号用于组合多组过滤器。 支持的字段 `name` 有 `userId`。 唯一支持的运 `==` 算符是（等于）。 例如，将 `name==my_template` 返回所有具有该名称的查询模 `my_template`板。 |

**请求**

以下请求将检索为您的IMS组织创建的最新查询模板。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，具有指定IMS组织的列表查询模板。 以下响应会返回为您的IMS组织创建的最新查询模板。

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
                    "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
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
>您可以使用的值删 `_links.delete` 除 [查询模板](#delete-a-specified-query-template)。

### 创建查询模板

您可以通过向端点发出查询请求来创建POST `/query-templates` 模板。

**API格式**

```http
POST /query-templates
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/query-templates
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的响应会返回HTTP状态202（已接受），其中包含新创建的查询模板的详细信息。

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
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>您可以使用的值删 `_links.delete` 除 [查询模板](#delete-a-specified-query-template)。

### 检索指定的查询模板

您可以通过向端点发出查询请求并在请求路径 `/query-templates/{TEMPLATE_ID}` 中提供GET模板的ID来检索特定的查询模板。

**API格式**

```http
GET /query-templates/{TEMPLATE_ID}
```

| 属性 | 描述 |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | 要 `id` 检索的查询模板的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态200，其中包含您指定的查询模板的详细信息。

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
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>您可以使用的值删 `_links.delete` 除 [查询模板](#delete-a-specified-query-template)。

### 更新指定的查询模板

您可以通过向端点发出查询请求并在请求路径 `/query-templates/{TEMPLATE_ID}` 中提供PUT模板的ID来更新特定的查询模板。

**API格式**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 要 `id` 检索的查询模板的值。 |

**请求**

>[!NOTE]
>
>PUT请求需要填写sql和name字段，并将覆 **盖** 该查询模板的当前内容。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的响应会返回HTTP状态202（已接受），其中包含指定查询模板的更新信息。

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
            "body": "{\"sql\" : \"new sql \", \"name\" : \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>您可以使用的值删 `_links.delete` 除 [查询模板](#delete-a-specified-query-template)。

### 删除指定的查询模板

您可以通过向查询请求并在请求路径中提 `/query-templates/{TEMPLATE_ID}` 供DELETE模板的ID来删除特定的查询模板。

**API格式**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 要 `id` 检索的查询模板的值。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态202（已接受），并显示以下消息。

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```

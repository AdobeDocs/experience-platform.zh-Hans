---
keywords: Experience Platform；主页；热门主题；查询服务；查询模板；API指南；模板；查询服务；
solution: Experience Platform
title: 查询模板API端点
description: 本指南详细说明您可以使用查询服务API进行的各种查询模板API调用。
exl-id: 14cd7907-73d2-478f-8992-da3bdf08eacc
source-git-commit: 958d5c322ff26f7372f8ab694a70ac491cbff56c
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 2%

---

# 查询模板端点

## 示例API调用

以下部分介绍了您可以使用进行的各种API调用。 [!DNL Query Service] API。 每个调用包括常规API格式、显示所需标头的示例请求以及示例响应。

请参阅 [UI查询模板文档](../ui/query-templates.md) 有关通过Experience PlatformUI创建模板的信息。

### 检索查询模板列表

您可以通过向以下网站发出GET请求，检索贵组织的所有查询模板列表： `/query-templates` 端点。

**API格式**

```http
GET /query-templates
GET /query-templates?{QUERY_PARAMETERS}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*可选*)参数添加到请求路径，用于配置响应中返回的结果。 可以包含多个参数，以&amp;分隔(`&`)。 下面列出了可用的参数。 |

**查询参数**

以下是列出查询模板的可用查询参数列表。 所有这些参数都是可选的。 在不使用参数的情况下对此端点进行调用将检索对您的组织可用的所有查询模板。

| 参数 | 描述 |
| --------- | ----------- |
| `orderby` | 指定排序结果所依据的字段。 支持的字段包括 `created` 和 `updated`. 例如， `orderby=created` 将按创建的内容对结果进行升序排序。 添加 `-` 创建前(`orderby=-created`)将按创建的项以降序对项排序。 |
| `limit` | 指定页大小限制，以控制页中包含的结果数。 (*默认值：20*) |
| `start` | 指定ISO格式时间戳对结果进行排序。 如果未指定开始日期，则API调用将首先返回最早创建的模板，然后继续列出更新的结果。<br> ISO时间戳允许在日期和时间实现不同级别的粒度。 基本ISO时间戳采用以下格式： `2020-09-07` 表示日期为2020年9月7日。 一个更复杂的示例可以编写为 `2022-11-05T08:15:30-05:00` 和对应于2022年11月5日， 8:15:上午30:00，美国东部标准时间。 可以为时区提供UTC偏移，并在后缀“Z”中表示(`2020-01-01T01:01:01Z`)。 如果未提供时区，则默认设置为0。 |
| `property` | 根据字段筛选结果。 过滤器 **必须** HTML逃跑了。 逗号用于组合多组过滤器。 支持的字段包括 `name` 和 `userId`. 唯一支持的运算符是 `==` （等于）。 例如， `name==my_template` 将返回名称为的所有查询模板 `my_template`. |

**请求**

以下请求将检索为您的组织创建的最新查询模板。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含指定组织的查询模板列表。 以下响应会返回为您的组织创建的最新查询模板。

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
>您可以使用值 `_links.delete` 到 [删除您的查询模板](#delete-a-specified-query-template).

### 创建查询模板

您可以通过向以下对象发出POST请求来创建查询模板 `/query-templates` 端点。

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
        "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
        "name": "Sample query template",
        "queryParameters": {
            user_id : {USER_ID}
            }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `sql` | 要创建的SQL查询。 您可以使用标准SQL或参数替换。 要在SQL中使用参数替换，必须在参数键前面加上 `$`. 例如， `$key`，并提供SQL中使用的参数作为 `queryParameters` 字段。 此处传递的值将是模板中使用的默认参数。 如果要覆盖这些参数，必须在POST请求中覆盖它们。 |
| `name` | 查询模板的名称。 |
| `queryParameters` | 键值配对，用于替换SQL语句中的任何参数化值。 仅此为必填项 **如果** 您在提供的SQL中使用参数替换。 将不对这些键值对执行任何值类型检查。 |

**响应**

成功的响应返回HTTP状态202（已接受）以及新创建的查询模板的详细信息。

```json
{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
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
>您可以使用值 `_links.delete` 到 [删除您的查询模板](#delete-a-specified-query-template).

### 检索指定的查询模板

您可以通过对以下对象发出GET请求，检索特定的查询模板： `/query-templates/{TEMPLATE_ID}` 端点并在请求路径中提供查询模板的ID。

**API格式**

```http
GET /query-templates/{TEMPLATE_ID}
```

| 属性 | 描述 |
| -------- | ----------- | 
| `{TEMPLATE_ID}` | 此 `id` 要检索的查询模板的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200以及指定查询模板的详细信息。

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
>您可以使用值 `_links.delete` 到 [删除您的查询模板](#delete-a-specified-query-template).

### 更新指定的查询模板

您可以通过向以下对象发出PUT请求来更新特定的查询模板： `/query-templates/{TEMPLATE_ID}` 端点并在请求路径中提供查询模板的ID。

**API格式**

```http
PUT /query-templates/{TEMPLATE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 此 `id` 要检索的查询模板的值。 |

**请求**

>[!NOTE]
>
>PUT请求要求同时填写sql和name字段，并且将 **覆盖** 该查询模板的当前内容。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "sql": "SELECT account_balance FROM user_data WHERE user_id='$user_id';",
    "name": "Sample query template",
    "queryParameters": {
            user_id : {USER_ID}
        }
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `sql` | 要创建的SQL查询。 您可以使用标准SQL或参数替换。 要在SQL中使用参数替换，必须在参数键前面加上 `$`. 例如， `$key`，并提供SQL中使用的参数作为 `queryParameters` 字段。 此处传递的值将是模板中使用的默认参数。 如果要覆盖这些参数，必须在POST请求中覆盖它们。 |
| `name` | 查询模板的名称。 |
| `queryParameters` | 键值配对，用于替换SQL语句中的任何参数化值。 仅此为必填项 **如果** 您在提供的SQL中使用参数替换。 将不对这些键值对执行任何值类型检查。 |

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
            "body": "{\"sql\": \"new sql \", \"name\": \"new name\"}"
        }
    }
}
```

>[!NOTE]
>
>您可以使用值 `_links.delete` 到 [删除您的查询模板](#delete-a-specified-query-template).

### 删除指定的查询模板

您可以通过对以下对象发出DELETE请求，删除特定的查询模板： `/query-templates/{TEMPLATE_ID}` 并在请求路径中提供查询模板的ID。

**API格式**

```http
DELETE /query-templates/{TEMPLATE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{TEMPLATE_ID}` | 此 `id` 要检索的查询模板的值。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/query-templates/0094d000-9062-4e6a-8fdb-05606805f08f
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态202（已接受），并显示以下消息。

```json
{
    "message": "Deleted",
    "statusCode": 202
}
```

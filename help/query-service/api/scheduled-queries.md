---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 查询服务开发人员指南
topic: scheduled queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# 计划查询

## 示例API调用

既然您了解了要使用哪些标头，就可以开始调用查询服务API了。 以下各节将介绍您可以使用查询服务API进行的各种API调用。 每个调用包括常规API格式、显示所需标题的示例请求和示例响应。

### 检索计划列表

您可以通过向端点发出GET请求，检索IMS组织的所有计划列表的查询 `/schedules` 信息。

**API格式**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (可&#x200B;*选*)添加到请求路径的参数，用于配置在响应中返回的结果。 可以包括多个参数，由&amp;符号(`&`)分隔。 以下列出了可用参数。 |

**查询参数**

以下是列出计划查询的可用查询参数列表。 所有这些参数都是可选的。 调用不带参数的此端点将检索组织可用的所有计划查询。

| 参数 | 描述 |
| --------- | ----------- |
| `orderby` | 指定对结果排序的字段。 支持的字段有 `created` 和 `updated`。 例如，将 `orderby=created` 按创建的升序对结果进行排序。 在创建 `-` 之前(`orderby=-created`)添加项目将按降序排序。 |
| `limit` | 指定页面大小限制，以控制包含在页面中的结果数。 (*Default value: 20*) |
| `start` | 使用从零开始的编号来偏移响应列表。 例如，将 `start=2` 返回一个从列出的第三个列表开始的查询。 (*Default value: 0*) |
| `property` | 根据字段筛选结果。 过滤器 **必须** HTML转义。 逗号用于组合多组过滤器。 支持的字段 `created`有、 `templateId`和 `userId`。 支持的操作符的列表 `>` 为（大于）、 `<` （小于）和 `==` （等于）。 例如，将 `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` 返回用户ID如指定的所有计划查询。 |

**请求**

以下请求将检索为IMS组织创建的最新计划查询。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态200，并且列表指定IMS组织的预定查询。 以下响应会返回为IMS组织创建的最新计划查询。

```json
{
    "schedules": [
        {
            "state": "ENABLED",
            "query": {
                "dbName": "prod:all",
                "sql": "SELECT * FROM accounts;",
                "name": "Sample Scheduled Query",
                "description": "A sample of a scheduled query."
            },
            "updatedUserId": "{USER_ID}",
            "version": 2,
            "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "updated": "1578523458919",
            "schedule": {
                "schedule": "30 * * * *",
                "startDate": "2020-01-08T12:30:00.000Z",
                "maxActiveRuns": 1
            },
            "userId": "{USER_ID}",
            "created": "1578523458919",
            "_links": {
                "enable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"enable\" }"
                },
                "runs": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "GET"
                },
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "DELETE"
                },
                "disable": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
                    "method": "PATCH",
                    "body": "{ \"op\": \"disable\" }"
                },
                "trigger": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
                    "method": "POST"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T22:44:18.919Z",
        "count": 1
    },
    "_links": {},
    "version": 2
}
```

### 创建新的计划查询

您可以通过向端点发出POST请求来创建新的计划查询 `/schedules` 。

**API格式**

```http
POST /schedules
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "query": {
         "dbName": "prod:all",
         "sql": "SELECT * FROM accounts;",
         "name": "Sample Scheduled Query",
         "description": "A sample of a scheduled query."
     }, 
     "schedule": {
         "schedule": "30 * * * *",
         "startDate": "2020-01-08T12:30:00.000Z"
     }
 }
 '
```

| 属性 | 描述 |
| -------- | ----------- |
| `query.dbName` | 要为其创建计划查询的数据库的名称。 |
| `query.sql` | 要创建的SQL查询。 |
| `query.name` | 计划查询的名称。 |
| `schedule.schedule` | 查询的计划。 有关cron计划的更多信息，请阅读 [cron表达式格式文档](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 。 在此示例中，“30 * * * * *”表示查询将在30分钟标记下每小时运行一次。 |
| `schedule.startDate` | 计划查询的开始日期，以UTC时间戳写入。 |

**响应**

成功的响应会返回HTTP状态202（已接受），其中包含您新创建的计划查询的详细信息。 计划查询完成激活后，将 `state` 从更改 `REGISTERING` 为 `ENABLED`。

```json
{
    "state": "REGISTERING",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE] 您可以使用的值删 `_links.delete` 除已 [创建的计划查询](#delete-a-specified-scheduled-query)。

### 请求指定计划查询的详细信息

您可以通过向端点发出GET请求并在请求路径中提供其ID来检索特定计 `/schedules` 划查询的信息。

**API格式**

```http
GET /schedules/{SCHEDULE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 要 `id` 检索的计划查询的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态200，其中包含指定计划查询的详细信息。

```json
{
    "state": "ENABLED",
    "query": {
        "dbName": "prod:all",
        "sql": "SELECT * FROM accounts;",
        "name": "Sample Scheduled Query",
        "description": "A sample of a scheduled query."
    },
    "updatedUserId": "{USER_ID}",
    "version": 2,
    "id": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "updated": "1578523458919",
    "schedule": {
        "schedule": "30 * * * *",
        "startDate": "2020-01-08T12:30:00.000Z",
        "maxActiveRuns": 1
    },
    "userId": "{USER_ID}",
    "created": "1578523458919",
    "_links": {
        "enable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"enable\" }"
        },
        "runs": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "GET"
        },
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "DELETE"
        },
        "disable": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
            "method": "PATCH",
            "body": "{ \"op\": \"disable\" }"
        },
        "trigger": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs",
            "method": "POST"
        }
    }
}
```

>[!NOTE] 您可以使用的值删 `_links.delete` 除已 [创建的计划查询](#delete-a-specified-scheduled-query)。

### 更新指定计划查询的详细信息

您可以通过向端点发出PATCH请求并在请求路径中提供其ID来更新指定计划查询的 `/schedules` 详细信息。

PATCH请求支持两种不同的路径： `/state` 和 `/schedule/schedule`。

### 更新计划的查询状态

您可以使 `/state` 用来更新选定计划查询的状态-“已启用”或“已禁用”。 要更新状态，您需要将值设置为 `enable` 或 `disable`。

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 要 `id` 检索的计划查询的值。 |


**请求**

此API请求使用JSON修补程序语法处理其有效负荷。 有关JSON修补程序工作原理的更多信息，请阅读API基础知识文档。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/state",
             "value": "disable"
         }
     ]
 }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `path` | 要修补的值的路径。 在这种情况下，由于您要更新计划的查询状态，因此需要将值设置为 `path``/state`。 |
| `value` | 的更新值 `/state`。 此值可以设置为，也 `enable` 可以 `disable` 启用或禁用计划的查询。 |

**响应**

成功的响应会返回HTTP状态202（已接受），并显示以下消息。

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 更新计划的查询计划

您可以使用 `/schedule/schedule` 更新计划查询的cron计划。 有关cron计划的更多信息，请阅读 [cron表达式格式文档](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 。

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 要 `id` 检索的计划查询的值。 |

**请求**

此API请求使用JSON修补程序语法处理其有效负荷。 有关JSON修补程序工作原理的更多信息，请阅读API基础知识文档。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "body": [
         {
             "op": "replace",
             "path": "/schedule/schedule",
             "value": "45 * * * *"
         }
     ]
 }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `path` | 要修补的值的路径。 在这种情况下，由于您要更新计划查询的计划，因此需要将值设置为 `path``/schedule/schedule`。 |
| `value` | 的更新值 `/schedule`。 此值必须为cron计划形式。 因此，在本例中，计划的查询将在每小时45分钟时运行。 |

**响应**

成功的响应会返回HTTP状态202（已接受），并显示以下消息。

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 删除指定的计划查询

可以通过向端点发出DELETE请求并在请求路径中提供要删除的计划查询的ID来删除指定的计划查询。 `/schedules`

>[!NOTE] 计划 **必须先禁用** ，然后才能删除。

**API格式**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 要 `id` 检索的计划查询的值。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态202（已接受），并显示以下消息。

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```

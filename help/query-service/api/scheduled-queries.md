---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；计划查询；计划查询；
solution: Experience Platform
title: 计划端点
description: 以下部分介绍了您可以使用查询服务API对计划查询进行的各种API调用。
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 2%

---

# 计划端点

## 示例API调用

现在您了解了要使用哪些标头，就可以开始调用 [!DNL Query Service] API。 以下部分介绍了您可以使用进行的各种API调用 [!DNL Query Service] API。 每个调用包括常规API格式、显示所需标头的示例请求和示例响应。

### 检索计划查询的列表

您可以通过向以下网站发出GET请求，检索贵组织所有计划查询的列表 `/schedules` 端点。

**API格式**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | (*可选*)参数添加到请求路径，用于配置响应中返回的结果。 可以包含多个参数，以&amp;符号(`&`)。 下面列出了可用的参数。 |

**查询参数**

以下是列出计划查询的可用查询参数列表。 所有这些参数都是可选的。 在不使用参数的情况下对此端点进行调用将检索对您的组织可用的所有计划查询。

| 参数 | 描述 |
| --------- | ----------- |
| `orderby` | 指定排序结果所依据的字段。 支持的字段包括 `created` 和 `updated`. 例如， `orderby=created` 将按创建的结果以升序排序。 添加 `-` 创建前(`orderby=-created`)将按创建的项以降序对项排序。 |
| `limit` | 指定页面大小限制，以控制页面中包含的结果数。 (*默认值：20*) |
| `start` | 使用从零开始的编号来偏移响应列表。 例如， `start=2` 将返回从列出的第三个查询开始的列表。 (*默认值： 0*) |
| `property` | 根据字段筛选结果。 过滤器 **必须** 被HTML逃跑了。 逗号用于组合多组过滤器。 支持的字段包括 `created`， `templateId`、和 `userId`. 支持的运算符列表包括 `>` （大于）， `<` （小于），以及 `==` （等于）。 例如， `userId==6ebd9c2d-494d-425a-aa91-24033f3abeec` 将返回用户ID为指定的所有计划查询。 |

**请求**

以下请求将检索为您的组织创建的最新计划查询。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含指定组织的计划查询列表。 以下响应返回为您的组织创建的最新计划查询。

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

您可以通过向以下对象发出POST请求来创建新的计划查询： `/schedules` 端点。 在API中创建计划查询时，您还可以在查询编辑器中看到它。 有关UI中计划查询的更多信息，请阅读 [查询编辑器文档](../ui/user-guide.md#scheduled-queries).

**API格式**

```http
POST /schedules
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `query.dbName` | 正在为其创建计划查询的数据库名称。 |
| `query.sql` | 要创建的SQL查询。 |
| `query.name` | 计划查询的名称。 |
| `schedule.schedule` | 查询的cron计划。 欲知cron计划的详情，请阅读 [cron表达式格式](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 文档。 在此示例中，“30 * * *”表示查询将每小时运行一次，时间为30分钟。<br><br>或者，您可以使用以下简写表达式：<ul><li>`@once`：查询只运行一次。</li><li>`@hourly`：查询每小时的开头运行一次。 这相当于cron表达式 `0 * * * *`.</li><li>`@daily`：查询每天午夜运行一次。 这相当于cron表达式 `0 0 * * *`.</li><li>`@weekly`：查询每周运行一次，于星期日、午夜运行。 这相当于cron表达式 `0 0 * * 0`.</li><li>`@monthly`：查询每月运行一次，于每月的第一天午夜运行。 这相当于cron表达式 `0 0 1 * *`.</li><li>`@yearly`：查询每年运行一次，于1月1日午夜。 这相当于cron表达式 `1 0 0 1 1 *`. |
| `schedule.startDate` | 计划查询的开始日期，作为UTC时间戳写入。 |

**响应**

成功的响应会返回HTTP状态202（已接受）以及新创建的计划查询的详细信息。 激活完计划的查询后， `state` 将更改 `REGISTERING` 到 `ENABLED`.

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

>[!NOTE]
>
>您可以使用 `_links.delete` 到 [删除您创建的计划查询](#delete-a-specified-scheduled-query).

### 指定计划查询的请求详细信息

您可以通过对以下网站发出GET请求，检索特定计划查询的信息： `/schedules` 端点并在请求路径中提供其ID。

**API格式**

```http
GET /schedules/{SCHEDULE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要检索的计划查询的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200以及指定的计划查询的详细信息。

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

>[!NOTE]
>
>您可以使用 `_links.delete` 到 [删除您创建的计划查询](#delete-a-specified-scheduled-query).

### 更新指定计划查询的详细信息

您可以通过向以下对象发出PATCH请求来更新指定计划查询的详细信息： `/schedules` 端点并在请求路径中提供其ID。

PATCH请求支持两种不同的路径： `/state` 和 `/schedule/schedule`.

### 更新计划的查询状态

您可以通过设置 `path` 属性至 `/state` 和 `value` 属性，作为 `enable` 或 `disable`.

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要PATCH的计划查询的值。 |


**请求**

此API请求对其有效负载使用JSON修补程序语法。 有关JSON修补程序如何工作的更多信息，请阅读API基础知识文档。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | 要对查询计划执行的操作。 接受的值为 `replace`. |
| `path` | 要修补的值的路径。 在这种情况下，由于您正在更新计划查询的状态，因此您需要将值设置为 `path` 到 `/state`. |
| `value` | 的更新值 `/state`. 此值可以设置为 `enable` 或 `disable` 启用或禁用计划查询。 |

**响应**

成功的响应返回HTTP状态202（已接受），并显示以下消息。

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 更新计划的查询计划

您可以通过设置 `path` 属性至 `/schedule/schedule` 在请求正文中。 欲知cron计划的详情，请阅读 [cron表达式格式](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 文档。

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要PATCH的计划查询的值。 |

**请求**

此API请求对其有效负载使用JSON修补程序语法。 有关JSON修补程序如何工作的更多信息，请阅读API基础知识文档。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | 要对查询计划执行的操作。 接受的值为 `replace`. |
| `path` | 要修补的值的路径。 在这种情况下，由于您正在更新计划查询的计划，因此您需要将值设置为 `path` 到 `/schedule/schedule`. |
| `value` | 的更新值 `/schedule`. 该值需要采用cron计划的形式。 因此，在此示例中，计划查询将每小时运行一次，时间为45分钟。 |

**响应**

成功的响应返回HTTP状态202（已接受），并显示以下消息。

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 删除指定的计划查询

您可以通过向以下对象发出DELETE请求来删除指定的计划查询： `/schedules` 端点并在请求路径中提供要删除的计划查询的ID。

>[!NOTE]
>
>计划 **必须** 被删除之前被禁用。

**API格式**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要DELETE的计划查询的值。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态202（已接受），并显示以下消息。

```json
{
    "message": "Schedule deleted successfully",
    "statusCode": 202
}
```

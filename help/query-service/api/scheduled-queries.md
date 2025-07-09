---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；计划查询；计划查询；
solution: Experience Platform
title: 计划端点
description: 以下部分介绍了您可以使用查询服务API对计划查询进行的各种API调用。
role: Developer
exl-id: f57dbda5-da50-4812-a924-c8571349f1cd
source-git-commit: 10c0c5c639226879b1ca25391fc4a1006cf40003
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 2%

---

# 计划端点

了解如何使用查询服务计划API（包含详细信息和示例）以编程方式创建、管理和监视计划查询。

## 要求和先决条件

您可以使用技术帐户（通过OAuth服务器到服务器凭据进行身份验证）或个人用户帐户（用户令牌）创建计划查询。 但是，Adobe强烈建议使用技术帐户来确保计划查询的不中断、安全执行 — 尤其是对于长期或生产工作负载。

如果撤销个人用户帐户的访问权限或禁用其帐户，则使用个人用户帐户创建的查询将失败。 技术帐户提供了更好的稳定性，因为它们与单个用户的就业状况或访问权限无关。

>[!IMPORTANT]
>
>管理计划查询时的重要注意事项：<ul><li>如果用于创建计划的查询的帐户（技术或用户）失去访问权限或权限，计划的查询将失败。</li><li>在通过API或UI删除之前，必须禁用计划查询。</li><li>不支持无限期计划而不设置结束日期；必须始终指定结束日期。</li></ul>

有关帐户要求、权限设置和管理计划查询的详细指导，请参阅[查询计划文档](../ui/query-schedules.md#technical-account-user-requirements)。 有关创建和配置技术帐户的逐步说明，请参阅[Developer Console设置](https://experienceleague.adobe.com/en/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/set-up-developer-console-and-postman)和[端到端技术帐户设置](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/setup)。

## 示例API调用

配置必要的身份验证标头（请参阅[API身份验证指南](../../landing/api-authentication.md)）后，即可开始调用[!DNL Query Service] API。 以下部分演示了各种具有通用格式的API调用，例如请求（包括所需的标头）和示例响应。

### 检索计划查询的列表

您可以通过向`/schedules`端点发出GET请求来检索贵组织的所有计划查询列表。

**API格式**

```http
GET /schedules
GET /schedules?{QUERY_PARAMETERS}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{QUERY_PARAMETERS}` | （*可选*）添加到请求路径的参数，用于配置响应中返回的结果。 可以包含多个参数，以&amp;符号(`&`)分隔。 下面列出了可用的参数。 |

**查询参数**

以下是列出计划查询的可用查询参数列表。 所有这些参数都是可选的。 在不使用参数的情况下调用此端点将检索对您的组织可用的所有计划查询。

| 参数 | 描述 |
| --------- | ----------- |
| `orderby` | 指定排序结果所依据的字段。 支持的字段为`created`和`updated`。 例如，`orderby=created`将按创建的结果以升序排序。 在创建之前(`-`)添加`orderby=-created`将按创建的顺序降序对项进行排序。 |
| `limit` | 指定页大小限制，以控制页中包含的结果数。 （*默认值： 20*） |
| `start` | 指定ISO格式时间戳对结果进行排序。 如果未指定开始日期，则API调用将首先返回创建的最旧的计划查询，然后继续列出更新的结果。<br>个ISO时间戳允许在日期和时间使用不同级别的粒度。 基本ISO时间戳采用`2020-09-07`格式，表示日期2020年9月7日。 一个更复杂的示例将编写为`2022-11-05T08:15:30-05:00`，对应于2022年11月5日美国东部标准时间上午8:15:30。 可以为时区提供UTC偏移量，时区由后缀“Z”(`2020-01-01T01:01:01Z`)表示。 如果未提供时区，则默认设置为0。 |
| `property` | 根据字段筛选结果。 筛选器&#x200B;**必须**&#x200B;对HTML进行转义。 逗号用于组合多组过滤器。 支持的字段为`created`、`templateId`和`userId`。 支持的运算符列表为`>` （大于）、`<` （小于）和`==` （等于）。 例如，`userId==6ebd9c2d-494d-425a-aa91-24033f3abeec`将返回用户ID为指定的所有计划查询。 |

**请求**

以下请求检索为您的组织创建的最新计划查询。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules?limit=1
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含指定组织的已计划查询列表。 以下响应返回为您的组织创建的最新计划查询。

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

您可以通过向`/schedules`端点发出POST请求来创建新的计划查询。 在API中创建计划查询时，您还可以在查询编辑器中看到它。 有关UI中计划查询的更多信息，请阅读[查询编辑器文档](../ui/user-guide.md#scheduled-queries)。

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
| `query.dbName` | 运行计划查询的数据库的名称。 |
| `query.sql` | 要按定义的计划执行的SQL查询。 |
| `query.name` | 计划查询的名称。 |
| `query.description` | 计划查询的可选描述。 |
| `schedule.schedule` | 查询的cron计划。 请参阅[Crontab.guru](https://crontab.guru/)以交互方式创建、验证和了解cron表达式。 在此示例中，“30 * * * *”表示查询将每小时在30分钟标记处运行。<br><br>或者，您可以使用以下简写表达式：<ul><li>`@once`：查询只运行一次。</li><li>`@hourly`：查询每小时在一小时的开头运行一次。 这相当于cron表达式`0 * * * *`。</li><li>`@daily`：查询每天午夜运行一次。 这相当于cron表达式`0 0 * * *`。</li><li>`@weekly`：查询每周运行一次，于星期日、午夜运行。 这相当于cron表达式`0 0 * * 0`。</li><li>`@monthly`：查询每月运行一次，在每月的第一天午夜运行。 这相当于cron表达式`0 0 1 * *`。</li><li>`@yearly`：查询每年运行一次，于1月1日午夜。 这相当于cron表达式`0 0 1 1 *`。 |
| `schedule.startDate` | 以UTC时间戳写入的计划查询开始日期。 |

**响应**

成功的响应返回HTTP状态202（已接受）以及新创建的计划查询的详细信息。 计划查询激活完成后，`state`将从`REGISTERING`更改为`ENABLED`。

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
>您可以使用`_links.delete`的值[删除您创建的计划查询](#delete-a-specified-scheduled-query)。

### 指定计划查询的请求详细信息

您可以通过向`/schedules`端点发出GET请求并在请求路径中提供其ID，来检索特定计划查询的信息。

**API格式**

```http
GET /schedules/{SCHEDULE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 要检索的计划查询的`id`值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含指定计划查询的详细信息。

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
>您可以使用`_links.delete`的值[删除您创建的计划查询](#delete-a-specified-scheduled-query)。

### 更新指定计划查询的详细信息

您可以通过向`/schedules`端点发出PATCH请求并在请求路径中提供其ID，来更新指定计划查询的详细信息。

PATCH请求支持两个不同的路径：`/state`和`/schedule/schedule`。

### 更新计划的查询状态

通过将`path`属性设置为`/state`并将`value`属性设置为`enable`或`disable`，可以更新所选计划查询的状态。

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 您希望PATCH的计划查询的`id`值。 |


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
| `op` | 要对查询计划执行的操作。 接受的值为`replace`。 |
| `path` | 要修补的值的路径。 在这种情况下，由于您正在更新计划查询的状态，因此您需要将`path`的值设置为`/state`。 |
| `value` | `/state`的更新值。 此值可设置为`enable`或`disable`以启用或禁用计划的查询。 |

**响应**

成功的响应返回HTTP状态202（已接受），并显示以下消息。

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 更新计划的查询计划

通过在请求正文中将`path`属性设置为`/schedule/schedule`，可以更新计划查询的cron计划。 有关cron计划的详细信息，请阅读[cron表达式格式](https://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html)文档。

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 您希望PATCH的计划查询的`id`值。 |

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
| `op` | 要对查询计划执行的操作。 接受的值为`replace`。 |
| `path` | 要修补的值的路径。 在这种情况下，由于您正在更新计划查询的计划，因此您需要将`path`的值设置为`/schedule/schedule`。 |
| `value` | `/schedule`的更新值。 该值需要采用cron计划的形式。 因此，在此示例中，计划查询将每小时以45分钟标记运行。 |

**响应**

成功的响应返回HTTP状态202（已接受），并显示以下消息。

```json
{
    "message": "Request to patch accepted",
    "statusCode": 202
}
```

### 删除指定的计划查询

您可以通过向`/schedules`端点发出DELETE请求并在请求路径中提供要删除的计划查询的ID来删除指定的计划查询。

>[!NOTE]
>
>删除计划&#x200B;**之前必须**&#x200B;被禁用。

**API格式**

```http
DELETE /schedules/{SCHEDULE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 要DELETE的计划查询的`id`值。 |

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

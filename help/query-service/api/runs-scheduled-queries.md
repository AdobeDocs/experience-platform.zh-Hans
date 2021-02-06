---
keywords: Experience Platform；主页；热门主题；查询服务；运行计划查询；运行计划查询;查询服务；计划查询；计划查询;
solution: Experience Platform
title: 计划查询运行API端点
topic: runs for scheduled queries
description: 以下各节将介绍使用查询服务API运行计划查询时可以进行的各种API调用。
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 2%

---


# 计划查询运行端点

## 示例API调用

既然您了解了要使用哪些标头，就可以开始调用[!DNL Query Service] API。 以下各节将介绍您可以使用[!DNL Query Service] API进行的各种API调用。 每个调用都包括常规API格式、显示所需标头的示例请求和示例响应。

### 检索指定计划列表的所有运行查询

您可以检索特定计划查询的所有运行的列表，而不管这些运行当前正在运行还是已完成。 这是通过向`/schedules/{SCHEDULE_ID}/runs`端点发出GET请求来完成的，其中`{SCHEDULE_ID}`是要检索其运行的计划查询的`id`值。

**API格式**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 要检索的计划查询的`id`值。 |
| `{QUERY_PARAMETERS}` | （*可选*）添加到请求路径的参数，这些参数配置在响应中返回的结果。 可以包括多个参数，用和符(`&`)分隔。 以下列出了可用参数。 |

**查询参数**

以下是可用查询参数的列表，用于列出指定计划查询的运行。 所有这些参数都是可选的。 调用此端点时，无参数将检索所有可用于指定计划查询的运行。

| 参数 | 描述 |
| --------- | ----------- |
| `orderby` | 指定对结果进行排序的字段。 支持的字段为`created`和`updated`。 例如，`orderby=created`将按升序创建结果。 在创建前添加`-`(`orderby=-created`)将按降序创建项目。 |
| `limit` | 指定页面大小限制以控制页面中包含的结果数。 (*默认值：20*) |
| `start` | 使用从零开始的编号，偏移响应列表。 例如，`start=2`将返回从第三个列出的列表开始的查询。 (*默认值：0* |
| `property` | 根据字段筛选结果。 过滤器&#x200B;**必须**&#x200B;为HTML转义。 逗号用于组合多组过滤器。 支持的字段有`created`、`state`和`externalTrigger`。 支持的运算符的列表为`>`（大于）、`<`（小于）和`==`（等于）和`!=`（不等于）。 例如，`externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z`将返回在2019年4月20日之后手动创建、成功和创建的所有运行。 |

**请求**

以下请求检索指定计划查询的最后四个运行。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态200，并将指定计划查询的列表运行为JSON。 以下响应返回指定计划查询的最后四次运行。

```json
{
    "runsSchedules": [
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T12:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEyOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T13:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDEzOjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "SUCCESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T14:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE0OjMwOjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        },
        {
            "state": "IN_PROGRESS",
            "version": 1,
            "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
            "externalTrigger": "false",
            "created": "2020-01-08T15:30:00Z",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "GET"
                },
                "cancel": {
                    "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDE4OjQ1OjAwKzAwOjAw",
                    "method": "PATCH",
                    "body": "{ \"op\": \"cancel\" }"
                }
            }
        }
    ],
    "_page": {
        "orderby": "+created",
        "start": "2020-01-08T12:30:00Z",
        "count": 4
    },
    "_links": {},
    "version": 1
}
```

>[!NOTE]
>
>可以使用值`_links.cancel`来[停止指定计划查询的运行](#immediately-stop-a-run-for-a-specific-scheduled-query)。

### 立即触发特定计划查询的运行

通过向`/schedules/{SCHEDULE_ID}/runs`端点发出POST请求，可以立即触发指定计划查询的运行，其中`{SCHEDULE_ID}`是要触发其运行的计划查询的`id`值。

**API格式**

```http
POST /schedules/{SCHEDULE_ID}/runs
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态202（已接受），并显示以下消息。

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### 检索特定计划查询的运行的详细信息

通过向`/schedules/{SCHEDULE_ID}/runs/{RUN_ID}`端点发出GET请求并在请求路径中提供计划查询的ID和运行，可以检索特定计划查询的运行的详细信息。

**API格式**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 要检索其详细信息的计划查询的`id`值。 |
| `{RUN_ID}` | 要检索的运行的`id`值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含指定运行的详细信息。

```json
{
    "state": "success",
    "taskStatusList": [
        {
            "duration": 303,
            "endDate": "2020-01-08T23:49:02.346318",
            "state": "SUCCESS",
            "message": "Processed Successfully",
            "startDate": "2020-01-08T23:43:58.936269",
            "taskId": "7Omob151BM"
        }
    ],
    "version": 1,
    "id": "c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
    "scheduleId": "e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm",
    "externalTrigger": "false",
    "created": "2020-01-08T20:45:00",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "GET"
        },
        "cancel": {
            "href": "https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\" }"
        }
    }
}
```

### 立即停止特定计划查询的运行

通过向`/schedules/{SCHEDULE_ID}/runs/{RUN_ID}`端点发出PATCH请求并提供计划查询的ID和请求路径中的运行，可以立即停止特定计划查询的运行。

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 要检索其详细信息的计划查询的`id`值。 |
| `{RUN_ID}` | 要检索的运行的`id`值。 |

**请求**

此API请求使用JSON修补程序语法处理其有效负荷。 有关JSON修补程序工作原理的更多信息，请阅读API基础文档。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "op": "cancel"
 }'
```

**响应**

成功的响应会返回HTTP状态202（已接受），并显示以下消息。

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```

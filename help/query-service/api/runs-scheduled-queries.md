---
keywords: Experience Platform；主页；热门主题；查询服务；运行计划的查询；运行计划的查询；查询服务；计划的查询；计划的查询；
solution: Experience Platform
title: 计划的查询运行API端点
description: 以下部分介绍了您可以使用查询服务API对运行计划查询进行的各种API调用。
role: Developer
exl-id: 1e69b467-460a-41ea-900c-00348c3c923c
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 2%

---

# 计划的查询运行终结点

## 示例API调用

现在您了解了要使用哪些标头，就可以开始调用 [!DNL Query Service] API。 以下部分介绍了您可以使用进行的各种API调用。 [!DNL Query Service] API。 每个调用包括常规API格式、显示所需标头的示例请求以及示例响应。

### 检索指定计划查询的所有运行的列表

您可以检索特定计划查询的所有运行列表，而不管它们当前是否正在运行或已完成。 这是通过向以下网站发出GET请求来完成的 `/schedules/{SCHEDULE_ID}/runs` 端点，其中 `{SCHEDULE_ID}` 是 `id` 要检索其运行的计划查询的值。

**API格式**

```http
GET /schedules/{SCHEDULE_ID}/runs
GET /schedules/{SCHEDULE_ID}/runs?{QUERY_PARAMETERS}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要检索的计划查询的值。 |
| `{QUERY_PARAMETERS}` | (*可选*)参数添加到请求路径，用于配置响应中返回的结果。 可以包含多个参数，以&amp;分隔(`&`)。 下面列出了可用的参数。 |

**查询参数**

以下是可用于列出指定计划查询运行的查询参数列表。 所有这些参数都是可选的。 在不使用参数的情况下调用此端点将检索指定计划查询的所有可用运行。

| 参数 | 描述 |
| --------- | ----------- |
| `orderby` | 指定排序结果所依据的字段。 支持的字段包括 `created` 和 `updated`. 例如， `orderby=created` 将按创建的内容对结果进行升序排序。 添加 `-` 创建前(`orderby=-created`)将按创建的项以降序对项排序。 |
| `limit` | 指定页大小限制，以控制页中包含的结果数。 (*默认值：20*) |
| `start` | 指定ISO格式时间戳对结果进行排序。 如果未指定开始日期，则API调用将首先返回最早的运行，然后继续列出更新的结果<br> ISO时间戳允许在日期和时间实现不同级别的粒度。 基本ISO时间戳采用以下格式： `2020-09-07` 表示日期为2020年9月7日。 一个更复杂的示例可以编写为 `2022-11-05T08:15:30-05:00` 和对应于2022年11月5日， 8:15:上午30:00，美国东部标准时间。 可以为时区提供UTC偏移，并在后缀“Z”中表示(`2020-01-01T01:01:01Z`)。 如果未提供时区，则默认设置为0。 |
| `property` | 根据字段筛选结果。 过滤器 **必须** HTML逃跑了。 逗号用于组合多组过滤器。 支持的字段包括 `created`， `state`、和 `externalTrigger`. 支持的运算符列表包括 `>` （大于）， `<` （小于），且  `==` （等于），和 `!=` （不等于）。 例如， `externalTrigger==true,state==SUCCESS,created>2019-04-20T13:37:00Z` 将返回在2019年4月20日之后手动创建、成功和创建的所有运行。 |

**请求**

以下请求检索指定计划查询的最后四次运行。

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs?limit=4
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，并将指定计划查询的运行列表作为JSON提供。 以下响应返回指定计划查询的最后四次运行。

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
>您可以使用值 `_links.cancel` 到 [停止指定计划查询的运行](#immediately-stop-a-run-for-a-specific-scheduled-query).

### 立即触发特定计划查询的运行

您可以通过对以下对象发出POST请求，立即触发指定计划查询的运行： `/schedules/{SCHEDULE_ID}/runs` 端点，其中 `{SCHEDULE_ID}` 是 `id` 要触发其运行的计划查询的值。

**API格式**

```http
POST /schedules/{SCHEDULE_ID}/runs
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态202（已接受），并显示以下消息。

```json
{
    "message": "Request to trigger run of a scheduled query accepted.",
    "statusCode": 202
}
```

### 检索特定计划查询的运行详细信息

您可以通过向以下网站发出GET请求，检索有关特定计划查询运行的详细信息： `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` 端点，并提供计划查询的ID和请求路径中的运行。

**API格式**

```http
GET /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 您希望检索其运行详细信息的计划查询的值。 |
| `{RUN_ID}` | 此 `id` 要检索的运行的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200以及指定运行的详细信息。

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

### 立即停止针对特定计划查询的运行

您可以通过对发出一个PATCH请求，立即停止特定计划查询的运行。 `/schedules/{SCHEDULE_ID}/runs/{RUN_ID}` 端点，并提供计划查询的ID和请求路径中的运行。

**API格式**

```http
PATCH /schedules/{SCHEDULE_ID}/runs/{RUN_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 您希望检索其运行详细信息的计划查询的值。 |
| `{RUN_ID}` | 此 `id` 要检索的运行的值。 |

**请求**

此API请求对其有效负载使用JSON修补程序语法。 有关JSON修补程序如何工作的更多信息，请阅读API基础知识文档。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/query/schedules/e95186d65a28abf00a495d82_28e74200-e3de-11e9-8f5d-7f27416c5f0d_sample_scheduled_query7omob151bm_birvwm/runs/c2NoZWR1bGVkX18yMDIwLTAxLTA4VDIwOjQ1OjAwKzAwOjAw
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
     "op": "cancel"
 }'
```

**响应**

成功的响应返回HTTP状态202（已接受），并显示以下消息。

```json
{
    "message": "Request to cancel run of a scheduled query accepted",
    "statusCode": 202
}
```

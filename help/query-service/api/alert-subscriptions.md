---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；警报；
title: 警报订阅端点
description: 本指南提供了示例HTTP请求以及您可使用查询服务API对警报订阅端点进行的各种API调用的响应。
role: Developer
exl-id: 30ac587a-2286-4a52-9199-7a2a8acd5362
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '2666'
ht-degree: 1%

---

# 警报订阅端点

Adobe Experience Platform查询服务允许您为临时查询和计划查询订阅警报。 警报可以通过电子邮件、Platform UI内或两者来接收。 平台内警报和电子邮件警报的通知内容相同。 目前，查询警报只能通过使用 [查询服务API](https://developer.adobe.com/experience-platform-apis/references/query-service/).

>[!IMPORTANT]
>
>要接收电子邮件警报，您必须先在UI中启用此设置。 请参阅相关文档 [有关如何启用电子邮件警报的说明](../../observability/alerts/ui.md#enable-email-alerts).

下表说明了不同类型的查询支持的警报类型：

| 查询类型 | 支持的警报类型 |
|---|---|
| 临时查询 | `success` 或 `failed` 执行。 |
| 计划的查询 | `start`， `success`，或 `failed` 执行。 |

>[!NOTE]
>
>所有非SELECT查询都支持警报订阅，您无需是查询创建者即可订阅警报。 其他用户也可以在未创建的查询上注册警报。

以下警报适用于没有警报订阅的情况：

* 当批处理查询作业结束时，用户会收到通知。
* 当批量查询作业持续时间超过阈值时，将为安排查询的人员触发警报。

>[!NOTE]
>
>如果进行了适当配置，则可以从这些警报中排除用于测试的查询。

## 示例API调用

以下部分介绍了您可以使用查询服务API进行的各种API调用。 每个调用包括常规API格式、显示所需标头的示例请求以及示例响应。

## 检索组织和沙盒的所有警报的列表 {#get-list-of-org-alert-subs}

通过向以下对象发出GET请求，检索组织沙盒的所有警报的列表： `/alert-subscriptions` 端点。

**API格式**

```http
GET /alert-subscriptions
GET /alert-subscriptions?{QUERY_PARAMETERS}
```

| 属性 | 描述 |
| --------- | ----------- |
| `{QUERY_PARAMETERS}` | （可选）添加到请求路径的参数，用于配置响应中返回的结果。 可以包含多个参数，以&amp;分隔。 下面列出了可用的参数。 |

**查询参数**

以下是列出查询的可用查询参数列表。 所有这些参数都是可选的。 在不使用参数的情况下对此端点进行调用将检索对您的组织可用的所有查询。

| 参数 | 描述 |
| --------- | ----------- |
| `orderby` | 指定结果顺序的字段。 支持的字段包括 `created` 和 `updated`. 在属性名称前面加上 `+` 升序和 `-` 以降序排序。 默认为 `-created`. 请注意，`+`)必须转义 `%2B`. 例如 `%2Bcreated` 是升序创建顺序的值。 |
| `pagesize` | 使用此参数可控制要从每页的API调用中获取的记录数。 默认限制设置为每页最大记录50条。 |
| `page` | 指明要查看记录的返回结果的页码。 |
| `property` | 根据所选字段筛选结果。 过滤器 **必须** HTML逃跑了。 逗号用于组合多组过滤器。 以下属性允许筛选： <ul><li>id</li><li>资产ID</li><li>状态</li><li>警报类型</li></ul> 支持的运算符为 `==` （等于）。 例如， `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` 将返回具有匹配ID的警报。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**响应**

成功的响应会返回HTTP 200状态，并且 `alerts` 数组，其中包含分页和版本信息。 此 `alerts` 数组包含组织和特定沙盒的所有警报的详细信息。 每个响应最多有三个警报可用，响应正文中包含每个警报类型的一个警报。

>[!NOTE]
>
>此 `alerts._links` 中的对象 `alerts` 为简短起见，数组已截断。 的完整示例 `alerts._links` 对象可在 [POST请求的响应](#subscribe-users).

```json
{
    "alerts": [
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_start-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "0ca168f4-e46b-4f7f-be6a-bdc386271b4a",
            "id": "query_service_flow_run_success-dcf7b4be-ccd7-4c73-ae0c-a4bb34a40adada84",
            "status": "enabled",
            "alertType": "success",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        },
        {
            "assetId": "700d43d9-3b99-4d4c-8dbb-29c911c0e0df",
            "id": "query_service_flow_run_start-75da972a-e859-47a5-934c-629904daa1ef",
            "status": "enabled",
            "alertType": "start",
            "_links":{
                "self": {…},
                "subscribe": {…},
                "patch_status": {…},
                "get_list_of_subscribers_by_alert_type": {…},
                "delete": {…}
            }
        }
    ], 
    "_page": {
        "orderby": "-created",
        "page": 1,
        "count": 26,
        "pageSize": 50
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `alerts.assetId` | 将警报与特定查询关联的查询ID。 |
| `alerts.id` | 警报的名称。 此名称由警报服务生成，并用于警报仪表板。 警报名称由存储该警报的文件夹组成， `alertType`和流ID。 有关可用警报的信息，请参见 [平台警报仪表板文档](../../observability/alerts/ui.md). |
| `alerts.status` | 警报有四个状态值： `enabled`， `enabling`， `disabled`、和 `disabling`. 警报正在主动侦听事件，并在保留所有相关订阅者和设置的同时暂停以供将来使用，或者在这些状态之间转换。 |
| `alerts.alertType` | 警报的类型。 警报有三种潜在值，分别是： <ul><li>`start`：在查询开始执行时通知用户。</li><li>`success`：在查询完成时通知用户。</li><li>`failure`：在查询失败时通知用户。</li></ul> |
| `alerts._links` | 提供有关可用于检索、更新、编辑或删除与此警报ID相关信息的可用方法和端点的信息。 |
| `_page` | 对象包含用于描述顺序、大小、总页数和当前页面的属性。 |
| `_links` | 对象包含可用于获取资源的下一页或上一页的URI引用。 |

## 检索特定查询或计划ID的警报订阅信息 {#retrieve-all-alert-subscriptions-by-id}

通过向发出一个GET请求，检索特定查询ID或计划ID的警报订阅信息 `/alert-subscriptions/{QUERY_ID}` 或 `/alert-subscriptions/{SCHEDULE_ID}` 端点。

**API格式**

```http
GET /alert-subscriptions/{QUERY_ID}
GET /alert-subscriptions/{SCHEDULE_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{QUERY_ID}` | 要为其返回订阅信息的查询的ID。 |
| `{SCHEDULE_ID}` | 要为其返回订阅信息的计划查询的ID。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**响应**

成功的响应会返回HTTP状态200，并且 `alerts` 数组，其中包含所提供查询或计划ID的订阅信息。

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_failure-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "failure",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com",
                    "keverdeen@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_start-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com"
                ],
                "inContextNotifications": [
                    "rrunner@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `assetId` | 警报与此ID关联。 该ID可以是查询ID或计划ID。 |
| `id` | 警报的名称。 此名称由警报服务生成，并用于警报仪表板。 警报名称由存储该警报的文件夹组成， `alertType`和流ID。 有关可用警报的信息，请参见 [平台警报仪表板文档](../../observability/alerts/ui.md). |
| `status` | 警报有四个状态值： `enabled`， `enabling`， `disabled`、和 `disabling`. 警报正在主动侦听事件，并在保留所有相关订阅者和设置的同时暂停以供将来使用，或者在这些状态之间转换。 |
| `alertType` | 每个警报可以有三种不同的警报类型。 它们是： <ul><li>`start`：在查询开始执行时通知用户。</li><li>`success`：在查询完成时通知用户。</li><li>`failure`：在查询失败时通知用户。</li></ul> |
| `subscriptions.emailNotifications` | Adobe注册的电子邮件地址数组，适用于已订阅接收警报电子邮件的用户。 |
| `subscriptions.inContextNotifications` | 为订阅了警报的UI通知的Adobe注册的电子邮件地址数组。 |

## 检索特定查询或计划ID和警报类型的警报订阅信息 {#get-alert-info-by-id-and-alert-type}

通过向发出一个GET请求，检索特定ID和警报类型的警报订阅信息 `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` 端点。 这同时适用于查询或计划的查询ID。

**API格式**

```http
GET /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
GET /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 参数 | 描述 |
| -------- | ----------- |
| `ALERT_TYPE` | 此属性描述触发警报的查询执行的状态。 响应将仅包括此类警报的警报订阅信息。 每个警报可以有三种不同的警报类型。 它们是： <ul><li>`start`：在查询开始执行时通知用户。</li><li>`success`：在查询完成时通知用户。</li><li>`failure`：在查询失败时通知用户。</li></ul> |
| `QUERY_ID` | 要更新的查询的唯一标识符。 |
| `SCHEDULE_ID` | 要更新的计划查询的唯一标识符。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**响应**

成功的响应会返回HTTP状态200以及订阅的所有警报。 这包括警报ID、警报类型、订阅者的Adobe注册的电子邮件ID及其首选通知渠道。

```json
{
    "alerts": [
        {
            "assetId": "6df22232-f427-4250-a4e1-43cd30990641",
            "id": "query_service_flow_run_success-5cdc3bbe-750a-4d80-9c43-96e5e09f1a96",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "emailNotifications": [
                    "rrunner@adobe.com",
                    "jsnow@adobe.com"
                ],
                "inContextNotifications": [
                    "jsnow@adobe.com"
                ]
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ]
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `assetId` | 将警报与特定查询关联的查询ID。 |
| `alertType` | 警报的类型。 警报有三种潜在值，分别是： <ul><li>`start`：在查询开始执行时通知用户。</li><li>`success`：在查询完成时通知用户。</li><li>`failure`：在查询失败时通知用户。</li></ul> |
| `subscriptions` | 一个对象，用于传递与警报相关联的Adobe注册的电子邮件ID，以及用户将接收警报的渠道。 |
| `subscriptions.inContextNotifications` | 为订阅了警报的UI通知的Adobe注册的电子邮件地址数组。 |
| `subscriptions.emailNotifications` | Adobe注册的电子邮件地址数组，适用于已订阅接收警报电子邮件的用户。 |

## 检索用户订阅的所有警报的列表 {#get-alert-subscription-list}

通过向GET发出请求，检索用户订阅的所有警报的列表 `/alert-subscriptions/user-subscriptions/{EMAIL_ID}` 端点。 响应包括警报名称、ID、状态、警报类型和通知渠道。

**API格式**

```http
GET /alert-subscriptions/user-subscriptions/{EMAIL_ID}
```

| 参数 | 描述 |
| -------- | ----------- |
| `{EMAIL_ID}` | 注册到Adobe帐户的电子邮件地址用于识别订阅了警报的用户。 |
| `orderby` | 指定结果顺序的字段。 支持的字段包括 `created` 和 `updated`. 在属性名称前面加上 `+` 升序和 `-` 以降序排序。 默认为 `-created`. 请注意，`+`)必须转义 `%2B`. 例如 `%2Bcreated` 是升序创建顺序的值。 |
| `pagesize` | 使用此参数可控制要从每页的API调用中获取的记录数。 默认限制设置为每页最大记录50条。 |
| `page` | 指明要查看记录的返回结果的页码。 |
| `property` | 根据所选字段筛选结果。 过滤器 **必须** HTML逃跑了。 逗号用于组合多组过滤器。 以下属性允许筛选： <ul><li>id</li><li>资产ID</li><li>状态</li><li>警报类型</li></ul> 支持的运算符为 `==` （等于）。 例如， `id==6ebd9c2d-494d-425a-aa91-24033f3abeec` 将返回具有匹配ID的警报。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/user-subscriptions/rrunner@adobe.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**响应**

成功的响应返回HTTP状态200，并且 `items` 阵列，其中包含由订阅的警报的详细信息 `emailId` 已提供。

```json
{
    "items": [
        {
            "name": "query_service_flow_run_success-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "success",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        },
        {
            "name": "query_service_flow_run_start-8f057161-b312-4274-b629-f346c7d15c1f",
            "assetId": "39e65373-e47a-4feb-9e5a-dffa2f677bca",
            "status": "enabled",
            "alertType": "start",
            "subscriptions": {
                "inContextNotification": true,
                "emailNotifications": true
            },
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
                    "method": "GET"
                },
                "subscribe": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
                    "method": "POST",
                    "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
                },
                "patch_status": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "PATCH",
                    "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
                },
                "get_list_of_subscribers_by_alert_type": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "GET"
                },
                "delete": {
                    "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
                    "method": "DELETE"
                }
            }
        }
    ], "_page": {
            "orderby": "-created",
            "page": 1,
            "count": 26,
            "pageSize": 50
        },
    "_links": {
        "next": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=2"
        },
        "prev": {
            "href": "https://platform-int.adobe.io/data/foundation/query/queries/alert-subscriptions?orderby=-created&page=0"
        }
    },
    "version": 1
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | 警报的名称。 此名称由警报服务生成，并用于警报仪表板。 警报名称由存储该警报的文件夹组成， `alertType`和流ID。 有关可用警报的信息，请参见 [平台警报仪表板文档](../../observability/alerts/ui.md). |
| `assetId` | 将警报与特定查询关联的查询ID。 |
| `status` | 警报有四个状态值： `enabled`， `enabling`， `disabled`、和 `disabling`. 警报正在主动侦听事件，并在保留所有相关订阅者和设置的同时暂停以供将来使用，或者在这些状态之间转换。 |
| `alertType` | 警报的类型。 警报有三种潜在值，分别是： <ul><li>`start`：在查询开始执行时通知用户。</li><li>`success`：在查询完成时通知用户。</li><li>`failure`：在查询失败时通知用户。</li></ul> |
| `subscriptions` | 一个对象，用于传递与警报相关联的Adobe注册的电子邮件ID，以及用户将接收警报的渠道。 |
| `subscriptions.inContextNotifications` | 一个布尔值，用于确定用户接收警报通知的方式。 A `true` 值用于确认应通过UI提供警报。 A `false` 值可确保不会通过该渠道通知用户。 |
| `subscriptions.emailNotifications` | 一个布尔值，用于确定用户接收警报通知的方式。 A `true` 值用于确认应通过电子邮件提供警报。 A `false` 值可确保不会通过该渠道通知用户。 |

## 创建警报并订阅用户 {#subscribe-users}

要创建警报并订阅用户以接收警报，请发出 `POST` 请求 `/alert-subscriptions` 端点。 此请求使用将查询关联到新创建的警报 `assetId` 属性，并通过使用为用户订阅该查询的警报 `emailIds`.

>[!IMPORTANT]
>
>您最多可以在单个Adobe中传递五个请求注册的电子邮件ID。 要为5个以上的用户订阅警报，必须发出后续请求。

**API格式**

```http
POST /alert-subscriptions
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/alert-subscriptions
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '
    {
    "assetId": "a679dd0e-bcb2-4e69-a610-22d17ba98cac",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "rrunner@adobe.com",
            "jsnow@adobe.com"
        ],
        "inContextNotifications": true,
        "emailNotifications": true
    }
}'
```

| 属性 | 描述 |
| -------- | ----------- |
| `assetId` | 警报与此ID关联。 该ID可以是查询ID或计划ID。 |
| `alertType` | 警报的类型。 警报有三种潜在值，分别是： <ul><li>`start`：在查询开始执行时通知用户。</li><li>`success`：在查询完成时通知用户。</li><li>`failure`：在查询失败时通知用户。</li></ul> |
| `subscriptions` | 一个对象，用于传递与警报相关联的Adobe注册的电子邮件ID，以及用户将接收警报的渠道。 |
| `subscriptions.emailIds` | 一系列电子邮件地址，用于标识应接收警报的用户。 电子邮件地址 **必须** 注册到Adobe账户。 |
| `subscriptions.inContextNotifications` | 一个布尔值，用于确定用户接收警报通知的方式。 A `true` 值用于确认应通过UI提供警报。 A `false` 值可确保不会通过该渠道通知用户。 |
| `subscriptions.emailNotifications` | 一个布尔值，用于确定用户接收警报通知的方式。 A `true` 值用于确认应通过电子邮件提供警报。 A `false` 值可确保不会通过该渠道通知用户。 |

{style="table-layout:auto"}

**响应**

成功的响应返回HTTP状态202（已接受）以及新创建警报的详细信息。

```json
{
    "assetId": "c4f67291-1161-4943-bc29-8736469bb928",
    "id": "query_service_flow_run_failure-5f4cb942-b67c-4ea4-a90d-5b6245e60aca",
    "alertType": "failure",
    "subscriptions": {
        "emailIds": [
            "{USER_EMAIL_ID}"
        ],
        "inContextNotifications": false,
        "emailNotifications": true
    },
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928",
            "method": "GET"
        },
        "subscribe": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions",
            "method": "POST",
            "body": "{\"assetId\": \"queryId/scheduleId\", \"alertType\": \"start/success/failure\", \"subscriptions\": {\n\"emailIds\": [\"xyz@example.com\", \"abc@example.com\"], \"email\": true, \"inContext\": false}}"
        },
        "patch_status": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "PATCH",
            "body": "{ \"op\": \"replace\", \"path\": \"/status\", \"value\": \"enable/disable\" }"
        },
        "get_list_of_subscribers_by_alert_type": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "GET"
        },
        "delete": {
            "href": "https://platform.adobe.io/data/foundation/query/alert-subscriptions/c4f67291-1161-4943-bc29-8736469bb928/failure",
            "method": "DELETE"
        }
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 警报的名称。 此名称由警报服务生成，并用于警报仪表板。 警报名称由存储该警报的文件夹组成， `alertType`和流ID。 有关可用警报的信息，请参见 [平台警报仪表板文档](../../observability/alerts/ui.md). |
| `_links` | 提供有关可用于检索、更新、编辑或删除与此警报ID相关信息的可用方法和端点的信息。 |

## 启用或禁用警报 {#enable-or-disable-alert}

此请求使用查询或计划ID和警报类型引用特定警报，并将警报状态更新为 `enable` 或 `disable`. 您可以通过以下方式更新警报的状态 `PATCH` 请求 `/alert-subscriptions/{queryId}/{alertType}` 或 `/alert-subscriptions/{scheduleId}/{alertType}` 端点。

**API格式**

```http
PATCH /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
PATCH /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 参数 | 描述 |
| -------- | ----------- |
| `ALERT_TYPE` | 警报的类型。 警报有三种潜在值，分别是： <ul><li>`start`：在查询开始执行时通知用户。</li><li>`success`：在查询完成时通知用户。</li><li>`failure`：在查询失败时通知用户。</li></ul>必须在端点命名空间中指定当前警报类型才能更改它。 |
| `QUERY_ID` | 要更新的查询的唯一标识符。 |
| `SCHEDULE_ID` | 要更新的计划查询的唯一标识符。 |

**请求**

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start'' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
        "op": "replace",
        "path" : "/status",
        "value": "enable"
      }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `op` | 要执行的操作。 目前，唯一接受的值是 `replace`. |
| `path` | 此值与端点中的命名空间相关。 目前，唯一接受的值是 `/status`. |
| `value` | 在成功的PATCH请求中，这会更改 `status` 警报的值。 目前，接受的值包括 `enable` 或 `disable`. |

{style="table-layout:auto"}

**响应**

成功的响应会返回HTTP状态200，其中包含警报状态、类型和ID的详细信息以及它相关的查询。

```json
{
    "id" : "query_service_flow_run_success-4422fc69-eaa7-464e-945b-63cfd435d3d1",
    "assetId": "4422fc69-eaa7-464e-945b-63cfd435d3d1", 
    "alertType": "start",
    "status": "enabled"
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `id` | 警报的名称。 此名称由警报服务生成，并用于警报仪表板。 警报名称由存储该警报的文件夹组成， `alertType`和流ID。 有关可用警报的信息，请参见 [平台警报仪表板文档](../../observability/alerts/ui.md). |
| `assetId` | 警报与此ID关联。 该ID可以是查询ID或计划ID。 |
| `alertType` | 每个警报可以有三种不同的警报类型。 它们是： <ul><li>`start`：在查询开始执行时通知用户。</li><li>`success`：在查询完成时通知用户。</li><li>`failure`：在查询失败时通知用户。</li></ul> |
| `status` | 警报有四个状态值： `enabled`， `enabling`， `disabled`、和 `disabling`. 警报正在主动侦听事件，并在保留所有相关订阅者和设置的同时暂停以供将来使用，或者在这些状态之间转换。 |

## 删除特定查询和警报类型的警报 {#delete-alert-info-by-id-and-alert-type}

通过向发出一个DELETE请求，删除特定查询的警报，或计划ID和警报类型 `/alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}` 或 `/alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}` 端点。

```http
DELETE /alert-subscriptions/{QUERY_ID}/{ALERT_TYPE}
DELETE /alert-subscriptions/{SCHEDULE_ID}/{ALERT_TYPE}
```

| 参数 | 描述 |
| -------- | ----------- |
| `ALERT_TYPE` | 警报的类型。 警报有三种潜在值，分别是： <ul><li>`start`：在查询开始执行时通知用户。</li><li>`success`：在查询完成时通知用户。</li><li>`failure`：在查询失败时通知用户。</li></ul> DELETE请求仅适用于提供的特定警报类型。 |
| `QUERY_ID` | 要更新的查询的唯一标识符。 |
| `SCHEDULE_ID` | 要更新的计划查询的唯一标识符。 |

**请求**

```shell
curl -X DELETE 'https://platform.adobe.io/data/foundation/query/alert-subscriptions/4422fc69-eaa7-464e-945b-63cfd435d3d1/start' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**响应**

成功的响应会返回HTTP 200状态和确认消息，其中包含已删除警报的资产ID和警报类型。

```json
{
"message": "Alert Deleted Successfully for assetId: 6df22232-f427-4250-a4e1-43cd30990641 and alertType: success",
"statusCode": 200
}
```

## 后续步骤

本指南介绍如何使用 `/alert-subscriptions` 查询服务API中的端点。 阅读本指南后，您现在可以更好地了解如何为查询创建警报、为用户订阅警报、可用的警报类型以及如何检索、更新和删除警报订阅信息。

请参阅 [查询服务API指南](./getting-started.md) 以了解有关其他可用功能和操作的更多信息。

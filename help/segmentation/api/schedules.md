---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 计划
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# 计划开发人员指南

介绍

- 检索一列表计划
- 创建新计划
- 检索特定计划
- 更新特定计划
- 删除特定计划

## 入门指南

本指南中使用的API端点是分段API的一部分。 在继续之前，请查阅分段开 [发人员指南](./getting-started.md)。

特别是，分段开 [发人员指南的入门部分](./getting-started.md#getting-started) ，包括相关主题的链接、在文档中阅读示例API调用的指南，以及成功调用任何Experience Platform API所需的标题的重要信息。

## 检索一列表计划

您可以通过向端点发出GET请求，检索IMS组织的所有计划的列表 `/config/schedules` 信息。

**API格式**

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

- `{QUERY_PARAMETERS}`:(可&#x200B;*选*)添加到请求路径的参数，用于配置在响应中返回的结果。 可以包括多个参数，由&amp;符号(`&`)分隔。 以下列出了可用参数。

**查询参数**

以下是列出列表的可用查询参数计划。 所有这些参数都是可选的。 调用此端点时不带参数将检索组织的所有可用计划。

| 参数 | 描述 |
| --------- | ----------- |
| `start` | 指定偏移将从哪个页面开始。 默认情况下，此值将为0。 |
| `limit` | 指定返回的计划数。 默认情况下，此值为100。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=X \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态200，并将指定IMS组织的列表计划为JSON。

```json
{
    "_page": {
        "totalCount": 1,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "Batch Segmentation",
            "state": "active",
            "type": "batch_segmentation",
            "schedule": "0 0 1 * * ?",
            "properties": {
                "segments": []
            },
            "createEpoch": 1573158851,
            "updateEpoch": 1574365202
        }
    ],
    "_links": {
        "next": {}
    }
}
```

## 创建新计划

您可以通过向端点发出POST请求来创建新计划 `/config/schedules` 。

**API格式**

```http
POST /config/schedules
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "name": "profile-default",
  "type": "batch_segmentation",
  "properties": {
    "segments": [
      "*"
    ]
  },
  "schedule": "0 0 1 * * ?",
  "state": "inactive"
}
 '
```

| 参数 | 描述 |
| --------- | ------------ |
| `name` | **必需.** 计划的字符串名称。 |
| `type` | **必需.** 作为字符串的作业类型。 支持的两种类型是 `batch_segmentation` 和 `export`。 |
| `properties` | **必需.** 包含与计划相关的其他属性的对象。 |
| `properties.segments` | **等于时`type`必填`batch_segmentation`。** 使用 `["*"]` 可确保包括所有区段。 |
| `schedule` | **必需.** 包含作业计划的字符串。 有关cron计划的更多信息，请阅读 [cron表达式格式文档](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 。 在此示例中，“0 0 1 * *”表示此计划将在每月第一个月的午夜运行。 |
| `state` | *可选.* 包含计划状态的字符串。 支持的两种状态是 `active` 和 `inactive`。 默认情况下，状态设置为 `inactive`。 |

**响应**

成功的响应会返回HTTP状态200，其中包含您新创建的计划的详细信息。

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

## 检索特定计划

您可以通过向端点发出GET请求并在请求路径中提供计划值来检索有关 `/config/schedules` 特定计划的 `id` 详细信息。

**API格式**

```http
GET /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`:要 `id` 检索的计划的值。

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID}
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态200，其中包含有关指定计划的详细信息。

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
```

## 更新特定计划的详细信息

您可以通过向端点发出PATCH请求并在请求路径中提 `/config/schedules` 供计划值来更新指 `id` 定的计划。

PATCH请求支持两种不同的路径： `/state` 和 `/schedule`。

### 更新计划状态

您可以使 `/state` 用来更新计划的状态——活动或非活动。 要更新状态，您需要将值设置为 `active` 或 `inactive`。

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`:要 `id` 更新的计划的值。

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
  {
    "op": "add",
    "path": "/state",
    "value": "active"
  }
]
'
```

| 参数 | 描述 |
| --------- | ----------- |
| `path` | 要修补的值的路径。 在这种情况下，由于您要更新计划的状态，因此需要将值设置为 `path``/state`。 |
| `value` | 的更新值 `/state`。 此值可以设置为，也 `active` 可以 `inactive` 激活或取消激活计划。 |

**响应**

成功的响应会返回HTTP状态204（无内容）。

### 更新计划cron计划

您可以使用 `schedule` 来更新cron计划。 有关cron计划的更多信息，请阅读 [cron表达式格式文档](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 。

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`:要 `id` 更新的计划的值。

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
  {
    "op": "add",
    "path": "/schedule",
    "value": "0 0 2 * *"
  }
]
'
```

| 参数 | 描述 |
| --------- | ----------- |
| `path` | 要修补的值的路径。 在这种情况下，由于您要更新计划的cron计划，因此需要将值设置为 `path``/schedule`。 |
| `value` | 的更新值 `/state`。 此值必须为cron计划形式。 在此示例中，计划将在每月的第二天运行。 |

**响应**

成功的响应会返回HTTP状态204（无内容）。

## 删除特定计划

您可以通过向计划发出DELETE请求并在请求路径中提供该的值来请 `/config/schedules``id` 求删除指定的计划。

**API格式**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

- `{SCHEDULE_ID}`:要 `id` 删除的计划的值。

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/{SCHEDULE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态204（无内容），并显示以下消息：

```json
(No Content) Schedule deleted successfully
```

## 后续步骤

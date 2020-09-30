---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;schedules;schedule;api;API;
solution: Experience Platform
title: 计划
topic: developer guide
description: 计划是一种工具，可用于每天自动运行一次批处理分段作业。
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 3%

---


# 计划端点

计划是一种工具，可用于每天自动运行一次批处理分段作业。 您可以使用端点 `/config/schedules` 检索列表、创建新计划、检索特定计划的详细信息、更新特定计划或删除特定计划。

## 入门指南

本指南中使用的端点是API的一 [!DNL Adobe Experience Platform Segmentation Service] 部分。 在继续之前，请查 [看入门指南](./getting-started.md) ，了解成功调用API需要了解的重要信息，包括必需的头以及如何读取示例API调用。

## 检索列表计划 {#retrieve-list}

您可以通过向端点发出列表请求，为IMS组织检索所有计划的 `/config/schedules` GET。

**API格式**

端点 `/config/schedules` 支持多个查询参数，以帮助筛选结果。 虽然这些参数是可选的，但强烈建议使用它们以帮助降低昂贵的开销。 调用此端点时不使用任何参数将检索组织可用的所有计划。 可以包括多个参数，用和号(`&`)分隔。

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{START}` | 指定偏移将从哪个页面开始。 默认情况下，此值将为0。 |
| `{LIMIT}` | 指定返回的计划数。 默认情况下，此值为100。 |

**请求**

以下请求将检索您的IMS组织中发布的最后十个计划。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态200，并将指定IMS组织的列表计划返回为JSON。

>[!NOTE]
>
>以下响应已被截断为空格，并且只显示返回的第一个计划。

```json
{
    "_page": {
        "totalCount": 10,
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

| 属性 | 描述 |
| -------- | ------------ |
| `_page.totalCount` | 返回的计划总数。 |
| `_page.pageSize` | 计划页的大小。 |
| `children.name` | 计划的名称（字符串）。 |
| `children.type` | 作业的字符串类型。 支持的两种类型是“batch_segmentation”和“export”。 |
| `children.properties` | 包含与计划相关的其他属性的对象。 |
| `children.properties.segments` | 使用 `["*"]` 可确保包括所有区段。 |
| `children.schedule` | 包含作业计划的字符串。 作业只能计划每天运行一次，这意味着在24小时内不能将作业计划为多次运行。 有关cron计划的更多信息，请阅读 [cron表达式格式文档](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 。 在此示例中，“0 0 1 * *”表示此计划将在每月第一个月的午夜运行。 |
| `children.state` | 包含计划状态的字符串。 支持的两种状态为“活动”和“非活动”。 默认情况下，状态设置为“非活动”。 |

## Create a new schedule {#create}

可以通过向端点发出计划请求来创建新POST `/config/schedules` 。

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
    "name":"profile-default",
    "type":"batch_segmentation",
    "properties":{
        "segments":[
            "*"
        ]
    },
    "schedule":"0 0 1 * * ?",
    "state":"inactive"
}'
```

| 属性 | 描述 |
| -------- | ------------ |
| `name` | **必需。** 计划的名称（字符串）。 |
| `type` | **必需。** 作业的字符串类型。 支持的两种类型是“batch_segmentation”和“export”。 |
| `properties` | **必需。** 包含与计划相关的其他属性的对象。 |
| `properties.segments` | **等于“`type`batch_segmentation”时必需。** 使用 `["*"]` 可确保包括所有区段。 |
| `schedule` | *可选.* 包含作业计划的字符串。 作业只能计划每天运行一次，这意味着在24小时内不能将作业计划为多次运行。 有关cron计划的更多信息，请阅读 [cron表达式格式文档](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 。 在此示例中，“0 0 1 * *”表示此计划将在每月第一个月的午夜运行。 <br><br>如果未提供此字符串，将自动生成系统生成的计划。 |
| `state` | *可选.* 包含计划状态的字符串。 支持的两种状态为“活动”和“非活动”。 默认情况下，状态设置为“非活动”。 |

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

## 检索特定计划 {#get}

您可以通过向端点发出计划请求并提供您希望在请求路径中检索的GET的 `/config/schedules` ID，来检索有关特定计划的详细信息。

**API格式**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 要 `id` 检索的计划的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含有关指定计划的详细信息。

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

| 属性 | 描述 |
| -------- | ------------ |
| `name` | 计划的名称（字符串）。 |
| `type` | 作业的字符串类型。 支持的两种类型 `batch_segmentation` 是和 `export`。 |
| `properties` | 包含与计划相关的其他属性的对象。 |
| `properties.segments` | 使用 `["*"]` 可确保包括所有区段。 |
| `schedule` | 包含作业计划的字符串。 作业只能计划每天运行一次，这意味着在24小时内不能将作业计划为多次运行。 有关cron计划的更多信息，请阅读 [cron表达式格式文档](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 。 在此示例中，“0 0 1 * *”表示此计划将在每月第一个月的午夜运行。 |
| `state` | 包含计划状态的字符串。 支持的两种状态 `active` 是和 `inactive`。 默认情况下，状态设置为 `inactive`。 |

## 更新特定计划的详细信息 {#update}

您可以通过向端点发出计划请求并提 `/config/schedules` 供您尝试在请求路径中更新的计划的ID，来更新特定PATCH。

PATCH请求允许您更新单 [个计划](#update-state)[的状态](#update-schedule) 或cron计划。

### 更新计划状态 {#update-state}

您可以使用JSON修补程序操作更新计划的状态。 要更新状态，请将属 `path` 性声明 `/state` 为，并将 `value` 其设置为 `active` 或 `inactive`。 有关JSON修补程序的更多信息，请阅读 [JSON修补程](http://jsonpatch.com/) 序文档。

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 要 `id` 更新的计划的值。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
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
]'
```

| 属性 | 描述 |
| -------- | ----------- |
| `path` | 要修补的值的路径。 在这种情况下，由于您正在更新计划的状态，因此需要将值 `path` 设置为“/state”。 |
| `value` | 计划状态的更新值。 此值可以设置为“活动”或“非活动”以激活或取消激活计划。 |

**响应**

成功的响应返回HTTP状态204（无内容）。

### 更新cron计划 {#update-schedule}

您可以使用JSON修补程序操作更新cron计划。 要更新计划，请将属性声 `path` 明为 `/schedule` ，并将 `value` 其设置为有效的cron计划。 有关JSON修补程序的更多信息，请阅读 [JSON修补程](http://jsonpatch.com/) 序文档。 有关cron计划的更多信息，请阅读 [cron表达式格式文档](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 。

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 要 `id` 更新的计划的值。 |

**请求**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * *"
    }
]'
```

| 属性 | 描述 |
| -------- | ----------- |
| `path` | 要更新的值的路径。 在这种情况下，由于您要更新cron计划，因此需要将值 `path` 设置为 `/schedule`。 |
| `value` | cron计划的更新值。 此值必须为cron计划。 在此示例中，计划将在每月的第二天运行。 |

**响应**

成功的响应返回HTTP状态204（无内容）。

## 删除特定计划

您可以请求删除特定计划，方法是向端点发出DELETE请求 `/config/schedules` ，并在请求路径中提供您要删除的计划的ID。

**API格式**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 要 `id` 删除的计划的值。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容）。

## 后续步骤

阅读本指南后，您现在可以更好地了解计划的工作方式。
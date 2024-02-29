---
solution: Experience Platform
title: 计划API端点
description: 计划是一种可用于每天自动运行一次批处理分段作业的工具。
role: Developer
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '2040'
ht-degree: 3%

---

# 计划端点

计划是一种可用于每天自动运行一次批处理分段作业的工具。 您可以使用 `/config/schedules` 端点检索计划列表、创建新计划、检索特定计划的详细信息、更新特定计划或删除特定计划。

## 快速入门

本指南中使用的端点是 [!DNL Adobe Experience Platform Segmentation Service] API。 在继续之前，请查看 [快速入门指南](./getting-started.md) 有关成功调用API所需了解的重要信息，包括所需的标头以及如何读取示例API调用。

## 检索计划列表 {#retrieve-list}

您可以通过向以下网站发出GET请求，检索贵组织所有计划的列表 `/config/schedules` 端点。

**API格式**

此 `/config/schedules` 端点支持多个查询参数以帮助筛选结果。 虽然这些参数是可选的，但强烈建议使用这些参数以帮助减少昂贵的开销。 在不使用参数的情况下对此端点进行调用将检索对您的组织可用的所有计划。 可以包含多个参数，以&amp;分隔(`&`)。

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{START}` | 指定偏移将从哪一页开始。 默认情况下，该值将为0。 |
| `{LIMIT}` | 指定返回的计划数。 默认情况下，该值将为100。 |

**请求**

以下请求将检索您组织内发布的最近十个计划。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回HTTP状态200，并将指定组织的计划列表作为JSON返回。

>[!NOTE]
>
>以下响应已截断空格，仅显示返回的第一个计划。

```json
{
    "_page": {
        "totalCount": 10,
        "pageSize": 1
    },
    "children": [
        {
            "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
            "imsOrgId": "{ORG_ID}",
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
| `_page.pageSize` | 计划的页面大小。 |
| `children.name` | 作为字符串的计划名称。 |
| `children.type` | 字符串形式的作业类型。 支持的两种类型是“batch_segmentation”和“export”。 |
| `children.properties` | 包含与计划相关的其他属性的对象。 |
| `children.properties.segments` | 使用 `["*"]` 确保包括所有区段。 |
| `children.schedule` | 包含作业计划的字符串。 作业只能被安排每天运行一次，这意味着您不能将作业安排在24小时期间运行多次。 有关cron时间表的详细信息，请阅读 [cron表达式格式](#appendix). 在此示例中，“0 0 1 * *”表示此计划将在每天凌晨1:00运行。 |
| `children.state` | 包含计划状态的字符串。 支持的两种状态分别为“活动”和“不活动”。 默认情况下，状态设置为“不活动”。 |

## 创建新计划 {#create}

您可以通过向以下网站发出POST请求来创建新计划： `/config/schedules` 端点。

**API格式**

```http
POST /config/schedules
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/config/schedules \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | **必需。** 作为字符串的计划名称。 |
| `type` | **必需。** 字符串形式的作业类型。 支持的两种类型是“batch_segmentation”和“export”。 |
| `properties` | **必需。** 包含与计划相关的其他属性的对象。 |
| `properties.segments` | **在以下情况下需要 `type` 等于“batch_segmentation”。** 使用 `["*"]` 确保包括所有区段。 |
| `schedule` | *可选。* 包含作业计划的字符串。 作业只能被安排每天运行一次，这意味着您不能将作业安排在24小时期间运行多次。 有关cron时间表的详细信息，请阅读 [cron表达式格式](#appendix). 在此示例中，“0 0 1 * *”表示此计划将在每天凌晨1:00运行。 <br><br>如果未提供此字符串，则将自动生成系统生成的计划。 |
| `state` | *可选。* 包含计划状态的字符串。 支持的两种状态分别为“活动”和“不活动”。 默认情况下，状态设置为“不活动”。 |

**响应**

成功的响应返回HTTP状态200以及新创建计划的详细信息。

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
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

您可以通过向以下网站发出GET请求，检索有关特定计划的详细信息： `/config/schedules` 端点，并提供要在请求路径中检索的计划的ID。

**API格式**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要检索的计划的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态200，其中包含有关指定调度的详细信息。

```json
{
    "id": "4e538382-dbd8-449e-988a-4ac639ebe72b",
    "imsOrgId": "{ORG_ID}",
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
| `name` | 作为字符串的计划名称。 |
| `type` | 字符串形式的作业类型。 支持的两种类型为 `batch_segmentation` 和 `export`. |
| `properties` | 包含与计划相关的其他属性的对象。 |
| `properties.segments` | 使用 `["*"]` 确保包括所有区段。 |
| `schedule` | 包含作业计划的字符串。 作业只能被安排每天运行一次，这意味着您不能将作业安排在24小时内运行多次。 有关cron时间表的详细信息，请阅读 [cron表达式格式](#appendix). 在此示例中，“0 0 1 * *”表示此计划将在每天凌晨1:00运行。 |
| `state` | 包含计划状态的字符串。 两种支持的状态是 `active` 和 `inactive`. 默认情况下，状态设置为 `inactive`. |

## 更新特定计划的详细信息 {#update}

您可以通过向以下网站发出PATCH请求来更新特定计划： `/config/schedules` 端点并在请求路径中提供您尝试更新的计划的ID。

PATCH请求允许您更新 [state](#update-state) 或 [cron计划](#update-schedule) 用于单个计划。

### 更新计划状态 {#update-state}

您可以使用JSON修补程序操作来更新计划的状态。 要更新状态，您需要声明 `path` 属性为 `/state` 并设置 `value` 更改为 `active` 或 `inactive`. 有关JSON修补程序的更多信息，请参阅 [JSON修补程序](https://datatracker.ietf.org/doc/html/rfc6902) 文档。

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要更新的计划的值。 |

**请求**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `path` | 要修补的值的路径。 在这种情况下，由于您正在更新计划的状态，因此需要设置值 `path` 更改为“/state”。 |
| `value` | 计划状态的更新值。 此值可设置为“活动”或“不活动”以激活或停用计划。 请注意 **无法** 如果组织已启用流式传输，则禁用计划。 |

**响应**

成功的响应返回HTTP状态204（无内容）。

### 更新cron计划 {#update-schedule}

您可以使用JSON修补程序操作来更新cron计划。 要更新计划，您需要声明 `path` 属性为 `/schedule` 并设置 `value` 到有效的cron计划。 有关JSON修补程序的更多信息，请参阅 [JSON修补程序](https://datatracker.ietf.org/doc/html/rfc6902) 文档。 有关cron时间表的详细信息，请阅读 [cron表达式格式](#appendix).

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要更新的计划的值。 |

**请求**

```shell
curl -X PATCH https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
[
    {
        "op":"add",
        "path":"/schedule",
        "value":"0 0 2 * * ?"
    }
]'
```

| 属性 | 描述 |
| -------- | ----------- |
| `path` | 要更新的值的路径。 在这种情况下，由于您正在更新cron计划，因此需要设置值 `path` 到 `/schedule`. |
| `value` | cron计划的更新值。 该值需要采用cron计划的形式。 在此示例中，计划将在每月的第二日运行。 |

**响应**

成功的响应返回HTTP状态204（无内容）。

## 删除特定计划

您可以通过对以下地址发出DELETE请求，请求删除特定计划： `/config/schedules` 端点并在请求路径中提供要删除的计划ID。

**API格式**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 此 `id` 要删除的计划的值。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回HTTP状态204（无内容）。

## 后续步骤

阅读本指南后，您现在可以更好地了解时间表的工作方式。

## 附录 {#appendix}

以下附录说明了时间表中使用的cron表达式的格式。

### 格式

cron表达式是由6或7个字段组成的字符串。 该表达式将类似于以下内容：

`0 0 12 * * ?`

在cron表达式字符串中，第一个字段表示秒，第二个字段表示分钟，第三个字段表示小时，第四个字段表示一月中的第几天，第五个字段表示一月中的第几天，第六个字段表示一周中的第几天。 您还可以选择包含第七个字段，该字段表示年份。

| 字段名称 | 必需 | 可能值 | 允许的特殊字符 |
| ---------- | -------- | --------------- | -------------------------- |
| Seconds | 是 | 0-59 | `, - * /` |
| Minutes | 是 | 0-59 | `, - * /` |
| 小时 | 是 | 0 时至 23 时 | `, - * /` |
| 月中几号 | 是 | 1 日至 31 日 | `, - * ? / L W` |
| 月 | 是 | 1-12,12月1日 | `, - * /` |
| 每周的某一日 | 是 | 1-7，星期六 | `, - * ? / L #` |
| 年 | 否 | 空的，1970-2099 | `, - * /` |

>[!NOTE]
>
>月份和星期的名称是 **非** 区分大小写。 因此， `SUN` 相当于使用 `sun`.

允许使用的特殊字符表示以下含义：

| 特殊字符 | 描述 |
| ----------------- | ----------- |
| `*` | 此值用于选择 **所有** 字段中的值。 例如，将 `*` 在小时字段中，将表示 **每** 小时。 |
| `?` | 此值表示不需要特定值。 这通常用于在一个允许字符的字段中指定某些内容，但在另一个字段中不指定该字符。 例如，如果您希望某个事件在每月第3天触发，但不管在一周中的哪一天触发，您会将 `3` 在“日期”字段中和 `?` 在“星期”字段中。 |
| `-` | 此值用于指定 **包含** 字段的范围。 例如，如果您将 `9-15` 在“小时数”字段中，这意味着小时数将包括9、10、11、12、13、14和15。 |
| `,` | 此值用于指定其他值。 例如，如果您将 `MON, FRI, SAT` 在“星期”字段中，这表示一周的日期包括星期一、星期五和星期六。 |
| `/` | 此值用于指定增量。 放置在 `/` 确定从何处递增，而值则放在 `/` 确定增量大小。 例如，如果您将 `1/7` 在分钟字段中，这将意味着该分钟将包含1、8、15、22、29、36、43、50和57。 |
| `L` | 此值用于指定 `Last`，并且根据其使用的字段具有不同的含义。 如果将其与月中的日字段一起使用，则它表示月中的最后一天。 如果单独与星期字段一起使用，则它表示一周的最后一天，即星期六(`SAT`)。 如果将其与“星期”字段一起使用，并配合使用其他值，则它表示该月中该类型的最后一天。 例如，如果您将 `5L` 在“星期”字段中，它将 **仅限** 包括一个月的最后一个星期五。 |
| `W` | 此值用于指定离给定日期最近的工作日。 例如，如果您将 `18W` 在月中的某天字段中，当月18日是星期六，则会在17日星期五触发，这是最接近的工作日。 如果当月18日是星期日，则会在19日星期一触发，这是最接近的工作日。 请注意，如果您将 `1W` 在“月”字段中，如果最近的工作日是上个月，则事件仍会在最近的工作日触发 **当前** 月。</br></br>此外，您可以组合 `L` 和 `W` 制作 `LW`，指定月份的最后一个工作日。 |
| `#` | 此值用于指定每月一周的第n天。 放置在 `#` 表示一周中的第几天，而值放置在 `#` 表示当月发生的次数。 例如，如果您将 `1#3`，则会在该月的第三个星期日触发该事件。 请注意，如果您将 `X#5` 而且那个月没有第五次出现该周某天，该事件将 **非** 被触发了。 例如，如果您将 `1#5`，并且当月没有第五个星期日，该事件将 **非** 被触发了。 |

### 示例

下表显示了cron表达式字符串示例及其含义。

| 表达式 | 解释 |
| ---------- | ----------- |
| `0 0 13 * * ?` | 事件将在每天下午1点触发。 |
| `0 30 9 * * ? 2022` | 该活动将于2022年每天上午9:30触发。 |
| `0 * 18 * * ?` | 该事件将每分钟触发一次，从下午6点开始，到每天下午6:59结束。 |
| `0 0/10 17 * * ?` | 该活动每10分钟触发一次，从下午5点开始，到每天下午6点结束。 |
| `0 13,38 5 ? 6 WED` | 该活动将于每年6月星期三清晨5点13分和清晨5点38分开始。 |
| `0 30 12 ? * 4#3` | 活动将于每月第三周的中午12:30激发。 |
| `0 30 12 ? * 6L` | 活动将于每月最后一个星期五中午12:30触发。 |
| `0 45 11 ? * MON-THU` | 事件将在每星期一、星期二、星期三和星期四上午11:45激发。 |
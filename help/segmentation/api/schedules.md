---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；计划；计划；API;API;
solution: Experience Platform
title: 计划API端点
topic-legacy: developer guide
description: 计划是一种工具，可用于每天自动运行一次批量分段作业。
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '2013'
ht-degree: 3%

---

# 计划端点

计划是一种工具，可用于每天自动运行一次批量分段作业。 您可以使用 `/config/schedules` 端点来检索计划列表、创建新计划、检索特定计划的详细信息、更新特定计划或删除特定计划。

## 快速入门

本指南中使用的端点是 [!DNL Adobe Experience Platform Segmentation Service] API。 在继续之前，请查看 [入门指南](./getting-started.md) 有关成功调用API所需的重要信息，包括所需的标头以及如何读取示例API调用。

## 检索计划列表 {#retrieve-list}

您可以通过向 `/config/schedules` 端点。

**API格式**

的 `/config/schedules` 端点支持多个查询参数来帮助筛选结果。 虽然这些参数是可选的，但强烈建议使用这些参数，以帮助减少昂贵的开销。 对此端点进行无参数调用将检索适用于贵组织的所有计划。 可以包含多个参数，这些参数之间用与号(`&`)。

```http
GET /config/schedules
GET /config/schedules?start={START}
GET /config/schedules?limit={LIMIT}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{START}` | 指定偏移将从哪个页面开始。 默认情况下，此值将为0。 |
| `{LIMIT}` | 指定返回的计划数。 默认情况下，此值将为100。 |

**请求**

以下请求将检索在您的IMS组织内发布的最近十个计划。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含指定IMS组织的计划列表(JSON)。

>[!NOTE]
>
>以下响应已因空间而被截断，并且仅显示返回的第一个计划。

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
| `_page.pageSize` | 计划页面的大小。 |
| `children.name` | 作为字符串的计划的名称。 |
| `children.type` | 作为字符串的作业类型。 支持的两种类型为“batch_segmentation”和“export”。 |
| `children.properties` | 包含与计划相关的其他属性的对象。 |
| `children.properties.segments` | 使用 `["*"]` 确保包含所有区段。 |
| `children.schedule` | 包含作业计划的字符串。 作业只能计划每天运行一次，这意味着您不能计划在24小时内运行多次作业。 欲知有关Cron计划的更多信息，请阅读 [cron表达式格式](#appendix). 在此示例中，“0 0 1 *”表示此计划将在每天凌晨1点运行。 |
| `children.state` | 包含计划状态的字符串。 两个受支持状态为“活动”和“不活动”。 默认情况下，状态设置为“不活动”。 |

## 创建新计划 {#create}

您可以通过向 `/config/schedules` 端点。

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
| `name` | **必需。** 作为字符串的计划的名称。 |
| `type` | **必需。** 作为字符串的作业类型。 支持的两种类型为“batch_segmentation”和“export”。 |
| `properties` | **必需。** 包含与计划相关的其他属性的对象。 |
| `properties.segments` | **在 `type` 等于“batch_segmentation”。** 使用 `["*"]` 确保包含所有区段。 |
| `schedule` | *可选.* 包含作业计划的字符串。 作业只能计划每天运行一次，这意味着您不能计划在24小时内运行多次作业。 欲知有关Cron计划的更多信息，请阅读 [cron表达式格式](#appendix). 在此示例中，“0 0 1 *”表示此计划将在每天凌晨1点运行。 <br><br>如果未提供此字符串，则将自动生成系统生成的计划。 |
| `state` | *可选.* 包含计划状态的字符串。 两个受支持状态为“活动”和“不活动”。 默认情况下，状态设置为“不活动”。 |

**响应**

成功响应会返回HTTP状态200，其中包含您新创建的计划的详细信息。

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

您可以通过向 `/config/schedules` 端点和提供您希望在请求路径中检索的计划的ID。

**API格式**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 的 `id` 要检索的计划值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态200，其中包含有关指定计划的详细信息。

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
| `name` | 作为字符串的计划的名称。 |
| `type` | 作为字符串的作业类型。 支持的类型包括 `batch_segmentation` 和 `export`. |
| `properties` | 包含与计划相关的其他属性的对象。 |
| `properties.segments` | 使用 `["*"]` 确保包含所有区段。 |
| `schedule` | 包含作业计划的字符串。 作业只能计划每天运行一次，这意味着您不能计划在24小时内运行多次作业。 欲知有关Cron计划的更多信息，请阅读 [cron表达式格式](#appendix). 在此示例中，“0 0 1 *”表示此计划将在每天凌晨1点运行。 |
| `state` | 包含计划状态的字符串。 支持的状态有 `active` 和 `inactive`. 默认情况下，状态设置为 `inactive`. |

## 更新特定计划的详细信息 {#update}

您可以通过向 `/config/schedules` 端点和提供您尝试在请求路径中更新的计划的ID。

PATCH请求允许您更新 [state](#update-state) 或 [cron计划](#update-schedule) 单个计划。

### 更新计划状态 {#update-state}

您可以使用JSON修补程序操作来更新计划的状态。 要更新状态，请声明 `path` 属性 `/state` 并设置 `value` 选择 `active` 或 `inactive`. 有关JSON修补程序的更多信息，请阅读 [JSON修补程序](https://datatracker.ietf.org/doc/html/rfc6902) 文档。

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 的 `id` 要更新的计划的值。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
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
| `path` | 要修补的值的路径。 在这种情况下，由于您正在更新计划的状态，因此需要设置 `path` 到“/state”。 |
| `value` | 计划状态的更新值。 此值可设置为“活动”或“不活动”以激活或停用计划。 请注意 **无法** 如果IMS组织已启用流式传输，则禁用计划。 |

**响应**

成功响应会返回HTTP状态204（无内容）。

### 更新cron计划 {#update-schedule}

您可以使用JSON修补程序操作来更新cron计划。 要更新计划，请声明 `path` 属性 `/schedule` 并设置 `value` 到有效的cron计划。 有关JSON修补程序的更多信息，请阅读 [JSON修补程序](https://datatracker.ietf.org/doc/html/rfc6902) 文档。 欲知有关Cron计划的更多信息，请阅读 [cron表达式格式](#appendix).

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 的 `id` 要更新的计划的值。 |

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
        "value":"0 0 2 * *"
    }
]'
```

| 属性 | 描述 |
| -------- | ----------- |
| `path` | 要更新的值的路径。 在这种情况下，由于您要更新cron计划，因此需要设置 `path` to `/schedule`. |
| `value` | cron计划的更新值。 此值需要采用cron计划的形式。 在本例中，计划将在每月的第二天运行。 |

**响应**

成功响应会返回HTTP状态204（无内容）。

## 删除特定计划

您可以通过向 `/config/schedules` 端点和提供您希望在请求路径中删除的计划的ID。

**API格式**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 的 `id` 要删除的计划值。 |

**请求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回HTTP状态204（无内容）。

## 后续步骤

阅读本指南后，您现在可以更好地了解计划的工作方式。

## 附录 {#appendix}

以下附录介绍了计划中使用的cron表达式的格式。

### 格式

cron表达式是由6或7个字段组成的字符串。 表达式应类似于以下内容：

`0 0 12 * * ?`

在cron表达式字符串中，第一个字段表示秒，第二个字段表示分钟，第三个字段表示小时，第四个字段表示月份的某天，第五个字段表示月，第六个字段表示星期几。 您还可以选择包含表示年份的第七个字段。

| 字段名称 | 必需 | 可能值 | 允许的特殊字符 |
| ---------- | -------- | --------------- | -------------------------- |
| Seconds | 是 | 0-59 | `, - * /` |
| Minutes | 是 | 0-59 | `, - * /` |
| 小时 | 是 | 0 时至 23 时 | `, - * /` |
| 月中几号 | 是 | 1 日至 31 日 | `, - * ? / L W` |
| 月 | 是 | 1-12,1月12日 | `, - * /` |
| 每周的某一日 | 是 | 1-7, SUN-SAT | `, - * ? / L #` |
| 年 | 否 | 空的，1970-2099年 | `, - * /` |

>[!NOTE]
>
>月份的名称和星期的名称为 **not** 区分大小写。 因此， `SUN` 等同于使用 `sun`.

允许使用的特殊字符表示以下含义：

| 特殊字符 | 描述 |
| ----------------- | ----------- |
| `*` | 此值用于选择 **全部** 值。 例如，在 `*` 在“小时”字段中表示 **每个** 小时。 |
| `?` | 此值表示不需要任何特定值。 通常，它用于在允许字符的一个字段中指定某些内容，但不能在另一个字段中指定。 例如，如果您希望每月的三分之一触发一次事件，但不关心一周中的哪一天，您会将 `3` （在月的某一天）字段和 `?` 在星期几字段中。 |
| `-` | 此值用于指定 **包含** 范围。 例如，如果将 `9-15` 在“小时”字段中，这表示“小时”将包括9、10、11、12、13、14和15。 |
| `,` | 此值用于指定其他值。 例如，如果将 `MON, FRI, SAT` 在“星期”字段中，这表示一周的日期包括星期一、星期五和星期六。 |
| `/` | 此值用于指定增量。 放置在 `/` 确定其从中递增的位置，而值将放在 `/` 确定它的增量。 例如，如果将 `1/7` 在“分钟”字段中，这表示分钟将包括1、8、15、22、29、36、43、50和57。 |
| `L` | 此值用于指定 `Last`，且的含义因使用的字段而异。 如果将其用于月的某天字段，则表示该月的最后一天。 如果单独将其与“星期”字段一起使用，则它表示一周的最后一天，即星期六(`SAT`)。 如果将其与“星期”字段和其他值一起使用，则它表示该月该类型的最后一天。 例如，如果将 `5L` 在星期一的场地里 **仅** 包括当月最后一个星期五。 |
| `W` | 此值用于指定与给定日期最接近的工作日。 例如，如果将 `18W` 在“月日”字段中，当月18日是星期六，它将在17日（星期五）触发，这是最接近的工作日。 如果当月18日是星期日，则将在19日星期一触发，这是最接近的工作日。 请注意，如果 `1W` 在“月份的某一天”字段中，最近的工作日是在上个月，则事件仍会在 **当前** 月。</br></br>此外，您还可以将 `L` 和 `W` 为 `LW`，指定当月的最后一个工作日。 |
| `#` | 此值用于指定一个月中一周的第n天。 放置在 `#` 表示一周中的某天，而将值放置在 `#` 表示该月中的哪个事件。 例如，如果将 `1#3`，则该事件将在当月第三个星期日触发。 请注意，如果 `X#5` 每周的第五次事件在该月没有，该事件将 **not** 触发。 例如，如果将 `1#5`，并且该月没有第五个星期日，活动将 **not** 触发。 |

### 示例

下表显示了cron表达式字符串示例并说明其含义。

| 表达式 | 说明 |
| ---------- | ----------- |
| `0 0 13 * * ?` | 该事件将于每天下午1点触发。 |
| `0 30 9 * * ? 2022` | 2022年，该活动将于每天早上9点30分触发。 |
| `0 * 18 * * ?` | 该事件将每分钟触发一次，从下午6点开始，到每天下午6点59分结束。 |
| `0 0/10 17 * * ?` | 该事件将每10分钟触发一次，从下午5点开始，到下午6点结束，一直持续。 |
| `0 13,38 5 ? 6 WED` | 活动将于6月每周三早5时13分和早5时38分开始。 |
| `0 30 12 ? * 4#3` | 活动将于每月第三个星期三中午12点30分触发。 |
| `0 30 12 ? * 6L` | 活动将在每月最后一个星期五中午12点30分触发。 |
| `0 45 11 ? * MON-THU` | 活动将于每周一、二、三、四的上午11:45触发。 |
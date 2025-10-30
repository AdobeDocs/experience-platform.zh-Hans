---
solution: Experience Platform
title: 计划API端点
description: 计划是一种可用于每天自动运行一次批处理分段作业的工具。
role: Developer
exl-id: 92477add-2e7d-4d7b-bd81-47d340998ff1
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '2088'
ht-degree: 2%

---

# 计划端点

计划是一种可用于每天自动运行一次批处理分段作业的工具。 您可以使用`/config/schedules`端点检索计划列表、创建新计划、检索特定计划的详细信息、更新特定计划或删除特定计划。

## 快速入门

本指南中使用的端点是[!DNL Adobe Experience Platform Segmentation Service] API的一部分。 在继续之前，请查看[快速入门指南](./getting-started.md)以了解成功调用API所需了解的重要信息，包括所需的标头以及如何读取示例API调用。

## 检索计划列表 {#retrieve-list}

您可以通过向`/config/schedules`端点发出GET请求来检索贵组织所有计划的列表。

**API格式**

`/config/schedules`端点支持多个查询参数以帮助筛选结果。 虽然这些参数是可选的，但强烈建议使用这些参数以帮助减少昂贵的开销。 在不使用参数的情况下对此端点进行调用将检索对您的组织可用的所有计划。 可以包含多个参数，以&amp;符号(`&`)分隔。

```http
GET /config/schedules
GET /config/schedules?{QUERY_PARAMETERS}
```

**查询参数**

+++ 可用查询参数的列表。

| 参数 | 描述 | 示例 |
| --------- | ----------- | ------- |
| `start` | 指定偏移将从哪一页开始。 默认情况下，该值将为0。 | `start=5` |
| `limit` | 指定返回的计划数。 默认情况下，该值将为100。 | `limit=20` |

+++

**请求**

以下请求将检索您组织内发布的最近十个计划。

+++ 用于检索计划列表的示例请求。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules?limit=10 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应会返回HTTP状态200，并将指定组织的计划列表作为JSON返回。

>[!NOTE]
>
>以下响应已截断空格，仅显示返回的第一个计划。

+++ 检索计划列表时的示例响应。

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
| `children.properties.segments` | 使用`["*"]`可确保包含所有区段。 |
| `children.schedule` | 包含作业计划的字符串。 作业只能被安排每天运行一次，这意味着您不能将作业安排在24小时期间运行多次。 有关cron计划的详细信息，请阅读[cron表达式格式](#appendix)的附录。 在此示例中，“`0 0 1 * *`”表示此计划将在每天凌晨1:00运行。 |
| `children.state` | 包含计划状态的字符串。 支持的两种状态分别为“活动”和“不活动”。 默认情况下，状态设置为“不活动”。 |

+++

## 创建新计划 {#create}

您可以通过向`/config/schedules`端点发出POST请求来创建新计划。

**API格式**

```http
POST /config/schedules
```

**请求**

+++ 创建计划的示例请求。 

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
| `name` | **必填。**&#x200B;作为字符串的计划名称。 |
| `type` | **必填。**&#x200B;作为字符串的作业类型。 支持的两种类型是“batch_segmentation”和“export”。 |
| `properties` | **必填。**&#x200B;包含与计划相关的其他属性的对象。 |
| `properties.segments` | **当`type`等于“batch_segmentation”时必需。**&#x200B;使用`["*"]`确保包含所有区段。 |
| `schedule` | *可选。*&#x200B;包含作业计划的字符串。 作业只能被安排每天运行一次，这意味着您不能将作业安排在24小时期间运行多次。 有关cron计划的详细信息，请阅读[cron表达式格式](#appendix)的附录。 在此示例中，“`0 0 1 * *`”表示此计划将在每天凌晨1:00运行。 <br><br>如果未提供此字符串，将自动生成系统生成的计划。 |
| `state` | *可选。*&#x200B;包含计划状态的字符串。 支持的两种状态分别为“活动”和“不活动”。 默认情况下，状态设置为“不活动”。 |

+++

**响应**

成功的响应返回HTTP状态200以及新创建计划的详细信息。

+++ 创建计划时的示例响应。

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

+++

## 检索特定计划 {#get}

您可以通过向`/config/schedules`端点发出GET请求，并在请求路径中提供要检索的计划ID，来检索有关特定计划的详细信息。

**API格式**

```http
GET /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 要检索的计划的`id`值。 |

**请求**

+++ 用于检索计划的示例请求。 

```shell
curl -X GET https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应返回HTTP状态200，其中包含有关指定调度的详细信息。

+++ 检索计划时的示例响应。

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
| `type` | 字符串形式的作业类型。 两种受支持的类型是`batch_segmentation`和`export`。 |
| `properties` | 包含与计划相关的其他属性的对象。 |
| `properties.segments` | 使用`["*"]`可确保包含所有区段。 |
| `schedule` | 包含作业计划的字符串。 作业只能被安排每天运行一次，这意味着您不能将作业安排在24小时内运行多次。 有关cron计划的详细信息，请阅读[cron表达式格式](#appendix)的附录。 在此示例中，“`0 0 1 * *`”表示此计划将在每天凌晨1:00运行。 |
| `state` | 包含计划状态的字符串。 两个支持的状态是`active`和`inactive`。 默认情况下，状态设置为`inactive`。 |

+++

## 更新特定计划的详细信息 {#update}

您可以更新特定计划，方法是向`/config/schedules`端点发出PATCH请求，并在请求路径中提供您尝试更新的计划的ID。

PATCH请求允许您更新单个计划的[状态](#update-state)或[cron计划](#update-schedule)。

**API格式**

```http
PATCH /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 要更新的计划的`id`值。 |

>[!BEGINTABS]

>[!TAB 更新计划状态]

您可以使用JSON修补程序操作来更新计划的状态。 要更新状态，请将`path`属性声明为`/state`并将`value`设置为`active`或`inactive`。 有关JSON修补程序的详细信息，请阅读[JSON修补程序](https://datatracker.ietf.org/doc/html/rfc6902)文档。

**请求**

+++ 更新计划状态的示例请求。

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

+++

| 属性 | 描述 |
| -------- | ----------- |
| `path` | 要修补的值的路径。 在这种情况下，由于您正在更新计划的状态，因此需要将`path`的值设置为“/state”。 |
| `value` | 计划状态的更新值。 此值可设置为“活动”或“不活动”以激活或停用计划。 请注意，如果组织已启用流式传输，则您&#x200B;**无法**&#x200B;禁用计划。 |

**响应**

成功的响应返回HTTP状态204（无内容）。

>[!TAB 更新cron计划]

您可以使用JSON修补程序操作来更新cron计划。 要更新计划，请将`path`属性声明为`/schedule`并将`value`设置为有效的cron计划。 有关JSON修补程序的详细信息，请阅读[JSON修补程序](https://datatracker.ietf.org/doc/html/rfc6902)文档。 有关cron计划的详细信息，请阅读[cron表达式格式](#appendix)的附录。

>[!ENDTABS]

**请求**

+++ 更新计划的示例请求。

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
| `path` | 要更新的值的路径。 在这种情况下，由于您正在更新cron计划，因此需要将`path`的值设置为`/schedule`。 |
| `value` | cron计划的更新值。 该值需要采用cron计划的形式。 在此示例中，计划将在每月的第二日运行。 |

+++

**响应**

成功的响应返回HTTP状态204（无内容）。

## 删除特定计划

您可以通过向`/config/schedules`端点发出DELETE请求并在请求路径中提供要删除的调度的ID，来请求删除特定调度。

**API格式**

```http
DELETE /config/schedules/{SCHEDULE_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SCHEDULE_ID}` | 要删除的计划的`id`值。 |

**请求**

+++ 删除计划的示例请求。

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/config/schedules/4e538382-dbd8-449e-988a-4ac639ebe72b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

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
| 小时 | 是 | 0-23 | `, - * /` |
| 每月的第几日 | 是 | 1-31 | `, - * ? / L W` |
| Month | 是 | 1-12,12月1日 | `, - * /` |
| 每周时间 | 是 | 1-7，星期六 | `, - * ? / L #` |
| Year | 否 | 空的，1970-2099 | `, - * /` |

>[!NOTE]
>
>月份名称和星期几的名称是&#x200B;**不区分**&#x200B;大小写。 因此，`SUN`等同于使用`sun`。

允许使用的特殊字符表示以下含义：

| 特殊字符 | 描述 |
| ----------------- | ----------- |
| `*` | 此值用于选择字段中的&#x200B;**所有**&#x200B;值。 例如，将`*`置于小时字段意味着每&#x200B;**小时**&#x200B;次。 |
| `?` | 此值表示不需要特定值。 这通常用于在一个允许字符的字段中指定某些内容，但在另一个字段中不指定该字符。 例如，如果希望每3个月触发一次事件，但不要关心该事件在一周中的哪一天，则会在月中的第几天字段中放置`3`，在周中的第几天字段中放置`?`。 |
| `-` | 此值用于指定字段的&#x200B;**包含**&#x200B;个范围。 例如，如果将`9-15`置于小时字段中，则意味着小时将包括9、10、11、12、13、14和15。 |
| `,` | 此值用于指定其他值。 例如，如果将`MON, FRI, SAT`置于星期字段中，则意味着一周的日期包括星期一、星期五和星期六。 |
| `/` | 此值用于指定增量。 放置在`/`之前的值决定其增量位置，而放置在`/`之后的值决定其增量大小。 例如，如果将`1/7`放在分钟字段中，则意味着分钟将包括1、8、15、22、29、36、43、50和57。 |
| `L` | 此值用于指定`Last`，并且根据其使用的字段具有不同的含义。 如果将其与月中的日字段一起使用，则它表示月中的最后一天。 如果单独与星期字段一起使用，则它表示一周的最后一天，即星期六(`SAT`)。 如果将其与“星期”字段一起使用，并配合使用其他值，则它表示该月中该类型的最后一天。 例如，如果将`5L`放在星期字段中，则&#x200B;**仅**&#x200B;包含该月的最后一个星期五。 |
| `W` | 此值用于指定离给定日期最近的工作日。 例如，如果将`18W`置于月份字段中，并且该月的18日是星期六，则会在17日的星期五触发，这是最接近的工作日。 如果当月18日是星期日，则会在19日星期一触发，这是最接近的工作日。 请注意，如果您将`1W`置于“月”字段中，且最近的工作日是上个月，则事件仍将在&#x200B;**当前**&#x200B;月的最近工作日触发。</br></br>此外，您可以将`L`和`W`结合使用，以生成`LW`，这会指定该月的最后一个工作日。 |
| `#` | 此值用于指定每月一周的第n天。 放置在`#`之前的值表示星期几，而放置在`#`之后的值表示当月它出现的次数。 例如，如果放入`1#3`，则事件将在月份的第三个星期日触发。 请注意，如果您输入`X#5`，而该月内没有出现该周的第5次发生次数，则事件将&#x200B;**不会**&#x200B;触发。 例如，如果放入`1#5`，并且该月没有第五个星期日，则事件将&#x200B;**不会**&#x200B;触发。 |

### 示例

下表显示了cron表达式字符串示例及其含义。

| 表达式 | 说明 |
| ---------- | ----------- |
| `0 0 13 * * ?` | 事件将在每天下午1点触发。 |
| `0 30 9 * * ? 2022` | 该活动将在2022年的每天的9:30AM触发。 |
| `0 * 18 * * ?` | 该事件将每分钟触发一次，从下午6点开始，到每天6:59PM结束。 |
| `0 0/10 17 * * ?` | 该活动每10分钟触发一次，从下午5点开始，到每天下午6点结束。 |
| `0 13,38 5 ? 6 WED` | 该事件将在6月的每个星期三的5:13AM和5:38AM触发。 |
| `0 30 12 ? * 4#3` | 该活动将于每月第三个星期三的12:30PM触发。 |
| `0 30 12 ? * 6L` | 该事件将在每月最后一个星期五的12:30PM触发。 |
| `0 45 11 ? * MON-THU` | 事件将在每个星期一、星期二、星期三和星期四的11:45AM触发。 |
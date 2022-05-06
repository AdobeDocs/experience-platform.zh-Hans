---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；流式分段；流式分段；连续评估；
solution: Experience Platform
title: '利用流分段快速实时评估事件 '
topic-legacy: developer guide
description: 本文档包含有关如何通过Adobe Experience Platform Segmentation Service API使用流分段的示例。
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1896'
ht-degree: 1%

---

# 使用流分段近乎实时地评估事件

>[!NOTE]
>
>以下文档说明了如何使用API进行流分段。 有关使用UI进行流式分段的信息，请阅读 [流式分段UI指南](../ui/streaming-segmentation.md).

流式分段 [!DNL Adobe Experience Platform] 允许客户近乎实时地进行分段，同时重点关注数据的丰富性。 通过流式客户细分，现在，当流数据进入 [!DNL Platform]，以缓解计划和运行分段作业的需求。 使用此功能，现在可以在数据被传递到时评估大多数区段规则 [!DNL Platform]，这意味着区段成员资格将保持为最新状态，而不运行计划的分段作业。

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>流分段适用于使用流源摄取的所有数据。 使用基于批处理的源摄取的区段将在夜间进行评估，即使它符合流式分段的条件也是如此。
>
>此外，如果使用流分段评估的区段基于使用批处理分段评估的另一个区段，则该区段可能会在理想成员资格与实际成员资格之间产生漂移。 例如，如果区段A基于区段B，并且区段B使用批量分段进行评估，因为区段B仅每24小时更新一次，因此区段A将远离实际数据，直到它与区段B更新重新同步为止。

## 快速入门

本开发人员指南需要对 [!DNL Adobe Experience Platform] 流分段涉及的服务。 在开始本教程之前，请查阅以下服务的文档：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的客户资料。
- [[!DNL Segmentation]](../home.md):提供从 [!DNL Real-time Customer Profile] 数据。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):标准化框架， [!DNL Platform] 组织客户体验数据。

以下部分提供了成功调用所需了解的其他信息 [!DNL Platform] API。

### 读取示例API调用

本开发人员指南提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将为所有中每个所需标头提供值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定虚拟沙箱隔离。 对 [!DNL Platform] API需要一个标头来指定操作将在其中执行的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关 [!DNL Platform]，请参阅 [沙盒概述文档](../../sandboxes/home.md).

所有包含有效负载(POST、PUT、PATCH)的请求都需要额外的标头：

- Content-Type:application/json

完成特定请求可能需要其他标头。 本文档的每个示例中都显示了正确的标题。 请特别注意示例请求，以确保包含所有必需的标头。

### 支持流分段的查询类型 {#query-types}

>[!NOTE]
>
>您需要为组织启用计划分段，才能使流式分段正常工作。 有关启用计划分段的信息，请参阅 [启用计划分段部分](#enable-scheduled-segmentation)

要使用流分段来评估区段，查询必须符合以下准则。

| 查询类型 | 详细信息 |
| ---------- | ------- |
| 单个事件 | 任何引用无时间限制的单个传入事件的区段定义。 |
| 相对时间窗口内的单个事件 | 引用单个传入事件的任何区段定义。 |
| 包含时间窗口的单个事件 | 引用带有时间窗口的单个传入事件的任何区段定义。 |
| 仅配置文件 | 仅引用配置文件属性的任何区段定义。 |
| 具有配置文件属性的单个事件 | 任何引用单个传入事件（无时间限制）和一个或多个用户档案属性的区段定义。 **注意：** 事件发生时，将立即评估查询。 但是，对于用户档案事件，必须等待24小时才能合并。 |
| 相对时间窗口内具有配置文件属性的单个事件 | 引用单个传入事件和一个或多个用户档案属性的任何区段定义。 |
| 区段 | 包含一个或多个批处理或流式处理区段的任何区段定义。 **注意：** 如果使用区段区段，则会发生配置文件取消资格事件 **每24小时**. |
| 具有配置文件属性的多个事件 | 引用多个事件的任何区段定义 **过去24小时内** 和（可选）具有一个或多个配置文件属性。 |

区段定义将 **not** 在以下情况下启用流分段：

- 区段定义包括Adobe Audience Manager(AAM)区段或特征。
- 区段定义包括多个实体（多实体查询）。

请注意，执行流式分段时应遵循以下准则：

| 查询类型 | 准则 |
| ---------- | -------- |
| 单个事件查询 | 回顾窗口没有限制。 |
| 包含事件历史记录的查询 | <ul><li>回顾窗口限制为 **一天**.</li><li>严格的时间排序条件 **必须** 事件之间存在。</li><li>支持具有至少一个否定事件的查询。 但是，整个事件 **无法** 是否定。</li></ul> |

如果修改了区段定义，使其不再符合流式分段的标准，则区段定义将自动从“流式”切换为“批处理”。

此外，区段取消资格与区段鉴别类似，会实时进行。 因此，如果受众不再符合某个区段的条件，则该受众将立即不合格。 例如，如果区段定义要求输入“过去三小时内购买了红鞋的所有用户”，则三小时后，最初符合区段定义条件的所有用户档案都将不合格。

## 检索为流式分段启用的所有区段

您可以通过向 `/segment/definitions` 端点。

**API格式**

要检索支持流式传输的区段，您必须包含查询参数 `evaluationInfo.continuous.enabled=true` 在请求路径中。

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回IMS组织中为流分段启用的区段数组。

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## 创建支持流式传输的区段

如果区段与 [上面列出的流分段类型](#query-types).

**API格式**

```http
POST /segment/definitions
```

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    }
}'
```

>[!NOTE]
>
>这是标准的“创建区段”请求。 有关创建区段定义的更多信息，请阅读 [创建区段](../tutorials/create-a-segment.md).

**响应**

成功的响应会返回新创建的启用流的区段定义的详细信息。

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true,
                   },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## 启用计划评估 {#enable-scheduled-segmentation}

启用流评估后，必须创建基线（在此之后，区段将始终保持最新）。 必须首先启用计划评估（也称为计划分段），以便系统自动执行基线设置。 通过计划分段，您的IMS组织可以遵守定期计划，以自动运行导出作业来评估区段。

>[!NOTE]
>
>对于最多五(5)个合并策略的沙箱，可以启用计划评估 [!DNL XDM Individual Profile]. 如果贵组织有五个以上的合并策略， [!DNL XDM Individual Profile] 在单个沙盒环境中，您将无法使用计划评估。

### 创建计划

通过向 `/config/schedules` 端点，您可以创建计划并包含应触发计划的特定时间。

**API格式**

```http
POST /config/schedules
```

**请求**

以下请求会根据有效负载中提供的规范创建新计划。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "{SCHEDULE_NAME}",
        "type": "batch_segmentation",
        "properties": {
            "segments": ["*"]
        },
        "schedule": "0 0 1 * * ?",
        "state": "inactive"
        }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `name` | **（必需）** 计划的名称。 必须是字符串。 |
| `type` | **（必需）** 字符串格式的作业类型。 支持的类型包括 `batch_segmentation` 和 `export`. |
| `properties` | **（必需）** 包含与计划相关的其他属性的对象。 |
| `properties.segments` | **(在 `type` 等于 `batch_segmentation`)** 使用 `["*"]` 确保包含所有区段。 |
| `schedule` | **（必需）** 包含作业计划的字符串。 作业只能计划每天运行一次，这意味着您不能计划在24小时内运行多次作业。 显示的示例(`0 0 1 * * ?`)表示作业在每天1时触发:00:00 UTC。 欲知详情，请参阅 [cron表达式格式](./schedules.md#appendix) 在文档中关于分段内的计划。 |
| `state` | *（可选）* 包含计划状态的字符串。 可用值： `active` 和 `inactive`. 默认值为 `inactive`。IMS组织只能创建一个计划。 本教程的后面部分提供了更新计划的步骤。 |

**响应**

成功的响应会返回新创建计划的详细信息。

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
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

### 启用计划

默认情况下，计划在创建时处于不活动状态，除非 `state` 属性设置为 `active` (在创建(POST)请求正文中)。 您可以启用计划(设置 `state` to `active`)，方法是向 `/config/schedules` 端点，并在路径中包含调度的ID。

**API格式**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**请求**

以下请求使用 [JSON修补程序格式](https://datatracker.ietf.org/doc/html/rfc6902) 以便更新 `state` 到 `active`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/state",
          "value": "active"
        }
      ]'
```

**响应**

成功更新会返回空的响应正文和HTTP状态204（无内容）。

同一操作可用于通过将上一个请求中的“值”替换为“不活动”来禁用计划。

## 后续步骤

现在，您已为流式分段启用新区段和现有区段，并且已启用计划区段以开发基线并执行定期评估，接下来您可以开始为组织创建支持流式分段。

要了解如何使用Adobe Experience Platform用户界面执行类似操作和处理区段，请访问 [区段生成器用户指南](../ui/segment-builder.md).

## 附录

以下部分列出了有关流式划分的常见问题解答：

### 流式分段是否也会实时发生“取消资格”？

对于大多数情况，流式分段会实时取消资格。 但是，使用区段的流区段确实会 **not** 取消实时资格，而是在24小时后取消资格。

### 流式分段适用于哪些数据？

流分段适用于使用流源摄取的所有数据。 使用基于批处理的源摄取的区段将在夜间进行评估，即使它符合流式分段的条件也是如此。

### 如何将区段定义为批量分段或流分段？

区段根据查询类型和事件历史记录持续时间的组合被定义为批量分段或流式分段。 在 [流式分段查询类型部分](#query-types).

### 用户能否将区段定义为批量区段或流区段？

此时，用户无法定义是使用批量摄取还是流式摄取来评估区段，因为系统将自动确定将使用哪种方法来评估区段。

### 为什么“符合条件的总数”区段的数量会持续增加，而“最近X天”下的数量在区段详细信息部分中保持为零？

符合条件的区段总数来自每日分段作业，其中包括符合批处理区段和流区段资格的受众。 此值同时针对批处理区段和流区段显示。

“最近X天”下的数字 **仅** 包括符合流式分段条件的受众，以及 **仅** 如果您已将数据流式传输到系统，并且它计入到流定义中，则会增加。 此值为 **仅** 显示的流区段。 因此，此值 **5月** 对于批处理客户细分，显示为0。

因此，如果您看到“最近X天”下的数字为零，并且折线图也报告为零，则您具有 **not** 将符合该区段资格的任何用户档案流式传输到系统中。
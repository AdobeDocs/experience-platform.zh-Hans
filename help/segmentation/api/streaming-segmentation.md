---
solution: Experience Platform
title: 使用流分段近乎实时地评估事件
description: 本文档包含有关如何将流式分段与Adobe Experience Platform分段服务API结合使用的示例。
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '1992'
ht-degree: 1%

---

# 通过流式分段近乎实时地评估事件

>[!NOTE]
>
>以下文档说明了如何使用API使用流式分段。 有关使用UI使用流式分段的信息，请阅读 [流式分段UI指南](../ui/streaming-segmentation.md).

流媒体分段 [!DNL Adobe Experience Platform] 允许客户近乎实时地进行分段，同时专注于数据丰富性。 借助流分段，现在当流数据进入时，就会进行区段鉴别 [!DNL Platform]，从而无需安排和运行分段作业。 借助此功能，现在可以在数据传入时评估大多数区段规则 [!DNL Platform]，这意味着区段成员资格将保持最新，而无需运行计划的分段作业。

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>流式分段适用于使用流式源摄取的所有数据。 使用基于批次的源摄取的区段将在夜间进行评估，即使它符合流式划分的条件。
>
>此外，如果区段定义基于使用批量分段评估的另一个区段定义，则使用流式分段评估的区段定义可能在理想成员资格和实际成员资格之间漂移。 例如，如果区段A基于区段B，而区段B是使用批处理分段来评估的，因为区段B仅每24小时更新一次，则区段A会与实际数据更远，直到它与区段B更新重新同步为止。

## 快速入门

本开发人员指南需要深入了解各种 [!DNL Adobe Experience Platform] 流分段涉及的服务。 在开始本教程之前，请查看以下服务的文档：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个源的汇总数据，实时提供统一的用户配置文件。
- [[!DNL Segmentation]](../home.md)：提供使用区段定义和其他外部源从创建受众的功能 [!DNL Real-Time Customer Profile] 数据。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Platform] 组织客户体验数据。

以下部分提供成功调用时需要了解的其他信息 [!DNL Platform] API。

### 正在读取示例API调用

本开发人员指南提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑难解答指南。

### 收集所需标题的值

为了调用 [!DNL Platform] API，您必须先完成 [身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 完成身份验证教程将提供所有中所有所需标头的值 [!DNL Experience Platform] API调用，如下所示：

- 授权：持有者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有资源 [!DNL Experience Platform] 与特定的虚拟沙盒隔离。 的所有请求 [!DNL Platform] API需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信息 [!DNL Platform]，请参见 [沙盒概述文档](../../sandboxes/home.md).

包含有效负载(POST、PUT、PATCH)的所有请求都需要额外的标头：

- Content-Type： application/json

可能需要其他标头才能完成特定请求。 正确的标题显示在本文档的每个示例中。 请特别注意示例请求，以确保包括所有必需的标头。

### 支持流式分段的查询类型 {#query-types}

>[!NOTE]
>
>您需要为组织启用计划分段，以便流式分段正常工作。 有关启用计划分段的信息，请参阅 [启用计划分段部分](#enable-scheduled-segmentation)

为了使用流式分段评估区段定义，查询必须遵循以下准则。

| 查询类型 | 详细信息 |
| ---------- | ------- |
| 单个事件 | 任何引用没有时间限制的单个传入事件的区段定义。 |
| 相对时间范围内的单个事件 | 任何引用单个传入事件的区段定义。 |
| 具有时间范围的单个事件 | 任何引用带有时间窗口的单个传入事件的区段定义。 |
| 仅配置文件 | 仅引用配置文件属性的任何区段定义。 |
| 具有配置文件属性的单个事件 | 任何引用单个传入事件（无时间限制）和一个或多个配置文件属性的区段定义。 **注意：** 当事件出现时，将立即评估查询。 但是，对于配置文件事件，它必须等待24小时才能合并。 |
| 相对时间范围内具有配置文件属性的单个事件 | 任何引用单个传入事件和一个或多个配置文件属性的区段定义。 |
| 区段分部 | 包含一个或多个批次或流区段的任何区段定义。 **注意：** 如果使用区段区段，则会发生配置文件取消资格 **每24小时**. |
| 具有配置文件属性的多个事件 | 引用多个事件的任何区段定义 **过去24小时内** 和（可选）具有一个或多个配置文件属性。 |

区段定义将 **非** 在以下场景中启用流分段：

- 区段定义包括Adobe Audience Manager (AAM)区段或特征。
- 区段定义包括多个实体（多实体查询）。
- 区段定义包括单个事件和 `inSegment` 事件。
   - 然而，倘该分部包含在 `inSegment` 事件仅用于配置文件，区段定义 **将** 启用流式客户细分功能。

请注意，在进行流分段时适用以下准则：

| 查询类型 | 准则 |
| ---------- | -------- |
| 单事件查询 | 回顾窗口没有限制。 |
| 使用事件历史记录进行查询 | <ul><li>回顾窗口限制为 **一天**.</li><li>严格的时间排序条件 **必须** 存在于事件之间。</li><li>支持至少具有一个否定事件的查询。 但是，整个事件 **无法** 是一种否定。</li></ul> |

如果修改了区段定义，使其不再符合流分段的标准，则区段定义将自动从“流”切换到“批次”。

此外，区段取消资格（与区段资格类似）是实时发生的。 因此，如果某个用户档案不再符合区段定义的条件，则它将被立即取消资格。 例如，如果区段定义要求“过去三小时内购买红鞋的所有用户”，则在三小时后，最初符合区段定义条件的所有配置文件都将不合格。

## 检索为流式分段启用的所有区段定义

您可以通过对以下网站发出GET请求，检索您的组织中启用流式分段的所有区段定义列表： `/segment/definitions` 端点。

**API格式**

要检索支持流的区段定义，您必须包含查询参数 `evaluationInfo.continuous.enabled=true` 在请求路径中。

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

成功的响应会返回您的组织中启用流式分段的一系列区段定义。

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

## 创建支持流的区段定义

如果区段定义与以下项之一匹配，则该区段定义将自动启用流式处理： [上面列出的流式分段类型](#query-types).

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
    }
}'
```

>[!NOTE]
>
>这是标准的“创建区段定义”请求。 有关创建区段定义的更多信息，请阅读以下教程： [创建区段定义](../tutorials/create-a-segment.md).

**响应**

成功响应将返回新创建的启用流的区段定义的详细信息。

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

启用流式评估后，必须创建基线（此后，区段定义将始终保持最新）。 必须首先启用计划评估（也称为计划分段），系统才能自动执行基准化。 通过计划的分段，您的组织可以遵循定期计划以自动运行导出作业来评估区段定义。

>[!NOTE]
>
>可以为最多具有五(5)个合并策略的沙盒启用计划评估 [!DNL XDM Individual Profile]. 如果贵组织有五个以上的合并策略 [!DNL XDM Individual Profile] 在单个沙盒环境中，您将无法使用计划的评估。

### 创建计划

向发出POST请求 `/config/schedules` 端点，您可以创建一个计划并包括应触发该计划的特定时间。

**API格式**

```http
POST /config/schedules
```

**请求**

以下请求基于有效负载中提供的规范创建新计划。

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
| `name` | **（必需）** 计划的名称。 必须为字符串。 |
| `type` | **（必需）** 字符串格式的作业类型。 支持的类型包括 `batch_segmentation` 和 `export`. |
| `properties` | **（必需）** 一个对象，其中包含与调度相关的其他属性。 |
| `properties.segments` | **(在以下情况下需要： `type` 等于 `batch_segmentation`)** 使用 `["*"]` 确保包括所有区段定义。 |
| `schedule` | **（必需）** 包含作业计划的字符串。 作业只能被安排每天运行一次，这意味着您不能将作业安排在24小时期间运行多次。 显示的示例(`0 0 1 * * ?`)表示作业每天在1触发:00:00 UTC. 欲知更多信息，请查阅 [cron表达式格式](./schedules.md#appendix) 有关分段内时间表的文档中。 |
| `state` | *（可选）* 包含计划状态的字符串。 可用值： `active` 和 `inactive`. 默认值为 `inactive`。组织只能创建一个计划。 更新计划的步骤将在本教程的后面部分提供。 |

**响应**

成功响应将返回新创建的计划的详细信息。

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

默认情况下，计划在创建时处于不活动状态，除非 `state` 属性设置为 `active` (POST)请求正文中的。 您可以启用计划(设置 `state` 到 `active`)向发出PATCH请求 `/config/schedules` 端点并在路径中包含计划的ID。

**API格式**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**请求**

以下请求使用 [JSON修补程序格式](https://datatracker.ietf.org/doc/html/rfc6902) 以更新 `state` 的日程安排 `active`.

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

成功更新将返回空响应正文和HTTP状态204（无内容）。

可使用同一操作禁用计划，方法是将上一个请求中的“值”替换为“非活动”。

## 后续步骤

现在，您已为流式分段启用新的和现有的区段定义，并启用了计划分段来开发基线和执行定期评估，您可以开始为组织创建支持流式处理的区段定义。

要了解如何使用Adobe Experience Platform用户界面执行类似操作和使用区段定义，请访问 [Segment Builder用户指南](../ui/segment-builder.md).

## 附录

以下部分列出了有关流式客户细分的常见问题解答：

### 流区段“取消资格”是否也会实时发生？

在大多数情况下，流式分段取消资格会实时发生。 但是，使用区段的流区段定义会 **非** 实时取消资格，而不是在24小时后取消资格。

### 流式分段处理哪些数据？

流式分段适用于使用流式源摄取的所有数据。 使用基于批次的源摄取的区段将在夜间进行评估，即使它符合流式划分的条件。 时间戳超过24小时且已流式传输到系统中的事件将在后续批处理作业中进行处理。

### 区段定义如何定义为批处理或流式分段？

区段定义定义为基于查询类型和事件历史记录持续时间的组合的批处理或流式分段。 要作为流区段评估哪些区段定义的列表，请参阅 [流式分段查询类型部分](#query-types).

请注意，如果区段包含 **两者** 一个 `inSegment` 表达式和直接单事件链，则不符合流式分段条件。 如果您希望此区段定义符合流式分段条件，则应将直接单事件链设置为自己的区段定义。

### 为什么“符合条件的总数”区段定义的数量持续增加，而“最近X天”下的数量在区段定义详细信息部分中保持为零？

符合条件的区段定义总数取自每日分段作业，其中包括同时符合批量定义和流式区段定义的受众。 该值会同时显示为批处理区段和流式区段定义。

“最近X天”下的数字 **仅限** 包括符合流分段条件的受众，以及 **仅限** 会增加（如果您已将数据流式传输到系统），并且这些数据计入该流式定义。 此值为 **仅限** 对于流区段定义显示。 因此，此值 **五月** 批处理区段定义显示为0。

因此，如果您看到“最近X天”下的数字为零，并且线形图也报告零，则您可以 **非** 已将符合该区段定义的任何用户档案流式传输到系统中。

### 区段定义需要多长时间才可用？

区段定义最多需要一小时才能可用。

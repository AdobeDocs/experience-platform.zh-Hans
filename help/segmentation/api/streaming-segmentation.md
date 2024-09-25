---
solution: Experience Platform
title: 使用流式分段近乎实时地评估事件
description: 本文档包含有关如何将流式分段与Adobe Experience Platform分段服务API一起使用的示例。
role: Developer
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: a1c9003a1b219325daf8fa38cda8bb1a019a55c6
workflow-type: tm+mt
source-wordcount: '2027'
ht-degree: 4%

---

# 通过流式分段近乎实时地评估事件

>[!NOTE]
>
>以下文档说明了如何使用API使用流式分段。 有关使用UI使用流式分段的信息，请阅读[流式分段UI指南](../ui/streaming-segmentation.md)。

在[!DNL Adobe Experience Platform]上流式分段允许客户近乎实时地进行分段，同时重点关注数据丰富度。 借助流式分段，现在可在流式数据进入[!DNL Platform]时进行区段鉴别，从而无需安排和运行分段作业。 借助此功能，现在可以在将数据传递到[!DNL Platform]时评估大多数区段规则，这意味着区段成员资格将保持最新，而无需运行计划的分段作业。

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>流式分段适用于使用流式源摄取的所有数据。 使用基于批次的源摄取的区段将在夜间进行评估，即使它符合流式分段条件。
>
>此外，如果区段定义基于使用批处理分段评估的另一个区段定义，则使用流式分段评估的区段定义可能在理想成员资格和实际成员资格之间漂移。 例如，如果区段A基于区段B，而区段B是使用批量分段评估的，因为区段B仅每24小时更新一次，则区段A会与实际数据进一步偏移，直到其与区段B更新重新同步为止。

## 快速入门

此开发人员指南需要实际了解与流式分段相关的各种[!DNL Adobe Experience Platform]服务。 在开始本教程之前，请查看以下服务的文档：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：基于来自多个源的聚合数据，实时提供统一的使用者配置文件。
- [[!DNL Segmentation]](../home.md)：提供使用区段定义和其他外部源从[!DNL Real-Time Customer Profile]数据创建受众的功能。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)： [!DNL Platform]用于组织客户体验数据的标准化框架。

以下部分提供成功调用[!DNL Platform] API所需了解的其他信息。

### 正在读取示例 API 调用

本开发人员指南提供了示例API调用，以演示如何格式化您的请求。 这些包括路径、必需的标头和格式正确的请求负载。还提供了在 API 响应中返回的示例 JSON。有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中有关[如何读取示例API调用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的部分。

### 收集所需标头的值

要调用[!DNL Platform] API，您必须先完成[身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份验证教程会提供所有 [!DNL Experience Platform] API 调用中每个所需标头的值，如下所示：

- 授权：持有人`{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有资源都被隔离到特定的虚拟沙盒中。 对[!DNL Platform] API的所有请求都需要一个标头，用于指定将在其中执行操作的沙盒的名称：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>有关[!DNL Platform]中沙盒的更多信息，请参阅[沙盒概述文档](../../sandboxes/home.md)。

包含负载 (POST、PUT、PATCH) 的所有请求都需要额外的标头：

- Content-Type： application/json

可能需要其他标头才能完成特定请求。 正确的标题显示在本文档的每个示例中。 请特别注意示例请求，以确保包括所有必需的标头。

### 支持流式分段的查询类型 {#query-types}

>[!NOTE]
>
>您需要为组织启用计划分段，流式分段才能正常工作。 有关启用计划分段的信息，请参阅[启用计划分段部分](#enable-scheduled-segmentation)

为了使用流式分段评估区段定义，查询必须符合以下准则。

| 查询类型 | 详细信息 |
| ---------- | ------- |
| 小于24小时时间范围内的单个事件 | 任何涉及少于24小时时间范围内的单个传入事件的区段定义。 |
| 仅配置文件 | 仅引用配置文件属性的任何区段定义。 |
| 在相对时间范围小于24小时内的配置文件属性为单个事件 | 任何涉及单个传入事件（具有一个或多个用户档案属性）且发生在小于24小时的相对时间范围内的区段定义。 |
| 区段划分 | 包含一个或多个批次或流式客户细分的任何客户细分定义。 **注意：**&#x200B;如果使用区段区段，则每24小时&#x200B;**将发生配置文件取消资格**。 |
| 具有配置文件属性的多个事件 | 任何在过去24小时&#x200B;**内引用多个事件**&#x200B;且（可选）具有一个或多个配置文件属性的区段定义。 |

在以下情况下，将&#x200B;**不**&#x200B;为流式分段启用区段定义：

- 区段定义包括Adobe Audience Manager (AAM)区段或特征。
- 区段定义包括多个实体（多实体查询）。
- 区段定义包含单个事件和`inSegment`事件的组合。
   - 但是，如果`inSegment`事件中包含的区段仅是配置文件，则区段定义&#x200B;**将**&#x200B;启用流式分段。
- 区段定义使用“忽略年份”作为其时间限制的一部分。

请注意，在进行流式分段时适用以下准则：

| 查询类型 | 准则 |
| ---------- | -------- |
| 单个事件查询 | 回顾窗口没有限制。 |
| 使用事件历史记录进行查询 | <ul><li>回看窗口限制为&#x200B;**一天**。</li><li>事件之间存在严格的时间排序条件&#x200B;**必须**。</li><li>支持至少具有一个否定事件的查询。 但是，整个事件&#x200B;**不能**&#x200B;是否定。</li></ul> |

如果修改了区段定义以使其不再满足流式分段标准，则区段定义将自动从“流式处理”切换到“批处理”。

此外，区段取消资格（与区段资格类似）是实时发生的。 因此，如果配置文件不再符合区段定义的条件，它将被立即取消资格。 例如，如果区段定义要求“过去三小时内购买红鞋的所有用户”，则在三小时后，最初符合区段定义条件的所有用户档案都将被取消资格。

## 检索为流式分段启用的所有区段定义

通过向`/segment/definitions`端点发出GET请求，您可以检索您的组织中启用流式分段的所有区段定义的列表。

**API格式**

要检索支持流式处理的区段定义，必须在请求路径中包含查询参数`evaluationInfo.continuous.enabled=true`。

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

成功的响应会返回组织中启用流式分段的一系列区段定义。

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
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

如果区段定义与上面列出的[流式分段类型之一](#query-types)匹配，则该区段定义将自动启用流式处理。

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
>这是标准的“创建区段定义”请求。 有关创建区段定义的更多信息，请阅读有关[创建区段定义](../tutorials/create-a-segment.md)的教程。

**响应**

成功的响应会返回新创建的启用流的区段定义的详细信息。

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
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

启用流式评估后，必须创建基线（此后，区段定义将始终保持最新）。 必须首先启用计划评估（也称为计划分段），系统才能自动执行基线化。 利用计划的分段，您的组织可以遵循定期计划来自动运行导出作业以评估区段定义。

>[!NOTE]
>
>可以为[!DNL XDM Individual Profile]最多有五(5)个合并策略的沙盒启用计划评估。 如果贵组织在单个沙盒环境中为[!DNL XDM Individual Profile]提供了五个以上的合并策略，您将无法使用计划的评估。

### 创建计划

通过向`/config/schedules`端点发出POST请求，您可以创建计划并包含应触发该计划的特定时间。

**API格式**

```http
POST /config/schedules
```

**请求**

以下请求基于有效负荷中提供的规范创建新计划。

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
| `name` | **（必需）**&#x200B;计划的名称。 必须为字符串。 |
| `type` | **（必需）**&#x200B;字符串格式的作业类型。 支持的类型为`batch_segmentation`和`export`。 |
| `properties` | **（必需）**&#x200B;包含与计划相关的其他属性的对象。 |
| `properties.segments` | **（当`type`等于`batch_segmentation`时为必需）**&#x200B;使用`["*"]`确保包含所有区段定义。 |
| `schedule` | **（必需）**&#x200B;包含作业计划的字符串。 作业只能被安排每天运行一次，这意味着您不能将作业安排在24小时内运行多次。 显示的示例(`0 0 1 * * ?`)表示作业每天在1:00:00 UTC触发。 有关详细信息，请查看分段内计划文档中的[cron表达式格式](./schedules.md#appendix)附录。 |
| `state` | *（可选）*&#x200B;包含计划状态的字符串。 可用值： `active`和`inactive`。 默认值为`inactive`。 组织只能创建一个计划。 本教程稍后会介绍更新计划的步骤。 |

**响应**

成功的响应将返回新创建计划的详细信息。

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

默认情况下，创建计划时处于非活动状态，除非在创建(POST)请求正文中将`state`属性设置为`active`。 您可以启用计划（将`state`设置为`active`），方法是向`/config/schedules`端点发出PATCH请求，并在路径中包含计划的ID。

**API格式**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**请求**

以下请求使用[JSON修补程序格式](https://datatracker.ietf.org/doc/html/rfc6902)以将计划的`state`更新为`active`。

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

成功更新将返回空的响应正文和HTTP状态204（无内容）。

可使用同一操作通过将上一个请求中的“值”替换为“非活动”来禁用计划。

## 后续步骤

现在，您已为流式分段启用新的和现有的区段定义，并启用了计划分段来开发基线和执行定期评估，您可以开始为组织创建支持流式处理的区段定义。

要了解如何使用Adobe Experience Platform用户界面执行类似操作和使用区段定义，请访问[区段生成器用户指南](../ui/segment-builder.md)。

## 附录

以下部分列出了有关流式客户细分的常见问题解答：

### 流式客户细分“不合格”是否也会实时发生？

在大多数情况下，流式分段取消资格会实时发生。 但是，使用区段的流区段定义不会&#x200B;**实时**&#x200B;取消资格，而是在24小时后取消资格。

### 流式分段处理哪些数据？

流式分段适用于使用流式源摄取的所有数据。 使用基于批次的源摄取的区段将在夜间进行评估，即使它符合流式分段条件。 时间戳超过24小时且流式传输到系统中的事件将在后续批处理作业中进行处理。

### 区段定义是如何定义为批处理或流式分段的？

区段定义定义为基于查询类型和事件历史记录持续时间的组合的批处理或流式分段。 可以在[流式分段查询类型部分](#query-types)中找到将作为流式分段评估的区段定义的列表。

请注意，如果区段同时包含&#x200B;**1}和`inSegment`表达式以及直接单事件链，则它不符合流式分段条件。**&#x200B;如果要使此区段定义符合流式分段条件，则应将直接单事件链设置为它自己的区段定义。

### 为什么“符合条件的总数”区段定义数量持续增加，而“最近X天”下的数量在区段定义详细信息部分中保持为零？

符合条件的区段定义总数源自每日分段作业，其中包括同时符合批量定义和流式区段定义的受众。 此值对于批次和流区段定义均显示。

“最近X天”**only**&#x200B;下的数字包括符合流式分段条件的受众，如果您已将数据流式传输到系统并且它计入该流式定义，则&#x200B;**only**&#x200B;会增加。 对于流区段定义，此值仅显示&#x200B;**个**。 因此，对于批处理区段定义，该值&#x200B;**可能**&#x200B;显示为0。

因此，如果您看到“最近X天”下的数字为零，并且折线图也报告零，则表示您有&#x200B;**没有**&#x200B;将任何符合该区段定义的配置文件流式传输到系统。

### 区段定义需要多久才能可用？

区段定义最多需要一小时才能可用。

### 流式传输的数据是否有任何限制？

为了在流式分段中使用流式传输的数据，流式传输的事件之间必须&#x200B;**有**&#x200B;间距。 如果在同一秒内有太多事件流入网络，Platform会将这些事件视为机器人生成的数据，因此它们将被丢弃。 作为最佳实践，您应在事件数据之间间隔至少&#x200B;**5秒**&#x200B;以确保正确使用该数据。

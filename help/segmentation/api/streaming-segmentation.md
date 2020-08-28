---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 流细分
topic: developer guide
translation-type: tm+mt
source-git-commit: d35d598b2ae8b46f53a20d41770b21ceeeafcce8
workflow-type: tm+mt
source-wordcount: '1426'
ht-degree: 1%

---


# 利用流细分快速实时评估事件

>[!NOTE]
>
>以下文档说明了如何使用API使用流分段。 有关使用UI使用流式分段的信息，请阅读流式 [分段UI指南](../ui/streaming-segmentation.md)。

基于的流 [!DNL Adobe Experience Platform] 式细分允许客户在关注数据丰富性的同时近乎实时地进行细分。 利用流细分，流数据进入时即会发生细分资格 [!DNL Platform]，从而减轻计划和运行细分作业的需求。 借助此功能，现在可以在数据传入时评估大多数细分规则， [!DNL Platform]这意味着，在不运行计划的细分作业的情况下，区段成员关系将保持最新状态。

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>流分段只能用于评估流入平台的数据。 换言之，通过批量摄取摄取的数据不会通过流分段进行评估，而需要触发批量评估。

## 入门指南

此开发人员指南需要对流分段所涉及的各 [!DNL Adobe Experience Platform] 种服务进行有效的了解。 在开始本教程之前，请查看以下服务的相关文档：

- [[!DNL实时客户用户档案]](../../profile/home.md):根据来自多个来源的汇总数据实时提供统一的消费者用户档案。
- [[!DNL分段]](../home.md):提供根据数据创建细分和受众的 [!DNL Real-time Customer Profile] 能力。
- [[!DNL体验数据模型(XDM)]](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。

以下各节提供了成功调用API所需了解的其他信 [!DNL Platform] 息。

### 读取示例API调用

此开发人员指南提供示例API调用，以演示如何格式化请求。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 用 [!DNL Experience Platform] 一节。

### 收集所需标题的值

要调用API，您必 [!DNL Platform] 须先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程可为所有API调用中的每个所需 [!DNL Experience Platform] 标头提供值，如下所示：

- 授权：承载者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有资源 [!DNL Experience Platform] 都与特定虚拟沙箱隔离。 对API的 [!DNL Platform] 所有请求都需要一个标头，它指定操作将在中进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有关中沙箱的详细信 [!DNL Platform]息，请参阅 [沙箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要附加标头：

- 内容类型：application/json

完成特定请求可能需要其他标题。 此文档中的每个示例都显示正确的标题。 请特别注意示例请求，以确保包含所有必需的标题。

### 支持流式分段的查询类型 {#streaming-segmentation-query-types}

>[!NOTE]
>
>您需要为组织启用计划分段才能使流式分段正常工作。 有关启用计划分段的信息，请参阅启用计 [划分段部分。](#enable-scheduled-segmentation)

要使用流分段来评估区段，查询必须遵循以下准则。

| 查询类型 | 详细信息 |
| ---------- | ------- |
| 传入点击 | 任何区段定义，指没有时间限制的单个传入事件。 |
| 相对时间窗口内的传入点击 | 指过去七天内单个传入事件 **的任何区段定义**。 |
| 仅用户档案 | 只引用用户档案属性的任何区段定义。 |
| 指用户档案 | 引用单个传入事件（无时间限制）和一个或多个用户档案属性的任何区段定义。 |
| 指相对时间窗口内用户档案的传入点击 | 在过去七天内引用单个传入事件和一个或多个属性 **的任何用户档案定义**。 |
| 引用事件的多个用户档案 | 任何引用过去24小时内的多个事件 **并且(可选** )具有一个或多个用户档案属性的定义。 |

下节列表段定义示例，这些示例将 **不启** 用流分段功能。

| 查询类型 | 详细信息 |
| ---------- | ------- | 
| 相对时间窗口内的传入点击 | 如果区段定义引用的事件不 **是** 在最 **近七天的时间段内**。 例如，在过去 **两周内**。 |
| 指相对窗口中的用户档案的传入点击 | 以下选项将不 **支持** 流分段：<ul><li>未在最 **后** 七 **天内到达的事件**。</li><li>包括Adobe Audience Manager(AAM)区段或特征的区段定义。</li></ul> |
| 引用事件的多个用户档案 | 以下选项将不 **支持** 流分段：<ul><li>在过去24 **小时** 内 **不发生的事件**。</li><li>包括Adobe Audience Manager(AAM)区段或特征的区段定义。</li></ul> |
| 多实体查询 | 整体而言，多实体查询不 **受流** 分段支持。 |

此外，执行流分段时还会应用一些准则：

| 查询类型 | 准则 |
| ---------- | -------- |
| 单事件查询 | 回顾窗限于 **七天**。 |
| 查询事件历史 | <ul><li>回顾窗限于一 **天**。</li><li>事件之间必 **须存** 在严格的时间排序条件。</li><li>只允许在事件之间进行简单的时间排序（前后）。</li><li>不能否定 **个别事件** 。 但是，整个查询 **可以** 被否定。</li></ul> |

## 检索支持流式分段的所有细分

您可以通过向端点发出列表请求，检索IMS组织内启用流分段的所有区段的GET `/segment/definitions` 。

**API格式**

要检索支持流的区段，必须在请求路径中 `evaluationInfo.continuous.enabled=true` 包含查询参数。

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
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回IMS组织中启用流分段的一组区段。

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
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
            "imsOrgId": "{IMS_ORG_ID}",
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

## 创建支持流的细分

如果区段与上面列出的流分段类型之一匹配，则该区段将 [自动启用流化](#streaming-segmentation-query-types)。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
>这是标准的“创建区段”请求。 有关创建区段定义的详细信息，请阅读有关创建区段 [的教程](../tutorials/create-a-segment.md)。

**响应**

成功的响应会返回新创建的支持流的段定义的详细信息。

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{IMS_ORG}",
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

启用流评估后，必须创建基线（在此之后，区段将始终保持最新）。 必须首先启用计划评估（也称为计划分段），系统才能自动执行基线设置。 通过计划的细分，您的IMS组织可以遵守循环计划，自动运行导出作业以评估细分。

>[!NOTE]
>
>对于最多五(5)个合并策略的沙箱，可启用计划评估 [!DNL XDM Individual Profile]。 如果您的组织在单个沙箱环境内 [!DNL XDM Individual Profile] 有五个以上的合并策略，您将无法使用计划的评估。

### 创建计划

通过向端点发出POST请 `/config/schedules` 求，您可以创建计划并包含应触发计划的特定时间。

**API格式**

```http
POST /config/schedules
```

**请求**

以下请求根据有效负荷中提供的规范创建新计划。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | **(必需** )计划名称。 必须是字符串。 |
| `type` | **（必需）** 字符串格式的作业类型。 支持的类型有 `batch_segmentation` 和 `export`。 |
| `properties` | **(必需** )包含与计划相关的其他属性的对象。 |
| `properties.segments` | **(等于时需`type`要)`batch_segmentation`使用** , `["*"]` 确保包括所有区段。 |
| `schedule` | **（必需）** 包含作业计划的字符串。 作业只能计划每天运行一次，这意味着在24小时内不能将作业计划为多次运行。 显示的示例(`0 0 1 * * ?`)表示作业每天在1:00:00 UTC时触发。 有关详细信息，请查阅 [cron表达式格式](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 文档。 |
| `state` | *（可选）包含计划状态的字符串* 。 可用值： `active` 和 `inactive`。 默认值为 `inactive`。IMS组织只能创建一个计划。 更新计划的步骤将在本教程的稍后部分提供。 |

**响应**

成功的响应会返回新创建计划的详细信息。

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
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

### 启用计划

默认情况下，创建计划时，处于非活动状 `state` 态，除非属性在 `active` create(POST)请求主体中设置为。 您可以通过向端点发出计划请求并在路 `state` 径中包含PATCH的ID，来启 `active``/config/schedules` 用计划（将设置为）。

**API格式**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**请求**

以下请求使 [用JSON修补程](http://jsonpatch.com/) 序格式，以将 `state` 计划更新为 `active`。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的更新返回空的响应正文和HTTP状态204（无内容）。

同一操作可用于禁用计划，方法是将上一个请求中的“值”替换为“非活动”。

## 后续步骤

现在，您已经为流式分段启用了新区段和现有区段，并启用了计划分段以开发基线和执行重复评估，因此您可以开始为组织创建区段。

要了解如何使用Adobe Experience Platform用户界面执行类似操作和处理区段，请访 [问区段生成器用户指南](../ui/segment-builder.md)。
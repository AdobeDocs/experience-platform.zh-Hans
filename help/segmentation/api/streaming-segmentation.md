---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 流细分
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# 使用流细分（测试版）实时评估事件

>[!NOTE] 流细分是测试版功能，可应要求提供。

流细分(也称为连续查询评估)是指在事件进入特定细分组后立即对客户进行评估的能力。 借助此功能，当数据传递到Adobe Experience Platform时，大多数细分规则现在都可以评估，这意味着，细分会员资格将保持最新状态，而无需运行计划的细分作业。

![](../images/api/streaming-segment-evaluation.png)

## 入门指南

本开发人员指南需要了解与流细分相关的各种Adobe Experience Platform服务。 在开始本教程之前，请查看以下服务的相关文档：

- [实时客户用户档案](../../profile/home.md):根据来自多个来源的汇总数据实时提供统一的消费者用户档案。
- [细分](../home.md):提供根据实时客户用户档案数据创建细分和受众的能力。
- [体验数据模型(XDM)](../../xdm/home.md):平台通过标准化框架组织客户体验数据。

以下各节提供了成功调用平台API所需了解的其他信息。

### 读取示例API调用

此开发人员指南提供示例API调用，以演示如何设置请求的格式。 这些包括路径、必需的标题和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅Experience Platform疑难解答指南 [中有关如何阅读示例API调用的部分](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集所需标题的值

要调用平台API，您必须首先完成身份验证 [教程](../../tutorials/authentication.md)。 完成身份验证教程后，将为所有Experience Platform API调用中的每个所需标头提供值，如下所示：

- 授权：承载人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有资源都与特定虚拟沙箱隔离。 对平台API的所有请求都需要一个标头，它指定操作将在以下位置进行的沙箱的名称：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 有关平台中沙箱的详细信息，请参阅沙 [箱概述文档](../../sandboxes/home.md)。

所有包含有效负荷(POST、PUT、PATCH)的请求都需要额外的标头：

- 内容类型：application/json

完成特定请求可能需要其他标题。 此文档中的每个示例中都显示正确的标题。 请特别注意示例请求，以确保包含所有必需的标题。

### 支持流式细分的查询类型

下表列表了不同类型的分段查询，以及它们是否支持流分段。

| 查询类型 | 示例查询 | 支持流细分 |
| ---------- | ------------ | --------------------------------- |
| 简单的人口统计 | “把所有住址在加拿大的人都给我。” | 支持 |
| 时间序列事件 | “给我所有下载Lightroom的人。” | 支持 |
| 人口统计和时间序列 | “把所有住在加拿大的人交给我，他们在过去30天里下了订单。” | 支持 |
| 缺乏事件 | &quot;把两天内放弃两辆单车的人都交给我。&quot; | 支持 |
| 多实体 | “给我所有权利类型为‘有经验’的人。” | 不受支持 |
| 高级PQL功能 | “请向我提供上周下订单的所有用户档案，并包含所有已购买产品的SKU和名称。” | 不受支持 |

## 检索所有支持流细分的细分

在创建新的支持流的区段或更新要启用流的现有区段之前，您应确保不会通过检索所有支持流的区段的列表来复制信息。

**API格式**

要检索支持流式播放的区段，您必须在请求路径中 `evaluationInfo.continuous.enabled=true` 包含查询参数。

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
  -H 'x-sandbox-name: {SANDBOX_NAME'
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

## 创建支持流的区段

确认要创建的区段尚不存在后，您可以创建已启用流式分段的新区段。

**API格式**

```http
POST /segment/definitions
```

**请求**

以下请求将创建启用流分段的新区段。 Note that the `continuous` section is set to `enabled: true`.

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

>[!NOTE] 这是标准的“创建区段”请求，其中将部分的已添 `continuous` 加参数设置为 `enabled: true`。 有关创建区段定义的详细信息，请阅读有关区段创建 [的文档](../tutorials/create-a-segment.md)。

**响应**

成功的响应会返回新创建的支持流式播放的区段定义的详细信息。

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

## 启用现有细分以实现流细分

您可以通过在PATCH请求的路径中提供区段定义的ID来启用现有区段以进行流式分段。 此外，此PATCH请求的有效负荷必须包含现有区段定义的完整详细信息，可通过向相关区段定义发出GET请求来访问该定义。

### 查找现有的区段定义

要查找现有的区段定义，您必须在GET请求的路径中提供其ID。

**API格式**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | 要查找的区段定义的ID。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回您请求的区段定义的详细信息。

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "sandbox": {
        "sandboxId": "",
        "sandboxName": "",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    }
}
```

>[!NOTE] 对于下一个请求，您需要在此响应中返回的区段定义的完整详细信息。 请复制此答复的详细信息，以便在下一个请求正文中使用。

### 启用现有细分以实现流细分

现在，您了解了要更新的区段的详细信息，可以执行PATCH请求以更新区段以启用流分段。

**API格式**

```http
PATCH /segment/definitions/{SEGMENT_DEFINITION_ID}
```

**请求**

以下请求的有效负荷提供段定义的详细信息(在上一步 [中获取](#look-up-an-existing-segment-definition))，并通过将其属性更改为来更新 `continuous.enabled` 它 `true`。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -d '{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
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

**响应**

成功的响应会返回新更新的区段定义的详细信息。

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "4A21D36B544916100A4C98A7@AdobeOrg",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
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
    },
    "creationTime": 1572029711000,
    "updateEpoch": 1572029712000,
    "updateTime": 1572029712000
}
```

## 启用计划评估

启用流评估后，必须创建基线（在此之后，区段将始终保持最新）。 这由系统自动完成，但必须首先启用计划评估（也称为计划分段）才能进行基准化。

通过计划的细分，IMS组织可以创建循环计划，以自动运行导出作业以评估细分。

>[!NOTE] 对于沙箱，对于XDM单个用户档案最多可以启用五(5)个合并策略的计划评估。 如果您的组织在单个沙箱环境中有五个以上的XDM单个用户档案合并策略，您将无法使用计划的评估。

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
| `name` | **（必需）** “计划”的名称。 必须为字符串。 |
| `type` | **（必需）** ，以字符串格式表示的作业类型。 支持的类型有 `batch_segmentation` 和 `export`。 |
| `properties` | **（必需）** ，包含与计划相关的其他属性的对象。 |
| `properties.segments` | **(等于时需`type`要)`batch_segmentation`** “使用” `["*"]` 可确保包括所有区段。 |
| `schedule` | **（必需）** ，包含作业计划的字符串。 作业只能计划为每天运行一次，这意味着您不能将作业计划为在24小时内运行多次。 显示的示例(`0 0 1 * * ?`)是指每天1:00:00 UTC时触发作业。 有关详细信息，请查看cron [表达式格式文档](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 。 |
| `state` | *（可选）包含计划状态的字符串* 。 可用值： `active` 和 `inactive`。 默认值为 `inactive`。IMS组织只能创建一个计划。 更新计划的步骤将在本教程的稍后部分提供。 |

**响应**

成功的响应会返回新创建的计划的详细信息。

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

默认情况下，计划在创建时处于非活动状态，除非 `state` 在create(POST)请 `active` 求主体中将该属性设置为。 您可以通过向端点发出PATCH请求并在路径中包含计划的ID来启 `state``active``/config/schedules` 用计划（设置为）。

**API格式**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**请求**

以下请求使用 [JSON修补程序格式](http://jsonpatch.com/) ，以将计划 `state` 的更新为 `active`。

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

成功的更新将返回空的响应正文和HTTP状态204（无内容）。

同一操作可用于禁用计划，方法是将上一个请求中的“value”替换为“inactive”。

## 后续步骤

现在，您已经为流细分启用了新细分和现有细分，并启用了计划细分以开发基准并执行重复评估，您可以开始为组织创建细分。

要了解如何使用Adobe Experience Platform用户界面执行类似操作和处理区段，请访问 [Segment Builder用户指南](../ui/overview.md)。
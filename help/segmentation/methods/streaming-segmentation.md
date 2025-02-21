---
solution: Experience Platform
title: 流式分段指南
description: 了解流式分段，包括内容、如何创建使用流式分段评估的受众，以及如何查看使用流式分段创建的受众。
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: 3f0cfd6c36344f481751bf05236df4fb288eab60
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 1%

---

# 流式分段指南

流式分段是在关注数据丰富性的同时，近乎实时地评估Adobe Experience Platform中的受众的能力。

借助流式分段，现在可以在流式数据进入Platform时进行受众鉴别，从而消除计划和运行分段作业的需求。 这样，您就可以在数据传递到Platform时对其进行评估，从而使受众成员资格自动保持最新。

## 符合条件的查询类型 {#query-types}

如果查询符合下表所列的任何标准，则它有资格进行流式分段。

>[!NOTE]
>
>为了使流式分段正常工作，您需要为组织启用计划分段。 有关启用计划分段的详细信息，请参阅[受众门户概述](../ui/audience-portal.md#scheduled-segmentation)。

| 查询类型 | 详细信息 | 查询 | 示例 |
| ---------- | ------- | ----- | ------- |
| 小于24小时时间范围内的单个事件 | 任何涉及少于24小时时间范围内的单个传入事件的区段定义。 | `CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![显示相对时间范围内单个事件的示例。](../images/methods/streaming/single-event.png) |
| 仅配置文件 | 仅引用配置文件属性的任何区段定义。 | `homeAddress.country.equals("US", false)` | ![显示的配置文件属性示例。](../images/methods/streaming/profile-attribute.png) |
| 在相对时间范围小于24小时内的配置文件属性为单个事件 | 任何涉及单个传入事件（具有一个或多个用户档案属性）且发生在小于24小时的相对时间范围内的区段定义。 | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![显示相对时间范围内具有配置文件属性的单个事件的示例。](../images/methods/streaming/single-event-with-profile-attribute.png) |
| 区段划分 | 包含一个或多个批次或流式客户细分的任何客户细分定义。 **注意：**&#x200B;如果使用区段区段，则每24小时&#x200B;**将发生配置文件取消资格**。 | `inSegment("a730ed3f-119c-415b-a4ac-27c396ae2dff") and inSegment("8fbbe169-2da6-4c9d-a332-b6a6ecf559b9")` | ![将显示区段示例。](../images/methods/streaming/segment-of-segments.png) |
| 具有配置文件属性的多个事件 | 任何在过去24小时&#x200B;**内引用多个事件**&#x200B;且（可选）具有一个或多个配置文件属性的区段定义。 | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("directMarketing.emailClicked", false)) WHEN(today), C1: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![显示具有配置文件属性的多个事件的示例。](../images/methods/streaming/multiple-events-with-profile-attribute.png) |

在以下情况下，区段定义&#x200B;**将不符合流式分段条件**：

- 区段定义包括Adobe Audience Manager (AAM)区段或特征。
- 区段定义包括多个实体（多实体查询）。
- 区段定义包含单个事件和`inSegment`事件的组合。
   - 但是，如果`inSegment`事件中包含的区段定义仅为配置文件，则区段定义&#x200B;**将**&#x200B;启用流式分段。
- 区段定义使用“忽略年份”作为其时间限制的一部分。

请注意以下适用于流式分段查询的准则：

| 查询类型 | 指南 |
| ---------- | -------- |
| 单个事件查询 | 回顾窗口没有限制。 |
| 使用事件历史记录进行查询 | <ul><li>回看窗口限制为&#x200B;**一天**。</li><li>事件之间存在严格的时间排序条件&#x200B;**必须**。</li><li>支持至少具有一个否定事件的查询。 但是，整个事件&#x200B;**不能**&#x200B;是否定。</li></ul> |

如果修改了区段定义以使其不再满足流式分段标准，则区段定义将自动从“流式处理”切换到“批处理”。

此外，区段取消资格（与区段资格类似）是实时发生的。 因此，如果受众不再符合区段的条件，则将被立即取消资格。 例如，如果区段定义要求“过去三小时内购买红鞋的所有用户”，则在三小时后，最初符合区段定义条件的所有用户档案都将被取消资格。

## 创建受众 {#create-audience}

您可以创建通过使用分段服务API或通过UI中的受众门户使用流式分段进行评估的受众。

如果区段定义与[符合条件的查询类型](#eligible-query-types)之一匹配，则可以启用流式处理。

>[!BEGINTABS]

>[!TAB 分段服务API]

**API格式**

```http
POST /segment/definitions
```

**请求**

+++ 用于创建已启用流式分段区段定义的示例请求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People in the USA",
        "description: "An audience that looks for people who live in the USA",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "homeAddress.country = \"US\""
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
        "schema": {
            "name": "_xdm.context.profile"
        }
     }'
```

+++

**响应**

成功的响应会返回HTTP状态200以及新创建的区段定义的详细信息。

+++创建区段定义时的示例响应。

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People in the USA",
    "description": "An audience that looks for people who live in the USA",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "homeAddress.country = \"US\""
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
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

+++

有关使用此端点的详细信息，请参阅[区段定义端点指南](../api/segment-definitions.md)。

>[!TAB 受众门户]

在受众门户中，选择&#x200B;**[!UICONTROL 创建受众]**。

![受众门户中突出显示“创建受众”按钮。](../images/methods/streaming/select-create-audience.png)

此时会出现弹出窗口。 选择&#x200B;**[!UICONTROL 生成规则]**&#x200B;以进入区段生成器。

![在“创建受众”弹出框中突出显示“生成规则”按钮。](../images/methods/streaming/select-build-rules.png)

在区段生成器中，创建与[符合条件的查询类型](#eligible-query-types)之一匹配的区段定义。 如果区段定义符合流式分段条件，您将能够选择&#x200B;**[!UICONTROL 流式处理]**&#x200B;作为&#x200B;**[!UICONTROL 评估方法]**。

![将显示区段定义。 评估类型已突出显示，显示可以使用流式分段评估区段定义。](../images/methods/streaming/streaming-evaluation-method.png)

要了解有关创建区段定义的更多信息，请参阅[区段生成器指南](../ui/segment-builder.md)

>[!ENDTABS]

## 检索受众 {#retrieve-audiences}

您可以使用分段服务API或通过UI中的受众门户检索使用流式分段评估的所有受众。

>[!BEGINTABS]

>[!TAB 分段服务API]

通过向`/segment/definitions`端点发出GET请求，检索使用组织内的流式分段评估的所有区段定义的列表。

**API格式**

您必须在请求路径中包含查询参数`evaluationInfo.synchronous.enabled=true`，以检索使用流式分段评估的区段定义。

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**请求**

+++ 列出所有支持流的区段定义的请求示例

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应会返回HTTP状态200，其中包含组织中启用流式分段的一系列区段定义。

+++一个示例响应，其中包含贵组织中所有支持流式客户细分的区段定义的列表

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

有关返回的区段定义的更多详细信息可在[区段定义终结点指南](../api/segment-definitions.md)中找到。

+++

>[!TAB 受众门户]

您可以使用受众门户中的过滤器，检索组织中支持流式分段的所有受众。 选择![筛选器图标](../../images/icons/filter.png)图标以显示筛选器列表。

![受众门户中突出显示了过滤器图标。](../images/methods/filter-audiences.png)

在可用筛选器内，转到&#x200B;**[!UICONTROL 更新频率]**&#x200B;并选择“[!UICONTROL 流式传输]”。 使用此过滤器可显示贵组织中通过流式分段评估的所有受众。

![选择了流式更新频率，显示组织中使用流式分段评估的所有受众。](../images/methods/streaming/filter-streaming.png)

若要了解有关在Platform中查看受众的更多信息，请阅读[受众门户指南](../ui/audience-portal.md)。

>[!ENDTABS]

## 受众详情 {#audience-details}

您可以在受众门户中选择使用流式分段评估的特定受众，以查看该受众的详细信息。

在Audience Portal中选择受众后，将显示受众详细信息页面。 该屏幕可显示有关受众的信息，包括受众详细信息摘要、一段时间内符合条件的配置文件数量以及受众激活到的目标。

![为使用流式分段评估的受众显示受众详细信息页面。](../images/methods/streaming/audience-details.png)

对于启用流处理的受众，将显示&#x200B;**[!UICONTROL 随时间变化的配置文件]**&#x200B;卡，其中显示符合条件的总量度和新受众更新的量度。

**[!UICONTROL 合格受众总数]**&#x200B;指标表示基于此受众的批次和流式评估的合格受众总数。

**[!UICONTROL 新受众已更新]**&#x200B;量度由一个折线图表示，该折线图显示通过流式分段而发生的受众规模变化。 您可以调整下拉菜单以显示过去24小时、上周或过去30天。

![已突出显示“随时间变化的配置文件”信息卡。](../images/methods/streaming/profiles-over-time.png)

有关受众详细信息的更多详细信息，请阅读[受众门户概述](../ui/audience-portal.md#audience-details)。

## 后续步骤

本指南介绍启用流的区段定义如何在Adobe Experience Platform上工作以及如何监测启用流的区段定义。

要了解有关使用Adobe Experience Platform用户界面的更多信息，请参阅[分段用户指南](./overview.md)。

有关流式客户细分的常见问题，请阅读常见问题解答](../faq.md#streaming-segmentation)的[流式客户细分部分。

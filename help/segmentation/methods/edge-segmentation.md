---
title: Edge Segmentation指南
description: 了解如何使用边缘分段在边缘即时评估Experience Platform中的受众，启用同一页面和下一页面个性化用例。
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 5de8597dd1d5249297a09976c804d1c1f3d822c5
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 1%

---

# 边缘分段指南

Edge分段功能能够在边缘[上即时评估Adobe Experience Platform中的区段定义](../../landing/edge-and-hub-comparison.md)，从而启用同一页面和下一页面个性化用例。

>[!IMPORTANT]
>
> 边缘数据将存储在距离收集位置最近的边缘服务器位置。 此数据也可以存储在指定为Adobe Experience Platform数据中心中心（或主体）以外的位置。
>
> 此外，边缘分段引擎将仅在具有&#x200B;**一个**&#x200B;主标记身份的边缘上处理请求，这与不基于边缘的主身份一致。

## Edge分段查询类型 {#query-types}

如果查询符合下表列出的任何标准，则可以使用边缘分段进行评估。

>[!NOTE]
>
>如果查询与下表中的任何查询类型匹配，则将使用边缘分段自动评估该查询。 系统会根据查询表达式自动确定此功能。
>
>此外，如果受众&#x200B;**仅**&#x200B;包含配置文件属性，则每天都将对其进行评估。 如果您希望实时评估受众，则需要将事件数据添加到受众。

| 查询类型 | 详细信息 | 查询 | 示例 |
| ---------- | ------- | ----- | ------- |
| 小于24小时时间范围内的单个事件 | 任何涉及少于24小时时间范围内的单个传入事件的区段定义。 | `CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![显示相对时间范围内单个事件的示例。](../images/methods/edge/single-event.png) |
| 仅配置文件 | 仅引用配置文件属性的任何区段定义。 | `homeAddress.country.equals("US", false)` | ![显示的配置文件属性示例。](../images/methods/edge/profile-attribute.png) |
| 在相对时间范围小于24小时内的配置文件属性为单个事件 | 任何涉及单个传入事件（具有一个或多个用户档案属性）且发生在小于24小时的相对时间范围内的区段定义。 | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![显示相对时间范围内具有配置文件属性的单个事件的示例。](../images/methods/edge/single-event-with-profile-attribute.png) |
| 区段划分 | 包含一个或多个批次或边缘区段的任意区段定义。 **注意：**&#x200B;如果使用区段区段，则每24小时&#x200B;**将发生配置文件取消资格**。 | `inSegment("a730ed3f-119c-415b-a4ac-27c396ae2dff") and inSegment("8fbbe169-2da6-4c9d-a332-b6a6ecf559b9")` | ![将显示区段示例。](../images/methods/edge/segment-of-segments.png) |

此外，区段定义&#x200B;**必须**&#x200B;绑定到边缘上活动的合并策略。 有关合并策略的更多信息，请参阅[合并策略指南](../../profile/api/merge-policies.md)。

在以下方案中，区段定义&#x200B;**不**&#x200B;适用于边缘分段：

- 区段定义包含单个事件和`inSegment`事件的组合。
   - 但是，如果`inSegment`事件中包含的区段定义仅为配置文件，则区段定义&#x200B;**将**&#x200B;启用边缘分段。
- 区段定义使用“忽略年份”作为其时间限制的一部分。

## 创建受众 {#create-audience}

您可以创建受众，该受众通过使用Segmentation Service API或通过UI中的受众门户使用边缘分段进行评估。

如果区段定义与[符合条件的查询类型](#eligible-query-types)之一，则可以启用边缘定义。

>[!BEGINTABS]

>[!TAB 分段服务API]

**API格式**

```http
POST /segment/definitions
```

**请求**

+++ 用于创建已启用边缘分段的区段定义的示例请求

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
                "enabled": false
            },
            "synchronous": {
                "enabled": true
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
            "enabled": false
        },
        "synchronous": {
            "enabled": true
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

![受众门户中突出显示“创建受众”按钮。](../images/methods/edge/select-create-audience.png)

此时会出现弹出窗口。 选择&#x200B;**[!UICONTROL 生成规则]**&#x200B;以进入区段生成器。

![在“创建受众”弹出框中突出显示“生成规则”按钮。](../images/methods/edge/select-build-rules.png)

在区段生成器中，创建与[符合条件的查询类型](#eligible-query-types)之一匹配的区段定义。 如果区段定义符合边缘分段条件，您将能够选择&#x200B;**[!UICONTROL Edge]**&#x200B;作为&#x200B;**[!UICONTROL 评估方法]**。

![将显示区段定义。 评估类型已突出显示，显示可以使用边缘分段评估区段定义。](../images/methods/edge/edge-evaluation-method.png)

要了解有关创建区段定义的更多信息，请参阅[区段生成器指南](../ui/segment-builder.md)

>[!ENDTABS]

## 检索使用边缘分段评估的受众 {#retrieve-audiences}

您可以在UI中使用分段服务API或通过Audience Portal检索使用边缘分段评估的所有受众。

>[!BEGINTABS]

>[!TAB 分段服务API]

通过向`/segment/definitions`端点发出GET请求，检索使用组织内边缘分段评估的所有区段定义的列表。

**API格式**

必须在请求路径中包含查询参数`evaluationInfo.synchronous.enabled=true`，以检索使用边缘分段评估的区段定义。

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**请求**

+++ 列出所有启用边缘的区段定义的请求示例

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**响应**

成功的响应会返回HTTP状态200，其中包含组织中启用了边缘分段的一系列区段定义。

+++ 包含组织中所有启用了边缘分段区段定义的列表的示例响应

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
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
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
                    "enabled": false
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
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

您可以使用受众门户中的过滤器，检索组织中为边缘分段启用的所有受众。 选择![筛选器图标](../../images/icons/filter.png)图标以显示筛选器列表。

![受众门户中突出显示了过滤器图标。](../images/methods/filter-audiences.png)

在可用筛选器内，转到&#x200B;**更新频率**&#x200B;并选择“Edge”。 使用此过滤器可显示贵组织中使用边缘分段评估的所有受众。

![已选择Edge更新频率，显示组织中使用边缘分段评估的所有受众。](../images/methods/edge/filter-edge.png)

要了解有关在Experience Platform中查看受众的更多信息，请阅读[受众门户指南](../ui/audience-portal.md)。

>[!ENDTABS]

## 受众详情 {#audience-details}

通过在受众门户中选择边缘分段，您可以查看使用边缘分段评估的特定受众的详细信息。

在Audience Portal中选择受众后，将显示受众详细信息页面。 该屏幕可显示有关受众的信息，包括受众详细信息摘要、一段时间内符合条件的配置文件数量以及受众激活到的目标。

![对于使用边缘分段评估的受众，将显示受众详细信息页面。](../images/methods/edge/audience-details.png)

对于启用Edge的受众，将显示&#x200B;**[!UICONTROL 随时间变化的配置文件]**&#x200B;信息卡，其中显示符合条件的总量度和新受众更新的量度。

**[!UICONTROL 合格受众总数]**&#x200B;指标表示基于此受众的边缘评估的合格受众总数。

**[!UICONTROL 新受众已更新]**&#x200B;量度由一个折线图表示，该折线图显示通过边缘分段所发生的受众规模变化。 您可以调整下拉菜单以显示过去24小时、上周或过去30天。

![已突出显示“随时间变化的配置文件”信息卡。](../images/methods/edge/profiles-over-time.png)

有关受众详细信息的更多详细信息，请阅读[受众门户概述](../ui/audience-portal.md#audience-details)。

## 后续步骤

本指南介绍什么是边缘分段，以及如何创建可使用Adobe Experience Platform上的边缘分段评估的区段定义。

要了解有关使用Experience Platform用户界面的更多信息，请参阅[分段用户指南](./overview.md)。

有关边缘分段的常见问题解答，请阅读常见问题解答[的](../faq.md#edge-segmentation)边缘分段部分。


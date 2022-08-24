---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；边缘分段；边缘分段；流式边缘；
solution: Experience Platform
title: '使用API进行边缘分段 '
topic-legacy: developer guide
description: 本文档包含有关如何将边缘分段与Adobe Experience Platform Segmentation Service API结合使用的示例。
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: de63939c44b338bb9632a57c74c095135f023d50
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 0%

---

# 边缘分割

>[!NOTE]
>
>以下文档说明了如何使用API执行边缘分段。 有关使用UI执行边缘分段的信息，请阅读 [边缘分段UI指南](../ui/edge-segmentation.md).
>
>现在，边缘分段通常可供所有Platform用户使用。 如果您在测试期间创建了边缘区段，则这些区段将继续可操作。

边缘分段功能可以即时在边缘上评估Adobe Experience Platform中的区段，从而实现同一页面和下一页面的个性化用例。

>[!IMPORTANT]
>
> 边缘数据将存储在与收集位置最接近的边缘服务器位置，并且可能存储在指定为中心（或主体）Adobe Experience Platform数据中心的位置以外的位置。
>
> 此外，边缘分段引擎将仅执行存在的边缘上的请求 **one** 主标记标识，与非基于边缘的主标识一致。

## 快速入门

本开发人员指南需要对 [!DNL Adobe Experience Platform] 与边缘分段相关的服务。 在开始本教程之前，请查阅以下服务的文档：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的消费者用户档案。
- [[!DNL Segmentation]](../home.md):提供从 [!DNL Real-time Customer Profile] 数据。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):标准化框架， [!DNL Platform] 组织客户体验数据。

要成功调用任何Experience PlatformAPI端点，请阅读 [Platform API快速入门](../../landing/api-guide.md) 以了解所需的标头以及如何读取示例API调用。

## 边缘分段查询类型 {#query-types}

要使用边缘分段来评估区段，查询必须符合以下准则：

| 查询类型 | 详细信息 | 示例 | PQL示例 |
| ---------- | ------- | ------- | ----------- |
| 单个事件 | 任何引用无时间限制的单个传入事件的区段定义。 | 向购物车中添加了商品的用户。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 单个用户档案 | 任何引用单个仅限用户档案属性的区段定义 | 住在美国的人。 | `homeAddress.countryCode = "US"` |
| 引用用户档案的单个事件 | 引用一个或多个用户档案属性以及无时间限制的单个传入事件的任何区段定义。 | 访问主页的美国人。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 使用配置文件属性否定单个事件 | 任何引用否定的单个传入事件和一个或多个用户档案属性的区段定义 | 在美国生活并拥有 **not** 访问主页。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| 一个时间范围内的单个事件 | 引用指定时间段内单个传入事件的任何区段定义。 | 过去24小时内访问主页的人员。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)])` |
| 时间窗口内具有配置文件属性的单个事件 | 引用一个或多个用户档案属性以及设置时间段内单个传入事件的任何区段定义。 | 过去24小时内访问主页的美国人。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)])` |
| 在时间窗口内使用配置文件属性否定单个事件 | 指一段时间内一个或多个用户档案属性以及否定的单个传入事件的任何区段定义。 | 在美国生活并拥有 **not** 在过去24小时内访问了主页。 | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)]))` |
| 24小时时间范围内的频度事件 | 任何区段定义，指在24小时内发生一定次数的事件。 | 访问主页的人员 **至少** 过去24小时里五次。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小时时间范围内具有用户档案属性的频率事件 | 任何区段定义，指一个或多个用户档案属性以及在24小时内发生一定次数的事件。 | 访问主页的美国人 **至少** 过去24小时里五次。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小时的时间范围内使用用户档案否定频率事件 | 任何区段定义，指一个或多个用户档案属性以及在24小时的时间范围内发生一定次数的否定事件。 | 未访问主页的人员 **更多** 超过5次。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| 在24小时的时间配置文件内多次传入的点击 | 指在24小时内发生的多个事件的任何区段定义。 | 访问主页的人员 **或** 在过去24小时内访问了结帐页面。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 在24小时的时间范围内使用用户档案进行多个事件 | 任何区段定义，指在24小时内发生的一个或多个用户档案属性和多个事件。 | 访问主页的美国人 **和** 在过去24小时内访问了结帐页面。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 区段 | 包含一个或多个批处理或流式处理区段的任何区段定义。 | 居住在美国且位于区段“现有区段”中的人员。 | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| 引用映射的查询 | 引用属性映射的任何区段定义。 | 基于外部区段数据添加到购物车的人员。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

此外，区段 **必须** 绑定到边缘上处于活动状态的合并策略。 有关合并策略的更多信息，请阅读 [合并策略指南](../../profile/api/merge-policies.md).

## 检索为边缘分段启用的所有区段

您可以通过向 `/segment/definitions` 端点。

**API格式**

要检索为边缘分段启用的区段，必须包含查询参数 `evaluationInfo.synchronous.enabled=true` 在请求路径中。

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回IMS组织中为边缘分段启用的区段数组。 有关返回的区段定义的更多详细信息，请参阅 [segment definitions endpoint buide](./segment-definitions.md).

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

## 创建已启用边缘分段的区段

您可以通过向 `/segment/definitions` 与其中一个 [上面列出的边缘分段查询类型](#query-types).

**API格式**

```http
POST /segment/definitions
```

**请求**

>[!NOTE]
>
>以下示例是创建区段的标准请求。 有关创建区段定义的更多信息，请阅读 [创建区段](../tutorials/create-a-segment.md).

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

**响应**

成功的响应会返回新创建的用于边缘分段的区段定义的详细信息。

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
        "value": "chain(xEvent, timestamp, [X: WHAT(var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = "true")])"
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
```

## 后续步骤

现在，您已了解如何创建启用了边缘分段的区段，接下来可以使用这些区段来启用同页和下一页个性化用例。

要了解如何使用Adobe Experience Platform用户界面执行类似操作和处理区段，请访问 [区段生成器用户指南](../ui/segment-builder.md).

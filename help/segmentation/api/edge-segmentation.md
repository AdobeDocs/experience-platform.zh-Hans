---
solution: Experience Platform
title: 使用API的边缘分段
description: 本文档包含有关如何将边缘分段与Adobe Experience Platform分段服务API一起使用的示例。
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: d3c0e5ed596661f11191bbcd8d51c888bbd4c1d2
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 1%

---

# 边缘分段

>[!NOTE]
>
>以下文档介绍了如何使用API执行边缘分段。 有关使用UI执行边缘分段的信息，请阅读 [边缘分段UI指南](../ui/edge-segmentation.md).
>
>现在，边缘分段已普遍适用于所有Platform用户。 如果您在测试版中创建了边缘区段定义，则这些区段定义将继续有效。

边缘分段能够在边缘即时评估Adobe Experience Platform中的区段定义，启用同一页面和下一页面个性化用例。

>[!IMPORTANT]
>
> 边缘数据将存储在距离收集位置最近的边缘服务器位置，并且可能会存储在指定为Adobe Experience Platform数据中心中心（或主体）的位置以外的位置。
>
> 此外，边缘分段引擎将仅处理存在以下条件的边缘上的请求： **一** 主标记身份，与不基于edge的主身份一致。

## 快速入门

本开发人员指南要求您实际了解各种 [!DNL Adobe Experience Platform] 边缘分段涉及的服务。 在开始本教程之前，请查看以下服务的文档：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根据来自多个来源的汇总数据，实时提供统一的用户用户档案。
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md)：允许您从构建受众 [!DNL Real-Time Customer Profile] 数据。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Platform] 组织客户体验数据。

要成功调用任何Experience PlatformAPI端点，请阅读以下指南： [Platform API快速入门](../../landing/api-guide.md) 了解所需的标头以及如何读取示例API调用。

## 边缘分段查询类型 {#query-types}

为了使用边缘分段来评估区段，查询必须遵循以下准则：

| 查询类型 | 详细信息 | 示例 | PQL示例 |
| ---------- | ------- | ------- | ----------- |
| 单个事件 | 任何引用没有时间限制的单个传入事件的区段定义。 | 将项目添加到购物车的人员。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 单个配置文件 | 任何引用单个纯配置文件属性的区段定义 | 住在美国的人。 | `homeAddress.countryCode = "US"` |
| 引用用户档案的单个事件 | 任何引用一个或多个用户档案属性和单个传入事件的区段定义，无时间限制。 | 在美国居住的人访问了该主页。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 否定了具有配置文件属性的单个事件 | 任何引用带反义的单个传入事件和一个或多个用户档案属性的区段定义 | 居住在美国并且拥有 **非** 访问了主页。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| 时间范围内的单个事件 | 任何引用一段时间内单个传入事件的区段定义。 | 过去24小时内访问过主页的人。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)])` |
| 在相对时间范围小于24小时内的配置文件属性为单个事件 | 任何涉及单个传入事件（具有一个或多个用户档案属性）且发生在小于24小时的相对时间范围内的区段定义。 | 居住在美国的人在过去24小时内访问了该主页。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)])` |
| 在一个时间范围内否定了具有配置文件属性的单个事件 | 任何引用一段时间内一个或多个用户档案属性和否定单个传入事件的区段定义。 | 居住在美国并且拥有 **非** 在过去24小时内访问了主页。 | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)]))` |
| 24小时时间范围内的频率事件 | 任何涉及在24小时的时间范围内发生特定次数的事件的区段定义。 | 访问过主页的人 **至少** 过去24小时内5次。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小时时间范围内具有配置文件属性的频率事件 | 任何区段定义，它是指一个或多个用户档案属性以及在24小时的时间范围内发生特定次数的事件。 | 访问主页的美国人 **至少** 过去24小时内5次。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小时时间范围内具有配置文件的否定频率事件 | 任何引用一个或多个用户档案属性的区段定义，以及在24小时的时间范围内发生特定次数的否定事件。 | 未访问过主页的人 **更多** 超过五次。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| 24小时时间配置文件内的多个传入点击 | 任何涉及在24小时的时间范围内发生的多个事件的区段定义。 | 访问主页的人 **或** 在过去24小时内访问了结账页面。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 一个配置文件在24小时时间范围内的多个事件 | 任何区段定义，它是指在24小时的时间范围内发生的一个或多个用户档案属性和多个事件。 | 访问主页的来自美国的人员 **和** 在过去24小时内访问了结账页面。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 区段划分 | 包含一个或多个批次或流式客户细分的任何客户细分定义。 | 居住在美国、属于“现有区段”的人群。 | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| 引用映射的查询 | 任何引用属性映射的区段定义。 | 根据外部区段数据添加到购物车的人员。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

此外，区段 **必须** 绑定到在Edge上处于活动状态的合并策略。 有关合并策略的更多信息，请参阅 [合并策略指南](../../profile/api/merge-policies.md).

区段定义将 **非** 在以下情况下启用边缘分段：

- 区段定义包括单个事件和 `inSegment` 事件。
   - 然而，倘分部包含在 `inSegment` 事件仅用于配置文件，区段定义 **将** 启用边缘分段。

## 检索为边缘分段启用的所有区段

您可以通过对以下网站发出GET请求，检索您的组织中启用了边缘分段的所有区段的列表： `/segment/definitions` 端点。

**API格式**

要检索为边缘分段启用的区段，您必须包括查询参数 `evaluationInfo.synchronous.enabled=true` 在请求路径中。

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

成功的响应会返回组织中启用了边缘分段的一系列区段。 有关返回的区段定义的更多详细信息，请参阅 [区段定义端点指南](./segment-definitions.md).

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

## 创建启用边缘分段的区段

您可以通过对以下对象发出POST请求，创建启用边缘分段的分段： `/segment/definitions` 与以下项之一匹配的端点： [上面列出的边缘分段查询类型](#query-types).

**API格式**

```http
POST /segment/definitions
```

**请求**

>[!NOTE]
>
>以下示例是创建区段的标准请求。 有关创建区段定义的更多信息，请阅读以下教程： [创建区段](../tutorials/create-a-segment.md).

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
            "enabled": false
        },
        "synchronous": {
            "enabled": true
        }
    }
}'
```

**响应**

成功的响应会返回为边缘分段启用的新创建区段定义的详细信息。

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

现在，您已了解如何创建支持边缘分段的区段，接下来可以使用它们启用同一页面和下一页面个性化用例。

要了解如何使用Adobe Experience Platform用户界面执行类似操作和处理区段，请访问 [区段生成器用户指南](../ui/segment-builder.md).

## 附录

以下部分列出了有关边缘分段的常见问题解答：

### 区段在Edge Network上可用需要多长时间？

在Edge Network上提供一个区段最多需要一小时。
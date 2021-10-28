---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；边缘分段；边缘分段；流式边缘；
solution: Experience Platform
title: '使用API进行边缘分段 '
topic-legacy: developer guide
description: 本文档包含有关如何将边缘分段与Adobe Experience Platform Segmentation Service API结合使用的示例。
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: 4d2c6385decd5b789a975165a87bc80f9b008cd7
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 2%

---

# Edge segmentation (beta)

>[!NOTE]
>
>The following document states how to perform edge segmentation using the API. 有关使用UI执行边缘分段的信息，请阅读 [边缘分段UI指南](../ui/edge-segmentation.md). 此外，边缘分段当前为测试版。 文档和功能可能会发生变化。

边缘分段功能可以即时在边缘上评估Adobe Experience Platform中的区段，从而实现同一页面和下一页面的个性化用例。

## 快速入门

本开发人员指南需要对 [!DNL Adobe Experience Platform] 与边缘分段相关的服务。 在开始本教程之前，请查阅以下服务的文档：

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Provides a unified consumer profile in real-time, based on aggregated data from multiple sources.
- [[!DNL Segmentation]](../home.md):提供从 [!DNL Real-time Customer Profile] 数据。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):标准化框架， [!DNL Platform] 组织客户体验数据。

要成功调用任何Experience PlatformAPI端点，请阅读 [Platform API快速入门](../../landing/api-guide.md) 以了解所需的标头以及如何读取示例API调用。

## Edge segmentation query types {#query-types}

要使用边缘分段来评估区段，查询必须符合以下准则：

| Query type | 详细信息 | 示例 |
| ---------- | ------- | ------- |
| Single event | 任何引用无时间限制的单个传入事件的区段定义。 | 向购物车中添加了商品的用户。 |
| 引用用户档案的单个事件 | 引用一个或多个用户档案属性以及无时间限制的单个传入事件的任何区段定义。 | 访问主页的美国人。 |
| Negated single event with a profile attribute | Any segment definition that refers to a negated single incoming event and one or more profile attributes | 在美国生活并拥有 **not** 访问主页。 |
| 在24小时的时间范围内单个事件 | 在24小时内引用单个传入事件的任何区段定义。 | 过去24小时内访问主页的人员。 |
| 在24小时的时间范围内具有配置文件属性的单个事件 | 在24小时内引用一个或多个用户档案属性以及否定的单个传入事件的任何区段定义。 | People who live in the USA that visited the homepage in the last 24 hours. |
| 在24小时的时间范围内使具有配置文件属性的单个事件失效 | 在24小时内引用一个或多个用户档案属性以及否定的单个传入事件的任何区段定义。 | 在美国生活并拥有 **not** 在过去24小时内访问了主页。 |
| 24小时时间范围内的频度事件 | 任何区段定义，指在24小时内发生一定次数的事件。 | 访问主页的人员 **至少** 过去24小时里五次。 |
| Frequency event with a profile attribute within a 24-hour time window | 任何区段定义，指一个或多个用户档案属性以及在24小时内发生一定次数的事件。 | 访问主页的美国人 **至少** 过去24小时里五次。 |
| 在24小时的时间范围内使用用户档案否定频率事件 | Any segment definition that refers to one or more profile attributes and a negated event that takes place a certain number of times within a time window of 24 hours. | 未访问主页的人员 **更多** 超过5次。 |
| 在24小时的时间配置文件内多次传入的点击 | Any segment definition that refers to multiple events that occur within a time window of 24 hours. | 访问主页的人员 **或** 在过去24小时内访问了结帐页面。 |
| Multiple events with a profile within a 24-hour time window | 任何区段定义，指在24小时内发生的一个或多个用户档案属性和多个事件。 | 访问主页的美国人 **和** 在过去24小时内访问了结帐页面。 |

Additionally, the segment **must** be tied to a merge policy that is active on edge. 有关合并策略的更多信息，请阅读 [合并策略指南](../../profile/api/merge-policies.md).

## Retrieve all segments enabled for edge segmentation

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
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
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

**响应**

成功的响应会返回新创建的用于边缘分段的区段定义的详细信息。

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

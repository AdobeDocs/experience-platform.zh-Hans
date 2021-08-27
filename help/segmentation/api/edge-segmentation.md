---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；边缘分段；边缘分段；流式边缘；
solution: Experience Platform
title: '使用API进行边缘分段 '
topic-legacy: developer guide
description: 本文档包含有关如何将边缘分段与Adobe Experience Platform Segmentation Service API结合使用的示例。
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: f92b12d343584f33870dd42288977e7b6e446b0f
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 3%

---

# 边缘分段（测试版）

>[!NOTE]
>
>以下文档说明了如何使用API执行边缘分段。 有关使用UI执行边缘分段的信息，请阅读[边缘分段UI指南](../ui/edge-segmentation.md)。 此外，边缘分段当前为测试版。 文档和功能可能会发生变化。

边缘分段功能可以即时在边缘上评估Adobe Experience Platform中的区段，从而实现同一页面和下一页面的个性化用例。

## 快速入门

本开发人员指南要求您对与边缘分割相关的各种[!DNL Adobe Experience Platform]服务有一定的了解。 在开始本教程之前，请查阅以下服务的文档：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据，实时提供统一的消费者用户档案。
- [[!DNL Segmentation]](../home.md):提供根据数据创建区段和受众的 [!DNL Real-time Customer Profile] 功能。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):用于组织客户体验数 [!DNL Platform] 据的标准化框架。

要成功调用[!DNL Data Prep] API端点，请阅读[Platform API](../../landing/api-guide.md)入门指南，了解所需的标头以及如何读取示例API调用。

## 边缘分段查询类型 {#query-types}

要使用边缘分段来评估区段，查询必须符合以下准则：

| 查询类型 | 详细信息 |
| ---------- | ------- |
| 传入点击 | 任何引用无时间限制的单个传入事件的区段定义。 |
| 引用用户档案的传入点击 | 任何引用单个传入事件（无时间限制）和一个或多个用户档案属性的区段定义。 |
| 时间窗口为24小时的传入点击 | 在24小时内引用单个传入事件的任何区段定义 |
| 引用时间窗口为24小时的用户档案的传入点击 | 在24小时内引用单个传入事件以及一个或多个用户档案属性的任何区段定义 |

{style=&quot;table-layout:auto&quot;}

以下查询类型是&#x200B;**not**，当前受边缘分段支持：

| 查询类型 | 详细信息 |
| ---------- | ------- |
| 多个事件 | 如果查询包含多个事件，则无法使用边缘分段来评估该查询。 |
| 频度查询 | 任何区段定义，指发生至少特定次数的事件。 |
| 引用用户档案的频率查询 | 任何区段定义，指发生至少特定次数且具有一个或多个用户档案属性的事件。 |

{style=&quot;table-layout:auto&quot;}

## 检索为边缘分段启用的所有区段

您可以通过向`/segment/definitions`端点发出GET请求，来检索IMS组织内为边缘分段启用的所有区段的列表。

**API格式**

要检索为边缘分段启用的区段，必须在请求路径中包含查询参数`evaluationInfo.synchronous.enabled=true`。

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

成功的响应会返回IMS组织中为边缘分段启用的区段数组。 有关返回的区段定义的详细信息，请参阅[区段定义端点指南](./segment-definitions.md)。

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

通过向`/segment/definitions`端点发出与上面列出的[边缘分段查询类型之一匹配的POST请求，可以创建为边缘分段启用的区段。](#query-types)

**API格式**

```http
POST /segment/definitions
```

**请求**

>[!NOTE]
>
>以下示例是创建区段的标准请求。 有关创建区段定义的更多信息，请阅读[创建区段](../tutorials/create-a-segment.md)的教程。

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

要了解如何使用Adobe Experience Platform用户界面执行类似操作和处理区段，请访问[区段生成器用户指南](../ui/segment-builder.md)。

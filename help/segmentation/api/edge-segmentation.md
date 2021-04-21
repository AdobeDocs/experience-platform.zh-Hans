---
keywords: Experience Platform；主题；流行主题；分割；分割；分割服务；边缘分割；边缘分割；流边缘；
solution: Experience Platform
title: '使用API进行边缘分割 '
topic-legacy: developer guide
description: 本文档包含有关如何使用Adobe Experience Platform Segmentation Service API的边缘分割的示例。
exl-id: effce253-3d9b-43ab-b330-943fb196180f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 3%

---

# 边缘分割（测试版）

>[!NOTE]
>
>以下文档说明如何使用API执行边缘分割。 有关使用UI执行边缘分割的信息，请阅读[边缘分割UI指南](../ui/edge-segmentation.md)。 此外，边缘分割当前处于测试阶段。 文档和功能可能会发生变化。

边缘细分是指在边缘即时评估Adobe Experience Platform中的细分，支持相同页面和下一页个性化使用案例。

## 入门指南

本开发人员指南要求对与边缘分割相关的各种[!DNL Adobe Experience Platform]服务有有效的了解。 在开始本教程之前，请查阅以下服务的文档：

- [[!DNL Real-time Customer Profile]](../../profile/home.md):根据来自多个来源的汇总数据实时提供统一的消费者用户档案。
- [[!DNL Segmentation]](../home.md):提供根据数据创建细分和受众的 [!DNL Real-time Customer Profile] 功能。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):组织客户体验数 [!DNL Platform] 据的标准化框架。

为了成功调用[!DNL Data Prep] API端点，请阅读[平台API](../../landing/api-guide.md)入门指南，了解所需标头以及如何读取示例API调用。

## 边缘分割查询类型{#query-types}

要使用边缘分割来评估区段，查询必须符合以下准则：

| 查询类型 | 详细信息 |
| ---------- | ------- |
| 传入点击 | 任何区段定义，指没有时间限制的单个传入事件。 |
| 指用户档案的传入点击 | 引用单个传入事件（无时间限制）和一个或多个用户档案属性的任何区段定义。 |
| 频率查询 | 指发生至少特定次数的事件的任何区段定义。 |
| 引用查询的频率用户档案 | 任何区段定义，指发生至少特定次数的事件，并具有一个或多个用户档案属性。 |

{style=&quot;table-layout:auto&quot;}

以下查询类型是&#x200B;**当前受边缘分段支持的**:

| 查询类型 | 详细信息 |
| ---------- | ------- |
| 相对时间窗口 | 如果查询引用时间窗口，则无法使用边缘分割来评估该窗口。 |
| 取反 | 如果查询包含取反或`not`事件，则无法使用边缘分段对其进行计算。 |
| 多个事件 | 如果查询包含多个事件，则无法使用边缘分割对其进行评估。 |

{style=&quot;table-layout:auto&quot;}

## 检索所有为边缘分割启用的段

您可以通过向`/segment/definitions`端点发出列表请求，检索IMS组织内为边缘分段启用的所有段的GET。

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

成功的响应会返回IMS组织中启用边缘分段的区段数组。 有关返回的区段定义的详细信息，请参阅[区段定义终结点指南](./segment-definitions.md)。

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

## 创建启用了边缘分割的区段

可以通过向`/segment/definitions`端点发出POST请求来创建已启用边缘分割的段。 除了匹配上面列出的[边缘分割查询类型之一之外，还必须将有效负荷中的`evaluationInfo.synchronous.enabled`标志设置为true。](#query-types)

**API格式**

```http
POST /segment/definitions
```

**请求**

>[!NOTE]
>
>以下示例是创建区段的标准请求。 有关创建区段定义的详细信息，请阅读教程[创建区段](../tutorials/create-a-segment.md)。

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
        "synchronous": {
            "enabled": true
        }
    }
}'
```

| 属性 | 描述 |
| -------- | ----------- |
| `evaluationInfo.synchronous.enabled` | `evaluationInfo`对象确定段定义将进行的评估类型。 要使用边缘分割，请将`evaluationInfo.synchronous.enabled`设置为值`true`。 |

**响应**

成功的响应会返回新创建的用于边缘分割的区段定义的详细信息。

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

现在，您已了解如何创建支持边缘细分的细分，因此，您可以使用这些细分来启用同页和下页个性化使用案例。

要了解如何使用Adobe Experience Platform用户界面执行类似操作和处理区段，请访问[区段生成器用户指南](../ui/segment-builder.md)。

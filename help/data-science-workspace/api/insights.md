---
keywords: Experience Platform；开发人员指南；端点；数据科学Workspace；热门主题；见解；sensei机器学习api
solution: Experience Platform
title: 分析API端点
description: 分析包含一些量度，用于使数据科学家能够通过显示相关评估量度来评估和选择最佳的ML模型。
role: Developer
exl-id: 603546d6-5686-4b59-99a7-90ecc0db8de3
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# 分析端点

分析包含一些量度，用于使数据科学家能够通过显示相关评估量度来评估和选择最佳的ML模型。

## 检索分析列表

您可以通过执行对分析端点的单个GET请求来检索分析列表。  要帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询的列表，请参阅[用于资源检索的查询参数](./appendix.md#query)的附录部分。

**API格式**

```http
GET /insights
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回一个有效负载，该有效负载包含分析列表，并且每个分析都有唯一标识符( `id` )。 此外，您将收到`context`，其中包含与随分析事件和量度数据一起跟踪的特定分析关联的唯一标识符。

```json
{
    "children": [
        {
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
        },
        {
            "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
            "context": {
                "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
                "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
                "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
            },
            "events": {
                "name": "fit",
                "eventValues": {
                    "algorithm": null,
                    "ratio": "0.8"
                }
            },
            "metrics": [
                {
                    "name": "MAPE",
                    "value": "0.0111111111111",
                    "valueType": "double"
                }
            ],
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-02T00:00:00.000Z"
            }
        ],
    "_page": {
        "count": 2
    }
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 与分析相对应的ID。 |
| `experimentId` | 有效的试验ID。 |
| `experimentRunId` | 有效的试验运行ID。 |
| `modelId` | 有效的模型ID。 |

## 检索特定分析

要查找特定分析，请发出GET请求并在请求路径中提供有效的`{INSIGHT_ID}`。 要帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询的列表，请参阅[用于资源检索的查询参数](./appendix.md#query)的附录部分。

**API格式**

```http
GET /insights/{INSIGHT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{INSIGHT_ID}` | Sensei Insight的唯一标识符。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights/08b8d174-6b0d-4d7e-acd8-1c4c908e14b2 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回包含分析唯一标识符(`id`)的有效负载。 此外，您将收到`context`，其中包含与分析事件和量度数据之后的特定分析关联的唯一标识符。

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
    },
    "events": {
        "name": "fit",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.8"
        }
    },
    "metrics": [
        {
            "name": "MAPE",
            "value": "0.0111111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 与分析相对应的ID。 |
| `experimentId` | 有效的试验ID。 |
| `experimentRunId` | 有效的试验运行ID。 |
| `modelId` | 有效的模型ID。 |

## 添加新的模型洞察

通过执行POST请求和有效负荷为新的模型分析提供上下文、事件和量度，可创建新的模型分析。 现有服务附加到用于创建新模型洞察的上下文字段时，不需要使用该字段，但您可以选择通过提供一个或多个对应的ID来使用现有服务创建新的模型洞察：

```json
"context": {
    "clientId": "f1ab3164-e688-433d-99ef-077b2be84731",
    "notebookId": "T4ab3164-e658-443d-97ef-022b2be84999",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "engineId": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
    "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71",
    "dataSetId": "5ee3cd7f2d34011913c56941"
  }
```

**API格式**

```http
POST /insights
```

**请求**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/insights \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H `Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json`
    -d {
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

**响应**

成功的响应将返回具有`{INSIGHT_ID}`的有效负载以及您在初始请求中提供的任何参数。

```json
{
    "id": "08b8d174-6b0d-4d7e-acd8-1c4c908e14b2",
    "context": {
        "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
        "experimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "modelId": "15c53796-bd6b-4e09-b51d-7296aa20af71"
    },
    "events": {
        "name": "fit2",
        "eventValues": {
            "algorithm": null,
            "ratio": "0.99"
        }
    },
    "metrics": [
        {
            "name": "MAPE2",
            "value": "0.11111111111",
            "valueType": "double"
        }
    ],
    "created": "2019-01-01T00:00:00.000Z",
    "updated": "2019-01-02T00:00:00.000Z"
}
```

| 属性 | 描述 |
| --- | --- |
| `insightId` | 发出成功的POST请求时为此特定见解创建的唯一ID。 |

## 检索算法的默认量度列表

您可以通过执行对指标端点的单个GET请求，检索所有算法和默认指标的列表。 要查询特定度量，请发出GET请求并在请求路径中提供有效的`{ALGORITHM}`。

**API格式**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| 参数 | 描述 |
| --- | --- |
| `{ALGORITHM}` | 算法类型的标识符。 |

**请求**

以下请求包含一个查询，并使用算法标识符`{ALGORITHM}`检索特定量度

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回一个有效负载，该有效负载包括`algorithm`唯一标识符和默认量度数组。

```json
{
    "children": [
        {
            "algorithm": "15c53796-bd6b-4e09-b51d-7296aa20af71",
            "defaultMetrics": [
                "f-score",
                "auroc",
                "roc",
                "precision",
                "recall",
                "accuracy",
                "confusion matrix"
            ]
        }
    ]
}
```

---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics;insights;sensei machine learning api
solution: Experience Platform
title: 洞察
topic: Developer guide
description: 洞察包含一些指标，这些指标可帮助数据科学家通过显示相关的评估指标来评估和选择最佳ML模型。
translation-type: tm+mt
source-git-commit: 194a29124949571638315efe00ff0b04bff19303
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 3%

---


# 洞察

洞察包含一些指标，这些指标可帮助数据科学家通过显示相关的评估指标来评估和选择最佳ML模型。

## 检索列表洞察

您可以通过向洞察端点执行单个列表请求来检索洞察GET。  要帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询的列表，请参阅附录部分中有关资产检 [索查询参数的部分](./appendix.md#query)。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回一个有效负荷，该负荷包含列表的洞察，并且每个分析都具有唯一标识符( `id` )。 此外，您还将收 `context` 到包含与该特定分析关联的唯一标识符(这些标识符与“洞察”事件和指标数据关联)。

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
| `id` | 与Insight对应的ID。 |
| `experimentId` | 有效的实验ID。 |
| `experimentRunId` | 有效的实验运行ID。 |
| `modelId` | 有效的模型ID。 |

## 检索特定Insight

要查找特定的分析，请发出GET请求，并在请求路 `{INSIGHT_ID}` 径中提供有效。 要帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询的列表，请参阅附录部分中有关资产检 [索查询参数的部分](./appendix.md#query)。

**API格式**

```http
GET /insights/{INSIGHT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{INSIGHT_ID}` | Sensei分析的唯一标识符。 |

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/insights/08b8d174-6b0d-4d7e-acd8-1c4c908e14b2 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回包含洞察唯一标识符(`id`)的有效负荷。 此外，您还将收 `context` 到包含与特定分析关联的唯一标识符(这些标识符与“洞察”事件和指标数据相关)。

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
| `id` | 与Insight对应的ID。 |
| `experimentId` | 有效的实验ID。 |
| `experimentRunId` | 有效的实验运行ID。 |
| `modelId` | 有效的模型ID。 |

## 添加新的模型分析

您可以通过执行POST请求和提供新模型分析的上下文、事件和度量的有效负荷来创建新模型分析。 用于创建新模型分析的上下文字段不需要将现有服务附加到该模型分析，但您可以通过提供一个或多个相应ID来选择使用现有服务创建新模型分析：

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的响应将返回一个有效负荷，该负 `{INSIGHT_ID}` 荷包含您在初始请求中提供的任何参数。

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
| `insightId` | 在成功发出POST请求时为此特定分析创建的唯一ID。 |

## 检索算法的默认列表

通过对度量端点执行单个列表请求，可以检索所有算法和默认度量的GET。 要查询特定度量，请发出GET请求，并在请求路 `{ALGORITHM}` 径中提供有效。

**API格式**

```http
GET /insights/metrics
GET /insights/metrics?algorithm={ALGORITHM}
```

| 参数 | 描述 |
| --- | --- |
| `{ALGORITHM}` | 算法类型的标识符。 |

**请求**

以下请求包含查询，并使用算法标识符检索特定度量 `{ALGORITHM}`

```shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/insights/metrics?algorithm={ALGORITHM}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回包含唯一标识符 `algorithm` 和一组默认度量的有效负荷。

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

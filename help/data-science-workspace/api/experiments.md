---
keywords: Experience Platform；开发人员指南；端点；Data Science Workspace；热门主题；实验；sensei机器学习api
solution: Experience Platform
title: 试验API端点
description: 模型开发和培训在试验级别进行，试验包括MLInstance、培训运行和评分运行。
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 4%

---

# 试验端点

模型开发和培训在试验级别进行，试验包括MLInstance、培训运行和评分运行。

## 创建试验 {#create-an-experiment}

您可以通过在请求有效负载中提供名称和有效的MLInstance ID时执行POST请求来创建试验。

>[!NOTE]
>
>与UI中的模型训练不同，通过显式API调用创建试验不会自动创建和执行训练运行。

**API格式**

```http
POST /experiments
```

**请求**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda"
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 试验所需的名称。 与此试验对应的训练运行将继承此值，以作为训练运行名称显示在UI中。 |
| `mlInstanceId` | 有效的MLInstance ID。 |

**响应**

成功响应将返回一个有效负载，其中包含新创建的试验的详细信息，包括其唯一标识符(`id`)。

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## 创建和执行训练或评分运行 {#experiment-training-scoring}

可通过执行POST请求并提供有效的试验ID并指定运行任务来创建训练或评分运行。 仅当试验已经存在且成功的训练运行时，才能创建评分运行。 成功创建训练运行将初始化模型训练过程，成功完成该过程将生成经过训练的模型。 生成经过训练的模型将替换任何以前已有的模型，以便试验在任何给定时间只能使用单个经过训练的模型。

**API格式**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| 参数 | 描述 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的试验ID。 |

**请求**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| 属性 | 描述 |
| --- | --- |
| `{TASK}` | 指定运行的任务。 将此值设置为 `train` 用于培训， `score` 用于评分，或 `featurePipeline` 用于功能管道。 |

**响应**

成功响应将返回一个有效负载，其中包含新创建的运行的详细信息（包括继承的默认训练或评分参数），以及运行的唯一ID (`{RUN_ID}`)。

```json
{
    "id": "33408593-2871-4198-a812-6d1b7d939cda",
    "mode": "{TASK}",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdBySchedule": false,
    "tasks": [
        {
            "name": "{TASK}",
            "parameters": [
                {
                    "key": "parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## 检索试验列表

通过执行单个GET请求并提供有效的MLInstance ID作为查询参数，可以检索属于特定MLInstance的试验列表。 有关可用查询的列表，请参阅 [用于资源检索的查询参数](./appendix.md#query).


**API格式**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MLINSTANCE_ID}` | 提供有效的MLInstance ID以检索属于该特定MLInstance的试验列表。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应将返回共享同一MLInstance ID (`{MLINSTANCE_ID}`)。

```json
{
    "children": [
        {
            "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "A name for this Experiment",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "6cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 1",
            "mlInstanceId": "46986c8f-7839-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "7cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 2",
            "mlInstanceId": "46986c8f-7939-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        }
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

## 检索特定试验 {#retrieve-specific}

您可以通过执行GET请求（请求路径中包含所需试验的ID）来检索特定试验的详细信息。

**API格式**

```http
GET /experiments/{EXPERIMENT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的试验ID。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回一个包含所请求试验详细信息的有效负载。

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## 检索试验运行的列表

通过执行单个GET请求并提供有效的试验ID，可检索属于特定试验的训练或评分运行的列表。 要帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询参数的完整列表，请参见 [用于资源检索的查询参数](./appendix.md#query).

>[!NOTE]
>
>组合多个查询参数时，必须使用&amp;符号分隔。

**API格式**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 参数 | 描述 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的试验ID。 |
| `{QUERY_PARAMETER}` | 其中一项 [可用的查询参数](./appendix.md#query) 用于筛选结果。 |
| `{VALUE}` | 上一个查询参数的值。 |

**请求**

以下请求包含一个查询，并检索属于某个试验的训练运行列表。

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回一个有效负载，其中包含运行的列表及其每个详细信息，包括其试验运行ID (`{RUN_ID}`)。

```json
{
    "children": [
        {
            "id": "33408593-2871-4198-a812-6d1b7d939cda",
            "mode": "train",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId==5cb25a2d-2cbd-4c99-a619-8ddae5250a7b,deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## 更新试验

您可以更新现有试验，方法是通过PUT请求（请求路径中包含目标试验的ID）覆盖其属性，并提供包含已更新属性的JSON有效负载。

>[!TIP]
>
>为了确保此PUT请求成功，建议您首先执行GET请求 [按ID检索试验](#retrieve-specific). 然后，修改并更新返回的JSON对象，并将修改后的JSON对象的整个内容应用为PUT请求的有效负载。

以下示例API调用最初具有这些属性时会更新实验的名称：

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "createdByService": false
}
```

**API格式**

```http
PUT /experiments/{EXPERIMENT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的试验ID。 |

**请求**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "createdByService": false
    }'
```

**响应**

成功的响应将返回包含试验更新详细信息的有效负载。

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "An updated name",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "createdByService": false
}
```

## 删除试验

您可以通过执行DELETE请求（请求路径中包含目标试验的ID）来删除单个试验。

**API格式**

```http
DELETE /experiments/{EXPERIMENT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的试验ID。 |

**请求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## 按MLInstance ID删除试验

通过执行包含MLInstance ID作为查询参数的DELETE请求，可以删除属于特定MLInstance的所有试验。

**API格式**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| 参数 | 描述 |
| --- | ---|
| `{MLINSTANCE_ID}` | 有效的MLInstance ID。 |

**请求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Experiments successfully deleted"
}
```

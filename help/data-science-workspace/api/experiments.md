---
keywords: Experience Platform；开发人员指南；端点；Data Science Workspace；热门主题；实验；Sensei机器学习API
solution: Experience Platform
title: Experiments API端点
topic-legacy: Developer guide
description: 模型开发和培训在实验级别进行，实验由MLI实例、培训运行和评分运行组成。
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 4%

---

# Experiments端点

模型开发和培训在实验级别进行，实验由MLI实例、培训运行和评分运行组成。

## 创建实验 {#create-an-experiment}

您可以通过执行POST请求来创建实验，同时在请求有效负载中提供名称和有效的MLInstance ID。

>[!NOTE]
>
>与UI中的模型培训不同，通过显式API调用创建实验不会自动创建和执行培训运行。

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
| `name` | 实验的所需名称。 与此实验对应的培训运行将继承此值，该值将作为培训运行名称显示在UI中。 |
| `mlInstanceId` | 有效的MLInstance ID。 |

**响应**

成功的响应会返回一个有效负载，其中包含新创建实验的详细信息，包括其唯一标识符(`id`)。

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

## 创建并执行培训或评分运行 {#experiment-training-scoring}

您可以通过执行POST请求并提供有效的实验ID并指定运行任务来创建培训或评分运行。 仅当实验具有现有且成功的培训运行时，才能创建评分运行。 成功创建培训运行将初始化模型培训过程，并且成功完成该过程将生成一个经过培训的模型。 生成经过培训的模型将取代之前存在的任何模型，以便实验在任何给定时间只能使用单个经过培训的模型。

**API格式**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| 参数 | 描述 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的实验ID。 |

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
| `{TASK}` | 指定运行的任务。 将此值设置为 `train` 培训， `score` 用于打分，或 `featurePipeline` ，用于特征管线。 |

**响应**

成功响应会返回一个有效负载，其中包含新创建运行的详细信息（包括继承的默认培训或评分参数）以及运行的唯一ID(`{RUN_ID}`)。

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

## 检索实验列表

您可以通过执行单个GET请求并提供有效的MLInstance ID作为查询参数，来检索属于特定MLInstance的实验列表。 有关可用查询的列表，请参阅 [资产检索查询参数](./appendix.md#query).


**API格式**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MLINSTANCE_ID}` | 提供有效的MLInstance ID以检索属于该特定MLInstance的实验列表。 |

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

成功的响应会返回共享相同MLInstance ID(`{MLINSTANCE_ID}`)。

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

## 检索特定实验 {#retrieve-specific}

您可以通过执行GET请求来检索特定实验的详细信息，该请求在请求路径中包含所需的实验ID。

**API格式**

```http
GET /experiments/{EXPERIMENT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的实验ID。 |

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

成功的响应会返回包含所请求实验详细信息的有效负载。

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

## 检索实验运行的列表

您可以通过执行单个GET请求并提供有效的实验ID，来检索属于特定实验的训练或评分运行列表。 要帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询参数的完整列表，请参阅附录中的 [资产检索查询参数](./appendix.md#query).

>[!NOTE]
>
>组合多个查询参数时，必须用与号(&amp;)分隔。

**API格式**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 参数 | 描述 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的实验ID。 |
| `{QUERY_PARAMETER}` | 其中一个 [可用查询参数](./appendix.md#query) 用于筛选结果。 |
| `{VALUE}` | 前一查询参数的值。 |

**请求**

以下请求包含一个查询，并检索属于某个实验的培训运行列表。

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功响应会返回一个有效负载，其中包含运行列表及其每个详细信息(包括其实验运行ID(`{RUN_ID}`)。

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

## 更新实验

您可以通过覆盖现有实验的属性来更新该实验，方法是：通过PUT请求覆盖其属性，该请求在请求路径中包含目标实验的ID，并提供包含已更新属性的JSON有效负载。

>[!TIP]
>
>为确保此PUT请求成功，建议您首先执行GET请求， [按ID检索实验](#retrieve-specific). 然后，修改并更新返回的JSON对象，并将修改的JSON对象的整个作为PUT请求的有效负载应用。

以下示例API调用会在最初具有这些属性时更新实验的名称：

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
| `{EXPERIMENT_ID}` | 有效的实验ID。 |

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

成功的响应会返回包含实验更新详细信息的有效负载。

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

## 删除实验

您可以通过执行DELETE请求来删除单个实验，该请求在请求路径中包含目标实验的ID。

**API格式**

```http
DELETE /experiments/{EXPERIMENT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的实验ID。 |

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

## 按MLInstance ID删除实验

您可以通过执行包含MLInstance ID作为查询参数的DELETE请求，删除属于特定MLInstance的所有实验。

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

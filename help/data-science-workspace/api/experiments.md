---
keywords: Experience Platform；开发人员指南；端点；数据科学Workspace；热门主题；实验；sensei机器学习api
solution: Experience Platform
title: 试验API端点
description: 模型开发和训练在试验级别进行，试验包括MLInstance、训练运行和评分运行。
role: Developer
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 4%

---

# 试验端点

>[!NOTE]
>
>Data Science Workspace不再可购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

模型开发和训练在试验级别进行，试验包括MLInstance、训练运行和评分运行。

## 创建试验 {#create-an-experiment}

您可以通过在请求有效载荷中提供一个名称和有效的MLInstance ID的同时执行POST请求来创建试验。

>[!NOTE]
>
>与UI中的模型训练不同，通过显式API调用创建试验不会自动创建和执行训练运行。

**API 格式**

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
| `name` | 实验的所需名称。 与此试验对应的训练运行将继承此值，以作为训练运行名称显示在 UI 中。 |
| `mlInstanceId` | 有效的MLInstance ID。 |

**响应**

成功响应将返回一个负载，其中包含新创建的实验的详细信息，包括其唯一标识符(`id`)。

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

## 创建和执行培训或评分运行 {#experiment-training-scoring}

您可以通过执行POST请求并提供有效的试验ID和指定运行任务来创建培训或评分运行。 只有当实验已经存在并成功运行培训时，才能创建评分运行。 成功创建培训运行将初始化模型培训过程，成功完成它将生成一个经过培训的模型。 生成经过训练的模型将替换任何以前存在的模型，以便试验在任何给定时间只能利用单个经过训练的模型。

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
| `{TASK}` | 指定运行的任务。 将此值设置为`train`以进行训练，`score`以进行评分，或`featurePipeline`以进行功能管道。 |

**响应**

成功的响应将返回一个有效负载，其中包含新创建的运行的详细信息（包括继承的默认训练或评分参数）以及运行的唯一ID (`{RUN_ID}`)。

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

您可以通过执行单个 GET 请求并提供有效的 MLInstance ID 作为查询参数来检索属于特定 MLInstance 的实验列表。 有关可用查询的列表，请参阅有关资产检索[&#128279;](./appendix.md#query)的查询参数的附录部分。


**API 格式**

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

成功的响应返回共享相同MLInstance ID (`{MLINSTANCE_ID}`)的试验列表。

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

成功的响应会返回一个有效负载，其中包含所请求实验的详细信息。

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

## 检索试验运行列表

可以通过执行单个 GET 请求并提供有效的实验 ID 来检索属于特定实验的训练或评分运行列表。 为了帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询参数的完整列表，请参阅有关资产检索[&#128279;](./appendix.md#query)的查询参数的附录部分。

>[!NOTE]
>
>在组合多个查询参数时，必须用&amp;符号分隔这些参数。

**API格式**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 参数 | 描述 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的试验ID。 |
| `{QUERY_PARAMETER}` | 用于筛选结果的[可用查询参数](./appendix.md#query)之一。 |
| `{VALUE}` | 上一个查询参数的值。 |

**请求**

以下请求包含一个查询并检索属于某个试验的训练运行列表。

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回一个负载，该负载包含运行列表及其每个详细信息，包括其实验运行ID (`{RUN_ID}`)。

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
>为确保此PUT请求成功，建议您首先执行GET请求，以[按ID](#retrieve-specific)检索试验。 然后，修改并更新返回的JSON对象，并将修改后的整个JSON对象应用作PUT请求的有效负载。

以下示例API调用在最初具有这些属性时会更新试验的名称：

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
| `{EXPERIMENT_ID}` | 有效的实验 ID。 |

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

## 删除试验

您可以通过执行请求路径中包含目标试验ID的DELETE请求来删除单个试验。

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

通过执行将MLInstance ID作为查询参数包含在内的DELETE请求，可以删除属于特定MLInstance的所有试验。

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

---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: 实验
topic: Developer guide
translation-type: tm+mt
source-git-commit: 01cfbc86516a05df36714b8c91666983f7a1b0e8

---


# 实验

模型开发和培训在实验级别进行，其中实验由MLI实例、培训运行和评分运行组成。

## 创建实验

您可以通过执行POST请求来创建实验，同时在请求有效负荷中提供名称和有效的MLI实例ID。

>[!NOTE] 与UI中的模型培训不同，通过显式API调用创建实验不会自动创建和执行培训运行。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "{MLINSTANCE_ID}"
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 实验的所需名称。 与此实验相对应的培训运行将继承此值，该值将作为培训运行名称显示在UI中。 |
| `mlInstanceId` | 有效的MLInstance ID。 |

**响应**

成功的响应返回一个包含新创建的实验详细信息(包括其唯一标识符(`id`))的有效负荷。

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## 创建并执行培训或评分运行

您可以通过执行POST请求并提供有效的实验ID并指定运行任务来创建培训或评分运行。 只有在实验具有现有且成功的培训运行时，才能创建评分运行。 成功创建培训运行将初始化模型培训过程，成功完成该过程将生成一个经过培训的模型。 生成经过培训的模型将取代任何先前已有的模型，这样实验在任何给定时间只能使用一个经过培训的模型。

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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| 属性 | 描述 |
| --- | --- |
| `{TASK}` | 指定运行的任务。 将此值设置为培训 `train` 、评分或功 `score` 能管道 `fp` 的值。 |

**响应**

成功的响应会返回一个有效负荷，其中包含新创建的运行的详细信息（包括继承的默认培训或评分参数）以及运行的唯一ID(`{RUN_ID}`)。

```json
{
    "id": "{RUN_ID}",
    "mode": "{TASK}",
    "experimentId": "{EXPERIMENT_ID}",
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

## 检索一列表实验

您可以通过执行单个GET请求并提供有效的MLInstance ID作为列表参数来检索属于特定MLInstance的实验查询。 有关可用查询的列表，请参阅有关资产检索的查询参 [数的附录部分](./appendix.md#query)。


**API格式**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MLINSTANCE_ID}` | 提供有效的MLInstance ID，以检索属于该特定MLInstance的实验列表。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId=={MLINSTANCE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回共享相同MLInstance ID(`{MLINSTANCE_ID}`)的一列表实验。

```json
{
    "children": [
        {
            "id": "{EXPERIMENT_ID}",
            "name": "A name for this Experiment",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "{EXPERIMENT_ID}",
            "name": "Training Run 1",
            "mlInstanceId": "{MLINSTANCE_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "{EXPERIMENT_ID}",
            "name": "Training Run 2",
            "mlInstanceId": "{MLINSTANCE_ID}",
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

您可以通过执行在请求路径中包含所需实验ID的GET请求来检索特定实验的详细信息。

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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```


**响应**

成功的响应会返回包含所请求实验详细信息的有效负荷。

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## 检索一列表实验运行

通过执行单个GET请求并提供有效的实验ID，可以检索属于特定实验的培训或得分运行列表。 要帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询参数的完整列表，请参阅有关资产检索的查询 [参数的附录部分](./appendix.md#query)。

>[!NOTE] 组合多个查询参数时，必须用&amp;符号(&amp;)分隔。

**API格式**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 参数 | 描述 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的实验ID。 |
| `{QUERY_PARAMETER}` | 用于筛选 [结果的可用查询](./appendix.md#query) 参数之一。 |
| `{VALUE}` | 前面查询参数的值。 |

**请求**

以下请求包含一个查询，并检索属于某个实验的列表培训运行。

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回一个有效负荷，它包含运行的列表及其每个详细信息(包括其实验运行ID(`{RUN_ID}`))。

```json
{
    "children": [
        {
            "id": "{RUN_ID}",
            "mode": "train",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId=={EXPERIMENT_ID},deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## 更新实验

您可以通过以下方式更新现有实验：通过PUT请求覆盖其属性，该请求在请求路径中包含目标实验的ID，并提供包含已更新属性的JSON有效负荷。

>[!TIP] 为了确保此PUT请求成功，建议首先执行GET请求以按ID [检索实验](#retrieve-specific)。 然后，修改并更新返回的JSON对象，并应用修改后的JSON对象的整个作为PUT请求的有效负荷。

以下示例API调用在最初具有这些属性时更新了实验的名称：

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "{MLINSTANCE_ID}",
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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "{MLINSTANCE_ID}",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "createdByService": false
    }'
```

**响应**

成功的响应会返回包含实验的更新详细信息的有效负荷。

```json
{
    "id": "{EXPERIMENT_ID}",
    "name": "An updated name",
    "mlInstanceId": "{MLINSTANCE_ID}",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "createdByService": false
}
```

## 删除实验

可以通过执行DELETE请求来删除单个实验，该请求在请求路径中包含目标实验的ID。

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
    https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

## 通过MLInstance ID删除实验

您可以通过执行DELETE请求来删除属于特定MLInstance的所有实验，该请求将MLInstance ID作为查询参数。

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
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId={MLINSTANCE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

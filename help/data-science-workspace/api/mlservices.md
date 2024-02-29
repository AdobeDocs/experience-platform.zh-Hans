---
keywords: Experience Platform；开发人员指南；端点；Data Science Workspace；热门主题；mlservices；sensei机器学习api
solution: Experience Platform
title: MLServices API端点
description: MLService是一个已发布的经过训练的模型，使您的组织能够访问和重复使用以前开发的模型。 MLServices的主要功能是能够按计划自动进行训练和评分。 计划的训练运行有助于保持模型的效率和准确性，而计划的得分运行可以确保始终如一地生成新见解。
role: Developer
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 2%

---

# MLServices端点

MLService是一个已发布的经过训练的模型，使您的组织能够访问和重复使用以前开发的模型。 MLServices的主要功能是能够按计划自动进行训练和评分。 计划的训练运行有助于保持模型的效率和准确性，而计划的得分运行可以确保始终如一地生成新见解。

自动训练和评分计划具有开始时间戳、结束时间戳和以表示的频率。 [cron表达式](https://en.wikipedia.org/wiki/Cron). 可以在以下情况下定义计划 [创建MLService](#create-an-mlservice) 或应用者 [更新现有MLService](#update-an-mlservice).

## 创建MLService {#create-an-mlservice}

您可以通过执行POST请求和提供服务的名称和有效MLInstance ID的有效负载来创建MLService。 用于创建MLService的MLInstance不需要具有现有的训练实验，但您可以通过提供相应的实验ID和训练运行ID，选择使用现有的训练模型创建MLService。

**API格式**

```http
POST /mlServices
```

**请求**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlServices \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingExperimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 所需的MLService名称。 与此MLService对应的服务将继承此值，以作为服务的名称显示在服务库UI中。 |
| `description` | MLService的可选描述。 与此MLService对应的服务将继承此值，以作为服务的描述显示在服务库UI中。 |
| `mlInstanceId` | 有效的MLInstance ID。 |
| `trainingDataSetId` | 培训数据集ID，如果提供，将覆盖MLInstance的默认数据集ID。 如果用于创建MLService的MLInstance未定义训练数据集，则必须提供相应的训练数据集ID。 |
| `trainingExperimentId` | 您可以选择提供的试验ID。 如果未提供此值，则创建MLService也将使用MLInstance的默认配置创建新的试验。 |
| `trainingExperimentRunId` | 您可以选择提供的训练运行ID。 如果未提供此值，则创建MLService也将使用MLInstance的默认训练参数创建和执行训练运行。 |
| `trainingSchedule` | 自动训练运行的时间表。 如果定义了此属性，则MLService将自动按计划执行训练运行。 |
| `trainingSchedule.startTime` | 计划训练运行将开始的时间戳。 |
| `trainingSchedule.endTime` | 计划培训运行将结束的时间戳。 |
| `trainingSchedule.cron` | 定义自动训练运行频率的cron表达式。 |
| `scoringSchedule` | 自动评分运行的时间表。 如果定义了此属性，则MLService将自动按计划执行评分运行。 |
| `scoringSchedule.startTime` | 开始计划评分运行的时间戳。 |
| `scoringSchedule.endTime` | 计划评分运行结束的时间戳。 |
| `scoringSchedule.cron` | 定义自动评分运行频率的cron表达式。 |

**响应**

成功的响应会返回包含新创建的MLService的详细信息的有效负载，包括其唯一标识符(`id`)，用于培训的试验ID (`trainingExperimentId`)，用于评分的试验ID (`scoringExperimentId`)，以及输入训练数据集ID (`trainingDataSetId`)。

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## 检索MLServices列表 {#retrieve-a-list-of-mlservices}

您可以通过执行单个GET请求来检索MLServices列表。 要帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询的列表，请参阅 [用于资源检索的查询参数](./appendix.md#query).

**API格式**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 参数 | 描述 |
| --- | --- |
| `{QUERY_PARAMETER}` | 其中一项 [可用的查询参数](./appendix.md#query) 用于筛选结果。 |
| `{VALUE}` | 上一个查询参数的值。 |

**请求**

以下请求包含一个查询，并检索共享同一MLInstance ID (`{MLINSTANCE_ID}`)。

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回MLServices列表及其详细信息，包括其MLService ID (`{MLSERVICE_ID}`)，用于培训的试验ID (`{TRAINING_ID}`)，用于评分的试验ID (`{SCORING_ID}`)，以及输入训练数据集ID (`{DATASET_ID}`)。

```json
{
    "children": [
        {
            "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
            "name": "A service created in UI",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
            "trainingDataSetId": "5ee3cd7f2d34011913c56941",
            "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda,deleted==false",
        "count": 1
    }
}
```

## 检索特定MLService {#retrieve-a-specific-mlservice}

您可以通过执行GET请求（请求路径中包含所需的MLService ID）来检索特定试验的详细信息。

**API格式**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`：有效的MLService ID。

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回包含所请求MLService的详细信息的有效负载。

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## 更新MLService {#update-an-mlservice}

您可以更新现有的MLService，方法是通过PUT请求（请求路径中包含目标MLService的ID）覆盖其属性，并提供包含已更新属性的JSON有效负载。

>[!TIP]
>
>为确保此PUT请求成功，建议您首先执行GET请求，以 [按ID检索MLService](#retrieve-a-specific-mlservice). 然后，修改并更新返回的JSON对象，并将修改后的整个JSON对象应用作PUT请求的有效负载。

**API格式**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`：有效的MLService ID。

**请求**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

**响应**

成功的响应将返回包含MLService更新详细信息的有效负载。

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-02T00:00:00.000Z"
}
```

## 删除MLService

通过执行DELETE路径中包含目标MLService ID的请求，可以删除单个MLService。

**API格式**

```http
DELETE /mlServices/{MLSERVICE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MLSERVICE_ID}` | 有效的MLService ID。 |

**请求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
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
    "detail": "MLService deletion was successful"
}
```

## 按MLInstance ID删除MLServices

通过执行将MLInstance ID指定为查询参数的DELETE请求，可以删除属于特定MLInstance的所有MLServices。

**API格式**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MLINSTANCE_ID}` | 有效的MLInstance ID。 |

**请求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "MLServices deletion was successful"
}
```

---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: 服务
topic: Developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 2%

---


# MLServices

MLService是已发布的经过培训的模型，它使您的组织能够访问和重用以前开发的模型。 MLServices的一个主要功能是能够按计划自动进行培训和评分。 计划的培训运行有助于保持模型的效率和准确性，而计划的评分运行可以确保一致地生成新的洞察。

自动化培训和评分计划由开始时间戳、结束时间戳和表示为崩溃表达式的频 [率定义](https://en.wikipedia.org/wiki/Cron)。 计划可在创建MLService [时定义](#create-an-mlservice) ，也可通 [过更新现有MLService](#update-an-mlservice)来应用。

## 创建MLService {#create-an-mlservice}

您可以通过执行POST请求和提供服务名称和有效MLInstance ID的有效负荷来创建MLService。 用于创建MLService的MLInstance不需要具有现有的培训实验，但您可以通过提供相应的实验ID和培训运行ID来选择使用现有的培训模型创建MLService。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | MLService的所需名称。 与此MLService对应的服务将继承此值，该值将作为服务的名称显示在服务库UI中。 |
| `description` | MLService的可选描述。 与此MLService对应的服务将继承此值，该值将作为服务的说明显示在服务库UI中。 |
| `mlInstanceId` | 有效的MLInstance ID。 |
| `trainingDataSetId` | 培训数据集ID，如果提供，将覆盖MLInstance的默认数据集ID。 如果用于创建MLService的MLInstance未定义培训数据集，则必须提供相应的培训数据集ID。 |
| `trainingExperimentId` | 您可以选择提供的实验ID。 如果未提供此值，则创建MLService还将使用MLInstance的默认配置创建新实验。 |
| `trainingExperimentRunId` | 培训运行ID，您可以选择提供它。 如果未提供此值，则创建MLService还将使用MLInstance的默认培训参数创建并执行培训运行。 |
| `trainingSchedule` | 自动化培训运行的计划。 如果定义了此属性，则MLService将自动按计划执行培训运行。 |
| `trainingSchedule.startTime` | 将开始进行预定培训的时间戳。 |
| `trainingSchedule.endTime` | 将结束预定培训运行的时间戳。 |
| `trainingSchedule.cron` | 定义自动培训运行频率的cron表达式。 |
| `scoringSchedule` | 自动评分的计划运行。 如果定义了此属性，则MLService将自动按计划执行评分运行。 |
| `scoringSchedule.startTime` | 将开始计划评分的时间戳。 |
| `scoringSchedule.endTime` | 将结束计划评分运行的时间戳。 |
| `scoringSchedule.cron` | 定义自动评分运行频率的cron表达式。 |

**响应**

成功的响应返回一个有效负荷，该有效负荷包含新创建的MLService的详细信息，包括其唯一标识符(`id`)、培训的实验ID(`trainingExperimentId`)、评分的实验ID(`scoringExperimentId`)和输入培训数据集ID(`trainingDataSetId`)。

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

## 检索MLServices的列表 {#retrieve-a-list-of-mlservices}

您可以通过执行单个GET请求来检索MLServices的列表。 要帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询的列表，请参阅附录部分中有关资产检 [索查询参数的部分](./appendix.md#query)。

**API格式**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 参数 | 描述 |
| --- | --- |
| `{QUERY_PARAMETER}` | 用于筛选 [结果的可用查询](./appendix.md#query) 参数之一。 |
| `{VALUE}` | 前一查询参数的值。 |

**请求**

以下请求包含一个查询，并检索共享同一MLInstance ID()的MLServices的列表`{MLINSTANCE_ID}`符。

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应返回MLServices的列表及其详细信息，`{MLSERVICE_ID}`包括其MLService ID()、培训的实验ID(`{TRAINING_ID}`)、评分的实验ID(`{SCORING_ID}`)和输入培训数据集ID(`{DATASET_ID}`)。

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

您可以通过执行GET请求来检索特定实验的详细信息，该请求在请求路径中包含所需的MLService ID。

**API格式**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: 有效的MLService ID。

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回包含所请求MLService的详细信息的有效负荷。

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

您可以通过PUT请求覆盖现有MLService的属性，该请求在请求路径中包含目标MLService的ID，并提供包含已更新属性的JSON有效负荷，从而更新现有MLService。

>[!TIP]
>
>为确保此PUT请求成功，建议先执行GET请求，以 [按ID检索MLService](#retrieve-a-specific-mlservice)。 然后，修改并更新返回的JSON对象，并应用已修改的JSON对象的整个作为PUT请求的有效负荷。

**API格式**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`: 有效的MLService ID。

**请求**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

成功的响应会返回包含MLService的更新详细信息的有效负荷。

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

您可以通过执行DELETE请求来删除单个MLService，该请求在请求路径中包含目标MLService的ID。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

您可以通过执行指定MLInstance ID作为DELETE参数的查询请求，删除属于特定MLInstance的所有MLService。

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

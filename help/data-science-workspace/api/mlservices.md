---
keywords: Experience Platform；开发人员指南；端点；Data Science Workspace；热门主题；mlservices;sensei机器学习API
solution: Experience Platform
title: MLServices API端点
topic-legacy: Developer guide
description: MLService是已发布的受过培训的模型，可让您的组织能够访问和重复使用以前开发的模型。 MLServices的一个关键功能是能够按计划自动执行培训和评分。 计划的培训运行有助于保持模型的效率和准确性，而计划的评分运行可确保始终如一地生成新的洞察。
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---

# MLServices端点

MLService是已发布的受过培训的模型，可让您的组织能够访问和重复使用以前开发的模型。 MLServices的一个关键功能是能够按计划自动执行培训和评分。 计划的培训运行有助于保持模型的效率和准确性，而计划的评分运行可确保始终如一地生成新的洞察。

自动培训和评分时间表由开始时间戳、结束时间戳和表示为 [cron表达式](https://en.wikipedia.org/wiki/Cron). 在 [创建MLService](#create-an-mlservice) 或 [更新现有MLService](#update-an-mlservice).

## 创建MLService {#create-an-mlservice}

您可以通过执行POST请求和有效负载来创建MLService，这些负载提供服务的名称和有效的MLInstance ID。 用于创建MLService的MLInstance不需要具有现有的培训实验，但您可以选择通过提供相应的实验ID和培训运行ID来使用现有的培训模型创建MLService。

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
| `name` | MLService所需的名称。 与此MLService对应的服务将继承此值，该值将作为服务的名称显示在服务库UI中。 |
| `description` | MLService的可选描述。 与此MLService对应的服务将继承此值，该值将在服务库UI中显示为服务的说明。 |
| `mlInstanceId` | 有效的MLInstance ID。 |
| `trainingDataSetId` | 培训数据集ID（如果提供）将覆盖MLInstance的默认数据集ID。 如果用于创建MLService的MLInstance未定义培训数据集，则必须提供相应的培训数据集ID。 |
| `trainingExperimentId` | 您可以选择提供的实验ID。 如果未提供此值，则创建MLService还将使用MLInstance的默认配置创建新的实验。 |
| `trainingExperimentRunId` | 您可以选择提供的培训运行ID。 如果未提供此值，则创建MLService也将使用MLInstance的默认培训参数创建和执行培训运行。 |
| `trainingSchedule` | 自动培训运行的时间表。 如果定义了此属性，则MLService将按计划自动执行培训运行。 |
| `trainingSchedule.startTime` | 将开始计划培训运行的时间戳。 |
| `trainingSchedule.endTime` | 计划培训运行的时间戳将结束。 |
| `trainingSchedule.cron` | 定义自动培训运行频率的CRON表达式。 |
| `scoringSchedule` | 运行自动评分的计划。 如果定义了此属性，则MLService将在计划的基础上自动执行评分运行。 |
| `scoringSchedule.startTime` | 将开始计划评分的时间戳。 |
| `scoringSchedule.endTime` | 计划评分运行的时间戳将结束。 |
| `scoringSchedule.cron` | 用于定义自动评分运行频率的CRON表达式。 |

**响应**

成功的响应会返回一个有效负载，其中包含新创建的MLService的详细信息，包括其唯一标识符(`id`)，用于培训的实验ID(`trainingExperimentId`)，用于评分的实验ID(`scoringExperimentId`)和输入培训数据集ID(`trainingDataSetId`)。

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

您可以通过执行单个GET请求来检索MLServices列表。 要帮助筛选结果，您可以在请求路径中指定查询参数。 有关可用查询的列表，请参阅 [资产检索查询参数](./appendix.md#query).

**API格式**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 参数 | 描述 |
| --- | --- |
| `{QUERY_PARAMETER}` | 其中一个 [可用查询参数](./appendix.md#query) 用于筛选结果。 |
| `{VALUE}` | 前一查询参数的值。 |

**请求**

以下请求包含一个查询，并检索共享相同MLInstance ID(`{MLINSTANCE_ID}`)。

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回MLServices的列表及其详细信息(包括其MLService ID(`{MLSERVICE_ID}`)，用于培训的实验ID(`{TRAINING_ID}`)，用于评分的实验ID(`{SCORING_ID}`)和输入培训数据集ID(`{DATASET_ID}`)。

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

## 检索特定的MLService {#retrieve-a-specific-mlservice}

您可以通过执行GET请求来检索特定实验的详细信息，该请求在请求路径中包含所需的MLService ID。

**API格式**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`:有效的MLService ID。

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

成功的响应会返回包含所请求MLService详细信息的有效负载。

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

您可以通过以下方法来更新现有MLService：通过PUT请求覆盖其属性，该请求在请求路径中包含目标MLService的ID，并提供包含已更新属性的JSON有效负载。

>[!TIP]
>
>为确保此PUT请求成功，建议您首先执行GET请求， [按ID检索MLService](#retrieve-a-specific-mlservice). 然后，修改并更新返回的JSON对象，并将修改的JSON对象的整个作为PUT请求的有效负载应用。

**API格式**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`:有效的MLService ID。

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

成功的响应会返回包含MLService更新详细信息的有效负载。

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

您可以通过执行DELETE请求来删除单个MLService，该请求将目标MLService的ID包含在请求路径中。

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

您可以通过执行DELETE请求来删除属于特定MLInstance的所有MLServices，该请求将MLInstance ID指定为查询参数。

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

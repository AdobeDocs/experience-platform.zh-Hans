---
keywords: Experience Platform；发布模型；Data Science Workspace；热门主题；敏感的机器学习api
solution: Experience Platform
title: 使用Sensei机器学习API发布模型作为服务
type: Tutorial
description: 本教程介绍使用Sensei机器学习API将模型作为服务发布的过程。
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 1%

---

# 使用 [!DNL Sensei Machine Learning API]

本教程介绍使用 [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## 快速入门

本教程需要对Adobe Experience Platform Data Science Workspace有一定的了解。 在开始本教程之前，请查看 [数据科学工作区概述](../home.md) 对该服务进行高级介绍。

要遵循本教程，您必须拥有现有的ML引擎、ML实例和实验。 有关如何在API中创建这些内容的步骤，请参阅 [导入打包的方法](./import-packaged-recipe-api.md).

最后，在开始本教程之前，请查看 [入门](../api/getting-started.md) 开发人员指南的部分，以了解成功调用 [!DNL Sensei Machine Learning] API，包括本教程中使用的所需标头：

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

所有POST、PUT和PATCH请求都需要一个额外的标头：

- Content-Type:application/json

### 关键术语

下表概述了本教程中使用的一些常用术语：

| 搜索词 | 定义 |
| --- | --- |
| **机器学习实例（ML实例）** | 实例 [!DNL Sensei] 特定租户的引擎，包含特定数据、参数和 [!DNL Sensei] 代码。 |
| **试验** | 用于保持培训实验运行、评分实验运行或两者的伞形实体。 |
| **计划实验** | 描述由用户定义的计划管理的培训或评分实验运行自动化的术语。 |
| **实验运行** | 培训或评分实验的特定实例。 来自特定实验的多个实验运行可能会因用于培训或评分的数据集值而异。 |
| **训练模型** | 在获得经过验证、评估和最终确定的模型之前，通过试验和特征工程过程创建的机器学习模型。 |
| **发布的模型** | 经过培训、验证和评估后，已完成并已版本化的模型即已到达。 |
| **机器学习服务（ML服务）** | 部署为服务的ML实例，用于支持使用API端点进行培训和评分的按需请求。 ML服务也可以使用现有的训练的实验运行创建。 |

## 使用现有的培训实验运行和计划评分创建ML服务

当您发布培训实验作为ML服务运行时，可以通过提供评分实验的详细信息来计划评分运行POST请求的有效负荷。 这会导致创建用于评分的计划实验实体。

**API格式**

```http
POST /mlServices
```

**请求**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'Content-Type: application/json'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "trainingExperimentId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingExperimentRunId": "5c5af39c73fcec153117eed1",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `mlInstanceId` | 现有的ML实例标识、用于创建ML服务的培训实验运行应与此特定ML实例对应。 |
| `trainingExperimentId` | 与ML实例识别对应的实验识别。 |
| `trainingExperimentRunId` | 用于发布ML服务的特定培训实验运行。 |
| `scoringDataSetId` | 指用于计划评分实验运行的特定数据集的标识。 |
| `scoringTimeframe` | 一个整数值，表示用于过滤数据以用于对实验运行进行评分的分钟数。 例如，值为 `10080` 是指过去10080分钟或168小时的数据将用于每个计划评分实验运行。 请注意， `0` 不会过滤数据，数据集中的所有数据都将用于评分。 |
| `scoringSchedule` | 包含有关计划评分实验运行的详细信息。 |
| `scoringSchedule.startTime` | 日期时间指示何时开始评分。 |
| `scoringSchedule.endTime` | 日期时间指示何时开始评分。 |
| `scoringSchedule.cron` | Cron值，指示对“实验运行”进行分数的间隔。 |

**响应**

成功的响应会返回新创建的ML服务的详细信息，包括其唯一 `id` 和 `scoringExperimentId` 对应的评分实验。


```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  },
  "created": "2019-04-08T14:45:25.981Z",
  "updated": "2019-04-08T14:45:25.981Z"
}
```

## 从现有ML实例创建ML服务

根据您的特定用例和要求，使用ML实例创建ML服务在计划培训和评分实验运行方面非常灵活。 本教程将介绍以下特定案例：

- [您不需要计划培训，但需要计划评分。](#ml-service-with-scheduled-experiment-for-scoring)
- [您需要计划实验运行才能进行培训和评分。](#ml-service-with-scheduled-experiments-for-training-and-scoring)

请注意，可以使用ML实例创建ML服务，而无需计划任何培训或评分实验。 此类ML服务将创建普通的实验实体和单个实验运行，以进行培训和评分。

### ML服务，具有计划实验，可进行评分 {#ml-service-with-scheduled-experiment-for-scoring}

您可以通过发布具有计划实验运行的ML实例以进行评分来创建ML服务，该实例将创建用于培训的普通实验实体。 将生成一个培训实验运行，并将用于所有计划的评分实验运行。 确保您具有 `mlInstanceId`, `trainingDataSetId`和 `scoringDataSetId` 创建ML服务时需要，并且它们存在且是有效值。

**API格式**

```http
POST /mlServices
```

**请求**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "mlInstanceId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingDataSetId": "5c5af39c73fcec153117eed1",
        "trainingTimeframe": "10000",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| JSON键 | 描述 |
| --- | --- |
| `mlInstanceId` | 现有ML实例标识，表示用于创建ML服务的ML实例。 |
| `trainingDataSetId` | 用于训练实验的特定数据集的标识。 |
| `trainingTimeframe` | 一个整数值，表示用于筛选用于培训实验的数据的分钟数。 例如，值为 `"10080"` 是指过去10080分钟或168小时的数据将用于培训实验运行。 请注意， `"0"` 将不会过滤数据，数据集中的所有数据都将用于培训。 |
| `scoringDataSetId` | 指用于计划评分实验运行的特定数据集的标识。 |
| `scoringTimeframe` | 一个整数值，表示用于过滤数据以用于对实验运行进行评分的分钟数。 例如，值为 `"10080"` 是指过去10080分钟或168小时的数据将用于每个计划评分实验运行。 请注意， `"0"` 不会过滤数据，数据集中的所有数据都将用于评分。 |
| `scoringSchedule` | 包含有关计划评分实验运行的详细信息。 |
| `scoringSchedule.startTime` | 日期时间指示何时开始评分。 |
| `scoringSchedule.endTime` | 日期时间指示何时开始评分。 |
| `scoringSchedule.cron` | Cron值，指示对“实验运行”进行分数的间隔。 |

**响应**

成功的响应会返回新创建的ML服务的详细信息。 这包括服务的独特 `id`，以及 `trainingExperimentId` 和 `scoringExperimentId` 对其相应的训练和评分实验分别进行。

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

### ML服务，具有用于培训和评分的计划实验 {#ml-service-with-scheduled-experiments-for-training-and-scoring}

要将现有ML实例作为ML服务发布并计划进行培训和评分实验运行，您需要提供培训和评分计划。 创建此配置的ML服务时，还会创建用于培训和评分的计划实验实体。 请注意，培训和评分计划不必相同。 在评分作业执行期间，将获取由计划培训实验运行生成的最新培训模型，并将其用于计划的评分运行。

**API格式**

```http
POST /mlServices
```

**请求**

```SHELL
curl -X POST 'https://platform.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "string",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| JSON键 | 描述 |
| --- | --- |
| `mlInstanceId` | 现有ML实例标识，表示用于创建ML服务的ML实例。 |
| `trainingDataSetId` | 用于训练实验的特定数据集的标识。 |
| `trainingTimeframe` | 一个整数值，表示用于筛选用于培训实验的数据的分钟数。 例如，值为 `"10080"` 是指过去10080分钟或168小时的数据将用于培训实验运行。 请注意， `"0"` 将不会过滤数据，数据集中的所有数据都将用于培训。 |
| `scoringDataSetId` | 指用于计划评分实验运行的特定数据集的标识。 |
| `scoringTimeframe` | 一个整数值，表示用于过滤数据以用于对实验运行进行评分的分钟数。 例如，值为 `"10080"` 是指过去10080分钟或168小时的数据将用于每个计划评分实验运行。 请注意， `"0"` 不会过滤数据，数据集中的所有数据都将用于评分。 |
| `trainingSchedule` | 包含有关计划培训实验运行的详细信息。 |
| `scoringSchedule` | 包含有关计划评分实验运行的详细信息。 |
| `scoringSchedule.startTime` | 日期时间指示何时开始评分。 |
| `scoringSchedule.endTime` | 日期时间指示何时开始评分。 |
| `scoringSchedule.cron` | Cron值，指示对“实验运行”进行分数的间隔。 |

**响应**

成功的响应会返回新创建的ML服务的详细信息。 这包括服务的独特 `id`，以及 `trainingExperimentId` 和 `scoringExperimentId` 分别进行相应的训练和评分实验。 在以下示例响应中，存在 `trainingSchedule` 和 `scoringSchedule` 建议用于培训和评分的实验实体是计划的实验。

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",,
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

## 查找ML服务 {#retrieving-ml-services}

您可以通过创建 `GET` 请求 `/mlServices` 提供 `id` ML服务的URL。

**API格式**

```http
GET /mlServices/{SERVICE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SERVICE_ID}` | 独特 `id` 你正在查的ML服务。 |

**请求**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应会返回ML服务的详细信息。

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-05-13T23:46:03.478Z",
  "updated": "2019-05-13T23:46:03.478Z"
}
```

>[!NOTE]
>
>检索不同的ML服务时，可能会返回包含更多或更少键值对的响应。 上述响应是 [ML服务，同时包含计划培训和评分实验运行](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## 安排培训或评分

如果要计划对已发布的ML服务的评分和培训，可以通过使用 `PUT` 请求 `/mlServices`.

**API格式**

```http
PUT /mlServices/{SERVICE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SERVICE_ID}` | 独特 `id` 的ML服务。 |

**请求**

以下请求通过添加 `trainingSchedule` 和 `scoringSchedule` 键 `startTime`, `endTime`和 `cron` 键。

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingExperimentId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "integer",
        "scoringExperimentId": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "integer",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        }
      }'
```

>[!WARNING]
>
>请勿尝试修改 `startTime` 现有计划培训和评分作业。 如果 `startTime` 必须修改，请考虑发布相同的模型并重新计划培训和评分作业。

**响应**

成功的响应会返回更新的ML服务的详细信息。

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T09:43:55.563Z"
}
```

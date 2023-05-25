---
keywords: Experience Platform；发布模型；Data Science Workspace；热门主题；sensei机器学习api
solution: Experience Platform
title: 使用Sensei机器学习API发布模型即服务
type: Tutorial
description: 本教程介绍了使用Sensei机器学习API发布模型作为服务的过程。
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 1%

---

# 使用将模型发布为服务 [!DNL Sensei Machine Learning API]

本教程介绍了使用将模型发布为服务的过程。 [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## 快速入门

本教程要求您对Adobe Experience Platform数据科学工作区有一定的了解。 在开始本教程之前，请查看 [数据科学工作区概述](../home.md) 了解该服务的高级介绍。

要遵循本教程，您必须具有现有的ML引擎、ML实例和试验。 有关如何在API中创建这些内容的步骤，请参阅关于的教程 [导入包装的配方](./import-packaged-recipe-api.md).

最后，在开始本教程之前，请查看 [快速入门](../api/getting-started.md) 部分，了解成功调用 [!DNL Sensei Machine Learning] API，包括本教程中使用的所需标头：

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

所有POST、PUT和PATCH请求都需要额外的标头：

- Content-Type： application/json

### 关键术语

下表概述了本教程中使用的一些常用术语：

| 搜索词 | 定义 |
| --- | --- |
| **机器学习实例（ML实例）** | 的实例 [!DNL Sensei] 特定租户的引擎，包含特定数据、参数和 [!DNL Sensei] 代码。 |
| **试验** | 用于举办培训实验运行、评分实验运行或两者的伞形实体。 |
| **计划的试验** | 一个术语，用于描述训练或评分实验运行的自动化，由用户定义的计划管理。 |
| **试验运行** | 训练或评分实验的特定实例。 特定实验中的多个实验运行在用于训练或评分的数据集值上可能有所不同。 |
| **训练好的模型** | 在到达验证、评估和最终确定模型之前，通过试验和特征工程过程创建的机器学习模型。 |
| **已发布模型** | 经过培训、验证和评估后，最终确定并确定了版本化模型。 |
| **机器学习服务（ML服务）** | 作为服务部署的ML实例，用于支持使用API端点进行训练和评分的按需请求。 也可以使用现有的经过训练的试验运行来创建ML服务。 |

## 使用现有的训练实验运行和计划评分创建ML服务

将训练实验运行作为ML服务发布时，您可以通过提供评分实验运行的详细信息来计划评分，并运行POST请求的有效负载。 这将导致创建一个计划试验实体以进行评分。

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
| `mlInstanceId` | 现有的ML实例标识，用于创建ML服务的训练实验运行应与此特定的ML实例对应。 |
| `trainingExperimentId` | 与ML实例标识对应的试验标识。 |
| `trainingExperimentRunId` | 用于发布ML服务的特定训练实验运行。 |
| `scoringDataSetId` | 指将用于计划评分实验运行的特定数据集的标识。 |
| `scoringTimeframe` | 一个整数值，表示用于筛选要用于评分试验运行的数据的分钟数。 例如，值 `10080` 表示过去10080分钟或168小时内的数据将用于每次计划的评分实验运行。 请注意，值 `0` 将不筛选数据，数据集中的所有数据将用于评分。 |
| `scoringSchedule` | 包含有关计划的评分试验运行的详细信息。 |
| `scoringSchedule.startTime` | 指示何时开始评分的日期时间。 |
| `scoringSchedule.endTime` | 指示何时开始评分的日期时间。 |
| `scoringSchedule.cron` | Cron值，指示对试验运行进行评分的间隔。 |

**响应**

成功响应将返回新创建的ML服务的详细信息，包括其唯一的 `id` 和 `scoringExperimentId` 进行相应的评分试验。


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

根据您的特定用例和要求，使用ML实例创建ML服务在计划训练和评分实验运行方面非常灵活。 本教程将介绍以下特定案例：

- [您不需要进行计划培训，但需要计划评分。](#ml-service-with-scheduled-experiment-for-scoring)
- [训练和评分都需要计划的实验运行。](#ml-service-with-scheduled-experiments-for-training-and-scoring)

请注意，可以使用ML实例创建ML服务，而无需安排任何训练或评分实验。 此类ML服务将创建普通实验实体和单个实验运行，用于训练和评分。

### 带有评分计划试验的ML服务 {#ml-service-with-scheduled-experiment-for-scoring}

您可以通过发布ML实例来创建ML服务，该实例具有为评分而计划的试验运行，这将创建一个用于训练的普通试验实体。 生成一个训练实验运行，该运行将用于所有计划的评分实验运行。 确保您拥有 `mlInstanceId`， `trainingDataSetId`、和 `scoringDataSetId` 创建ML服务所必需的，并且它们存在且是有效值。

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
| `trainingDataSetId` | 指用于训练试验的特定数据集的标识。 |
| `trainingTimeframe` | 一个整数值，表示用于筛选要用于训练试验的数据的分钟数。 例如，值 `"10080"` 表示将使用过去10080分钟或168小时的数据进行训练实验运行。 请注意，值 `"0"` 将不过滤数据，数据集中的所有数据都用于训练。 |
| `scoringDataSetId` | 指将用于计划评分实验运行的特定数据集的标识。 |
| `scoringTimeframe` | 一个整数值，表示用于筛选要用于评分试验运行的数据的分钟数。 例如，值 `"10080"` 表示过去10080分钟或168小时内的数据将用于每次计划的评分实验运行。 请注意，值 `"0"` 将不筛选数据，数据集中的所有数据将用于评分。 |
| `scoringSchedule` | 包含有关计划的评分试验运行的详细信息。 |
| `scoringSchedule.startTime` | 指示何时开始评分的日期时间。 |
| `scoringSchedule.endTime` | 指示何时开始评分的日期时间。 |
| `scoringSchedule.cron` | Cron值，指示对试验运行进行评分的间隔。 |

**响应**

成功的响应将返回新创建的ML服务的详细信息。 这包括服务的独特 `id`以及 `trainingExperimentId` 和 `scoringExperimentId` 分别进行了相应的训练和评分实验。

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

### 包含用于训练和评分的计划实验的ML服务 {#ml-service-with-scheduled-experiments-for-training-and-scoring}

要将现有ML实例发布为ML服务，并安排训练和评分实验运行，您需要提供训练和评分计划。 在创建此配置的ML服务时，还会创建用于训练和评分的计划试验实体。 请注意，训练和评分时间表不必相同。 在评分作业执行期间，将获取计划培训实验运行生成的最新已训练模型，并将其用于计划评分运行。

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
| `trainingDataSetId` | 指用于训练试验的特定数据集的标识。 |
| `trainingTimeframe` | 一个整数值，表示用于筛选要用于训练试验的数据的分钟数。 例如，值 `"10080"` 表示将使用过去10080分钟或168小时的数据进行训练实验运行。 请注意，值 `"0"` 将不过滤数据，数据集中的所有数据都用于训练。 |
| `scoringDataSetId` | 指将用于计划评分实验运行的特定数据集的标识。 |
| `scoringTimeframe` | 一个整数值，表示用于筛选要用于评分试验运行的数据的分钟数。 例如，值 `"10080"` 表示过去10080分钟或168小时内的数据将用于每次计划的评分实验运行。 请注意，值 `"0"` 将不筛选数据，数据集中的所有数据将用于评分。 |
| `trainingSchedule` | 包含有关计划的培训试验运行的详细信息。 |
| `scoringSchedule` | 包含有关计划的评分试验运行的详细信息。 |
| `scoringSchedule.startTime` | 指示何时开始评分的日期时间。 |
| `scoringSchedule.endTime` | 指示何时开始评分的日期时间。 |
| `scoringSchedule.cron` | Cron值，指示对试验运行进行评分的间隔。 |

**响应**

成功的响应将返回新创建的ML服务的详细信息。 这包括服务的独特 `id`以及 `trainingExperimentId` 和 `scoringExperimentId` 分别进行了相应的训练和评分实验。 在下面的示例响应中， `trainingSchedule` 和 `scoringSchedule` 建议用于训练和评分的实验实体是计划的实验。

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

您可以通过以下方式查找现有ML服务 `GET` 请求 `/mlServices` 并提供独一无二的 `id` 路径中ML服务的路径路径。

**API格式**

```http
GET /mlServices/{SERVICE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SERVICE_ID}` | 唯一 `id` 中指定的ML服务。 |

**请求**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的响应将返回ML服务的详细信息。

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
>检索不同的ML服务可能会返回包含更多或更少键值对的响应。 上述响应是 [包含计划训练和评分实验运行的ML服务](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## 计划培训或评分

如果要为已发布的ML服务计划评分和培训，可以通过更新现有的ML服务来完成此操作。 `PUT` 请求日期 `/mlServices`.

**API格式**

```http
PUT /mlServices/{SERVICE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SERVICE_ID}` | 唯一 `id` 要更新的ML服务的属性。 |

**请求**

以下请求通过添加 `trainingSchedule` 和 `scoringSchedule` 键及其各自对应的 `startTime`， `endTime`、和 `cron` 键。

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
>不要尝试修改 `startTime` 现有计划的培训和评分作业。 如果 `startTime` 必须修改，请考虑发布相同的模型并重新计划训练和评分作业。

**响应**

成功的响应将返回更新的ML服务的详细信息。

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

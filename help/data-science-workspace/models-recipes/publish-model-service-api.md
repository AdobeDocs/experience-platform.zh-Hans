---
keywords: Experience Platform；发布模型；数据科学Workspace；热门主题；sensei机器学习api
solution: Experience Platform
title: 使用Sensei机器学习API的Publish a Model as a Service
type: Tutorial
description: 本教程介绍了使用Sensei机器学习API将模型发布为服务的过程。
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 1%

---

# 使用[!DNL Sensei Machine Learning API]Publish模型即服务

本教程介绍使用[[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)将模型发布为服务的过程。

## 快速入门

本教程需要您对Adobe Experience Platform数据科学Workspace有一定的了解。 在开始本教程之前，请查看[Data Science Workspace概述](../home.md)，了解有关该服务的高级介绍。

要遵循本教程，您必须具有现有的ML引擎、ML实例和试验。 有关如何在API中创建这些方法的步骤，请参阅有关[导入打包的方法](./import-packaged-recipe-api.md)的教程。

最后，在开始本教程之前，请查看开发人员指南的[快速入门](../api/getting-started.md)部分，以了解成功调用[!DNL Sensei Machine Learning] API所需了解的重要信息，包括本教程中使用的所需标头：

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

所有POST、PUT和PATCH请求都需要额外的标头：

- Content-Type： application/json

### 关键术语

下表概述了本教程中使用的一些常用术语：

| 搜索词 | 定义 |
| --- | --- |
| **机器学习实例（ML实例）** | 特定租户的[!DNL Sensei]引擎实例，包含特定数据、参数和[!DNL Sensei]代码。 |
| **试验** | 用于举办培训实验运行、评分实验运行或两者的伞形实体。 |
| **计划的试验** | 一个术语，用于描述训练或评分实验运行的自动化，受用户定义的计划约束。 |
| **试验运行** | 训练或评分实验的特定实例。 特定实验中的多个实验运行在用于训练或评分的数据集值上可能有所不同。 |
| **训练好的模型** | 在到达验证、评估和最终确定的模型之前，通过试验和特征工程过程创建的机器学习模型。 |
| **已发布的模型** | 经过培训、验证和评估后，最终确定和版本化的模型最终形成。 |
| **机器学习服务（ML服务）** | 作为服务部署的ML实例，用于支持使用API端点进行培训和评分的按需请求。 ML服务也可以使用现有的经过训练的试验运行来创建。 |

## 使用现有的训练实验运行和计划评分创建ML服务

在将训练实验运行作为ML服务发布时，您可以通过提供评分实验运行请求的有效负荷的详细信息，来安排POST。 这将导致创建计划的试验实体以进行评分。

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
| `mlInstanceId` | 现有的ML实例标识，用于创建ML服务的训练实验运行应该与此特定的ML实例对应。 |
| `trainingExperimentId` | 与ML实例标识对应的试验标识。 |
| `trainingExperimentRunId` | 用于发布ML服务的特定训练实验运行。 |
| `scoringDataSetId` | 指将用于计划评分实验运行的特定数据集的标识。 |
| `scoringTimeframe` | 一个整数值，表示用于筛选要用于评分试验运行的数据的分钟数。 例如，值`10080`表示将使用过去10080分钟或168小时的数据进行每次计划的评分试验运行。 请注意，值`0`不会过滤数据，数据集中的所有数据均用于评分。 |
| `scoringSchedule` | 包含有关计划的评分试验运行的详细信息。 |
| `scoringSchedule.startTime` | 指示何时开始评分的日期时间。 |
| `scoringSchedule.endTime` | 指示何时开始评分的日期时间。 |
| `scoringSchedule.cron` | Cron值，指示对试验运行进行评分的间隔。 |

**响应**

成功的响应返回新创建的ML服务的详细信息，包括其唯一的`id`及其相应评分试验的`scoringExperimentId`。


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

根据您的特定用例和要求，使用ML实例创建ML服务在计划训练和评分实验运行方面比较灵活。 本教程将介绍以下特定案例：

- [您不需要进行计划训练，但需要计划得分。](#ml-service-with-scheduled-experiment-for-scoring)
- [训练和评分都需要按计划进行试验运行。](#ml-service-with-scheduled-experiments-for-training-and-scoring)

请注意，可以使用ML实例创建ML服务，而无需计划任何训练或评分实验。 此类ML服务将创建普通实验实体和单个实验运行，以进行训练和评分。

### 带有计划的评分试验的ML服务 {#ml-service-with-scheduled-experiment-for-scoring}

您可以通过发布具有计划的试验运行以进行评分的ML实例来创建ML服务，这将创建一个用于培训的普通试验实体。 生成训练实验运行，并将用于所有计划的评分实验运行。 确保您具有创建ML服务所需的`mlInstanceId`、`trainingDataSetId`和`scoringDataSetId`，并且它们存在且是有效值。

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
| `trainingTimeframe` | 一个整数值，表示用于筛选要用于训练试验的数据的分钟数。 例如，值`"10080"`表示将使用过去10080分钟或168小时的数据进行训练试验运行。 请注意，值`"0"`不会过滤数据，数据集中的所有数据都用于训练。 |
| `scoringDataSetId` | 指将用于计划评分实验运行的特定数据集的标识。 |
| `scoringTimeframe` | 一个整数值，表示用于筛选要用于评分试验运行的数据的分钟数。 例如，值`"10080"`表示将使用过去10080分钟或168小时的数据进行每次计划的评分试验运行。 请注意，值`"0"`不会过滤数据，数据集中的所有数据均用于评分。 |
| `scoringSchedule` | 包含有关计划的评分试验运行的详细信息。 |
| `scoringSchedule.startTime` | 指示何时开始评分的日期时间。 |
| `scoringSchedule.endTime` | 指示何时开始评分的日期时间。 |
| `scoringSchedule.cron` | Cron值，指示对试验运行进行评分的间隔。 |

**响应**

成功的响应将返回新创建的ML服务的详细信息。 这包括服务的唯一`id`，以及分别用于其相应训练和评分实验的`trainingExperimentId`和`scoringExperimentId`。

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

要将现有ML实例发布为ML服务，并安排训练和评分实验运行，您需要提供训练和评分计划。 当创建此配置的ML服务时，还会创建用于训练和评分的计划试验实体。 请注意，训练和评分时间表不必相同。 在评分作业执行期间，将获取计划培训实验运行生成的最新已训练模型，并将其用于计划评分运行。

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
| `trainingTimeframe` | 一个整数值，表示用于筛选要用于训练试验的数据的分钟数。 例如，值`"10080"`表示将使用过去10080分钟或168小时的数据进行训练试验运行。 请注意，值`"0"`不会过滤数据，数据集中的所有数据都用于训练。 |
| `scoringDataSetId` | 指将用于计划评分实验运行的特定数据集的标识。 |
| `scoringTimeframe` | 一个整数值，表示用于筛选要用于评分试验运行的数据的分钟数。 例如，值`"10080"`表示将使用过去10080分钟或168小时的数据进行每次计划的评分试验运行。 请注意，值`"0"`不会过滤数据，数据集中的所有数据均用于评分。 |
| `trainingSchedule` | 包含有关计划的培训试验运行的详细信息。 |
| `scoringSchedule` | 包含有关计划的评分试验运行的详细信息。 |
| `scoringSchedule.startTime` | 指示何时开始评分的日期时间。 |
| `scoringSchedule.endTime` | 指示何时开始评分的日期时间。 |
| `scoringSchedule.cron` | Cron值，指示对试验运行进行评分的间隔。 |

**响应**

成功的响应将返回新创建的ML服务的详细信息。 这包括服务的唯一`id`，以及其相应的训练和评分实验的`trainingExperimentId`和`scoringExperimentId`。 在下面的示例响应中，`trainingSchedule`和`scoringSchedule`的存在表明用于训练和评分的试验实体是计划的试验。

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

您可以通过向`/mlServices`发出`GET`请求并在路径中提供唯一的`id`ML服务来查找现有ML服务。

**API格式**

```http
GET /mlServices/{SERVICE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SERVICE_ID}` | 您正在查找的ML服务的唯一`id`。 |

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
>检索不同的ML服务可能会返回包含更多或更少键值对的响应。 上述响应是[ML服务的表示形式，包含计划的训练和评分实验运行](#ml-service-with-scheduled-experiments-for-training-and-scoring)。


## 计划培训或评分

如果要对已发布的ML服务计划评分和培训，可以通过在`/mlServices`上使用`PUT`请求更新现有ML服务来实现。

**API格式**

```http
PUT /mlServices/{SERVICE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SERVICE_ID}` | 您正在更新的ML服务的唯一`id`。 |

**请求**

以下请求通过添加`trainingSchedule`和`scoringSchedule`键以及它们各自的`startTime`、`endTime`和`cron`键来为现有ML服务计划训练和评分。

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
>不要尝试修改现有计划培训和评分作业上的`startTime`。 如果必须修改`startTime`，请考虑发布相同的模型并重新计划训练和评分作业。

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

---
keywords: Experience Platform；发布模型；数据科学工作区；热门主题；sensei机器学习api
solution: Experience Platform
title: 使用Sensei机器学习API将模型发布为服务
topic-legacy: tutorial
type: Tutorial
description: 本教程介绍使用Sensei Machine Learning API将模型作为服务发布的过程。
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
translation-type: tm+mt
source-git-commit: a6d047d52dad085ba662bd684c896bdffe3eef2e
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 1%

---

# 使用[!DNL Sensei Machine Learning API]将模型发布为服务

本教程介绍使用[[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)将模型作为服务发布的过程。

## 入门指南

本教程需要对Adobe Experience Platform Data Science Workspace有充分的了解。 在开始本教程之前，请查看[数据科学工作区概述](../home.md)，以了解有关该服务的高级介绍。

要完成本教程，您必须拥有一个现有的ML引擎、ML实例和实验。 有关如何在API中创建这些菜谱的步骤，请参阅有关[导入打包菜谱](./import-packaged-recipe-api.md)的教程。

最后，在开始本教程之前，请查看开发人员指南的[入门](../api/getting-started.md)部分，了解成功调用[!DNL Sensei Machine Learning] API所需的重要信息，包括本教程中使用的所需标头：

- `{ACCESS_TOKEN}`
- `{IMS_ORG}`
- `{API_KEY}`

所有POST、PUT和PATCH请求都需要额外的标题：

- 内容类型：application/json

### 主要条款

下表概述了本教程中使用的一些常见术语：

| 搜索词 | 定义 |
| --- | --- |
| **机器学习实例（ML实例）** | 特定租户的[!DNL Sensei]引擎实例，包含特定数据、参数和[!DNL Sensei]代码。 |
| **实验** | 用于保持培训“实验运行”、“得分”“实验运行”或两者的伞形实体。 |
| **计划实验** | 一个术语，用于描述由用户定义的计划管理的培训或评分实验运行的自动化。 |
| **实验运行** | 培训或评分实验的特定实例。 来自特定实验的多个实验运行在用于培训或评分的数据集值中可能有所不同。 |
| **训练模型** | 通过实验和特征工程过程创建的机器学习模型，然后得到一个经过验证、评估和最终的模型。 |
| **发布模型** | 经过培训、验证和评估后即可获得最终的版本化模型。 |
| **机器学习服务（ML服务）** | 作为服务部署的ML实例，用于支持使用API端点进行培训和评分的按需请求。 还可以使用现有的已培训实验运行创建ML服务。 |

## 使用现有培训实验运行和计划评分创建ML服务

当您将培训实验运行作为ML服务发布时，可以通过提供评分实验运行POST请求的有效负荷的详细信息来计划评分。 这会导致创建用于评分的计划实验实体。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}'
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
| `mlInstanceId` | 现有ML实例标识、用于创建ML服务的培训实验运行应与此特定ML实例相对应。 |
| `trainingExperimentId` | 与ML实例识别对应的实验识别。 |
| `trainingExperimentRunId` | 用于发布ML服务的特定培训“Experience Run”。 |
| `scoringDataSetId` | 参考要用于计划评分实验运行的特定数据集的标识。 |
| `scoringTimeframe` | 一个整数值，表示用于筛选数据以用于评分“Emperience Runs”的分钟数。 例如，值`10080`表示过去10080分钟或168小时内的数据将用于每个计划的评分实验运行。 请注意，值`0`将不会筛选数据，数据集中的所有数据都将用于评分。 |
| `scoringSchedule` | 包含有关计划评分实验运行的详细信息。 |
| `scoringSchedule.startTime` | 日期时间指示何时开始评分。 |
| `scoringSchedule.endTime` | 日期时间指示何时开始评分。 |
| `scoringSchedule.cron` | Cron值，指示对“实验运行”进行评分的间隔。 |

**响应**

成功的响应返回新创建的ML服务的详细信息，包括其唯一`id`和其相应评分实验的`scoringExperimentId`。


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

根据您的特定用例和要求，使用ML实例创建ML服务在计划培训和评分实验运行方面是灵活的。 本教程将介绍以下具体案例：

- [您不需要计划培训，但需要计划得分。](#ml-service-with-scheduled-experiment-for-scoring)
- [您需要为培训和得分安排实验运行。](#ml-service-with-scheduled-experiments-for-training-and-scoring)

请注意，可以使用ML实例创建ML服务，无需计划任何培训或评分实验。 此类ML服务将创建普通的实验实体和用于培训和评分的单个实验运行。

### 针对评分{#ml-service-with-scheduled-experiment-for-scoring}进行计划实验的ML服务

可以通过发布具有计划Emperic Runs的ML实例来创建ML服务，该实例将创建用于培训的普通Experient实体。 将生成一个培训实验运行，并将用于所有计划的得分实验运行。 确保您具有创建ML服务所需的`mlInstanceId`、`trainingDataSetId`和`scoringDataSetId`，并且它们存在且是有效值。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
| `trainingDataSetId` | 参考用于培训实验的特定数据集的标识。 |
| `trainingTimeframe` | 一个整数值，表示用于过滤数据以用于培训实验的分钟数。 例如，值`"10080"`表示过去10080分钟或168小时的数据将用于培训“Experience Run”。 请注意，值`"0"`将不会过滤数据，数据集中的所有数据都将用于培训。 |
| `scoringDataSetId` | 参考要用于计划评分实验运行的特定数据集的标识。 |
| `scoringTimeframe` | 一个整数值，表示用于筛选数据以用于评分“Emperience Runs”的分钟数。 例如，值`"10080"`表示过去10080分钟或168小时内的数据将用于每个计划的评分实验运行。 请注意，值`"0"`将不会筛选数据，数据集中的所有数据都将用于评分。 |
| `scoringSchedule` | 包含有关计划评分实验运行的详细信息。 |
| `scoringSchedule.startTime` | 日期时间指示何时开始评分。 |
| `scoringSchedule.endTime` | 日期时间指示何时开始评分。 |
| `scoringSchedule.cron` | Cron值，指示对“实验运行”进行评分的间隔。 |

**响应**

成功的响应会返回新创建的ML服务的详细信息。 这包括该服务的唯一`id`，以及相应的培训和得分实验的`trainingExperimentId`和`scoringExperimentId`。

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

### ML服务，包含训练和评分的计划实验{#ml-service-with-scheduled-experiments-for-training-and-scoring}

要将现有ML实例作为具有计划培训和评分实验运行的ML服务发布，您需要提供培训和评分计划。 创建此配置的ML服务时，还会为培训和评分创建计划实验实体。 请注意，培训和得分计划不一定相同。 在评分作业执行期间，将获取由计划培训实验运行生成的最新培训模型并用于计划的得分运行。

**API格式**

```http
POST /mlServices
```

**请求**

```SHELL
curl -X POST 'https://platform-int.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
| `trainingDataSetId` | 参考用于培训实验的特定数据集的标识。 |
| `trainingTimeframe` | 一个整数值，表示用于过滤数据以用于培训实验的分钟数。 例如，值`"10080"`表示过去10080分钟或168小时的数据将用于培训“Experience Run”。 请注意，值`"0"`将不会过滤数据，数据集中的所有数据都将用于培训。 |
| `scoringDataSetId` | 参考要用于计划评分实验运行的特定数据集的标识。 |
| `scoringTimeframe` | 一个整数值，表示用于筛选数据以用于评分“Emperience Runs”的分钟数。 例如，值`"10080"`表示过去10080分钟或168小时内的数据将用于每个计划的评分实验运行。 请注意，值`"0"`将不会筛选数据，数据集中的所有数据都将用于评分。 |
| `trainingSchedule` | 包含有关计划培训实验运行的详细信息。 |
| `scoringSchedule` | 包含有关计划评分实验运行的详细信息。 |
| `scoringSchedule.startTime` | 日期时间指示何时开始评分。 |
| `scoringSchedule.endTime` | 日期时间指示何时开始评分。 |
| `scoringSchedule.cron` | Cron值，指示对“实验运行”进行评分的间隔。 |

**响应**

成功的响应会返回新创建的ML服务的详细信息。 这包括该服务的唯一`id`，以及相应培训和评分实验的`trainingExperimentId`和`scoringExperimentId`。 在下面的示例响应中，`trainingSchedule`和`scoringSchedule`的出现表明用于培训和评分的实验实体是计划的实验。

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

## 查找ML服务{#retrieving-ml-services}

您可以通过向`/mlServices`发出`GET`请求并在路径中提供ML服务的唯一`id`来查找现有ML服务。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
>检索不同的ML服务可能会返回具有或多或少键值对的响应。 上述响应是[ML服务的表示，该服务包含计划培训和评分实验运行](#ml-service-with-scheduled-experiments-for-training-and-scoring)。


## 计划培训或评分

如果要计划已发布的ML服务的评分和培训，可以通过在`/mlServices`上使用`PUT`请求更新现有ML服务来执行此操作。

**API格式**

```http
PUT /mlServices/{SERVICE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SERVICE_ID}` | 要更新的ML服务的唯一`id`。 |

**请求**

以下请求通过添加`trainingSchedule`和`scoringSchedule`键以及各自的`startTime`、`endTime`和`cron`键，计划现有ML服务的培训和评分。

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
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
>请勿尝试修改现有计划培训和评分作业上的`startTime`。 如果`startTime`必须修改，请考虑发布相同的模型并重新计划培训和评分作业。

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

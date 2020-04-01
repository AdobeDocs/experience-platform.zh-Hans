---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: 将模型发布为服务(API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 将模型发布为服务(API)

## 先决条件

- 请阅读本 [教程](../../tutorials/authentication.md) ，了解授权进行API调用的开始。
在教程中，您现在应该有以下信息：
   - `{ACCESS_TOKEN}`:身份验证后提供的特定承载令牌值。
   - `{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。
   - `{API_KEY}`:您在独特的Adobe Experience Platform集成中可找到特定API密钥价值。
- 本教程需要现有的ML引擎、ML实例和实验实体。 请参阅本教 [程](./import-packaged-recipe-api.md) （关于创建ML引擎、ML实例或实验实体）。
- 有关本教程中提到的API端点和请求的信息，请查阅完整的 [Sensei机器学习API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)。

## 主要条款

本教程中使用的一些常见术语：

| 搜索词 | 定义 |
--- | ---
| **机器学习实例（ML实例）** | 概念实体，它是由特定数据、参数和Sensei代码组成的特定租户的Sensei引擎的实例。 |
| **实验** | 用于保持培训实验运行和／或评分实验运行的伞形实体。 |
| **计划实验** | 用于描述培训或评分实验运行自动化的术语，受用户定义的计划管辖。 |
| **实验运行** | 培训或评分实验的特定实例。 特定实验的多个实验运行可能不同于用于培训或评分的数据集值。 |
| **培训的模型** | 通过试验和特征工程过程创建的机器学习模型，然后到达一个经过验证、评估和最终确定的模型。 |
| **发布模型** | 经过培训、验证和评估后，最终确定的版本化模型即可到达。 |
| **机器学习服务（ML服务）** | 部署为服务的ML实例，用于通过端点支持针对培训和评分的点播请求。 请注意，还可以使用现有的经过培训的实验运行创建ML服务。 |


## API工作流

本教程将介绍如何创建、检索和更新ML服务。

## 使用现有培训实验运行和计划评分创建ML服务

将培训实验运行作为ML服务发布时，您可以通过在{JSON_PAYLOAD}中提供评分实验运行的详细信息来计划 `scoringSchedule` 评分。 这会导致创建用于评分的计划实验实体。 确保您有、 `mlInstanceId`、 `trainingExperimentId`、 `trainingExperimentRunId`、以 `scoringDataSetId`及它们存在且是有效值。

对于开始，请 `POST` 向提出请 `/mlServices`求。 curl命令示例如下：

**请求**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` :您在独特的Adobe Experience Platform集成中可找到特定API密钥价值。
- `{IMS_ORG}` : 您的IMS组织ID位于Adobe I/O控制台的集成详细信息下。
- `{ACCESS_TOKEN}` :身份验证后提供的特定承载令牌值。
- `{JSON_PAYLOAD}` :JSON有效负荷格式示例如下：

```JSON
{
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  }
}
```

- `mlInstanceId` :现有的ML实例标识，用于创建ML服务的培训实验运行应与此特定ML实例对应。
- `trainingExperimentId` :与ML实例标识对应的实验标识。
- `trainingExperimentRunId` :用于发布ML服务的特定培训实验运行。
- `scoringDataSetId` :引用用于计划评分实验运行的特定数据集的标识。
- `scoringTimeframe` :一个整数值，表示用于过滤数据以用于评分“实验运行”的分钟数。 例如，每个计划的 `"10080"` 评分实验运行将使用过去10080分钟或168小时的均值数据。 请注意，值不会过 `"0"` 滤数据，数据集中的所有数据都将用于评分。
- `scoringSchedule` :包含有关计划评分实验运行的详细信息。
- `startTime` : 定义.
- `endTime` : 定义.
- `cron` : 定义.

**响应**

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

从JSON响应中，键及其相 `scoringExperimentId` 应值表示已创建一个新的评分实验，以及您在请求中提供的实验计划 `POST` 。 响 `id` 应中的键可唯一标识已创建的ML服务。

## 从现有ML实例创建ML服务

根据您的特定用例和要求，使用ML实例创建ML服务在计划培训和评分实验运行方面是灵活的。 本教程将介绍以下具体情况：

- [您不需要计划培训，但需要计划评分。](#ml-service-with-scheduled-experiment-for-scoring)
- [您需要计划的实验运行才能进行培训和评分。](#ml-service-with-scheduled-experiments-for-training-and-scoring)

请注意，可以使用ML实例创建ML服务，而无需安排任何培训或评分实验。 此类ML服务将创建普通的实验实体和单个实验运行以进行培训和评分。

### ML服务（带有计划评分实验）

通过发布具有计划实验运行的ML实例进行评分来创建ML服务，将导致创建用于培训的普通实验实体。 生成的培训实验运行将用于所有计划的评分实验运行。 确保您具有创 `mlInstanceId`建ML服务 `trainingDataSetId`所 `scoringDataSetId` 需的、和必需的值，并且这些值存在且是有效值。

对于开始，请 `POST` 向提出请 `/mlServices`求。 curl命令示例如下：

**请求**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {IMS_ORG}' 
  -d '{JSON_PAYLOAD}'
```

- `{API_KEY}` :您在独特的Adobe Experience Platform集成中可找到特定API密钥价值。
- `{IMS_ORG}` : 您的IMS组织ID位于Adobe I/O控制台的集成详细信息下。
- `{ACCESS_TOKEN}` :身份验证后提供的特定承载令牌值。
- `{JSON_PAYLOAD}` :JSON有效负荷格式示例如下：

```JSON
{
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
}
```

| JSON密钥 | 描述 |
| --- | --- |
| **`mlInstanceId`** | 现有ML实例标识，表示用于创建ML服务的ML实例。 |
| **`trainingDataSetId`** | 参考用于培训实验的特定数据集的标识。 |
| **`trainingTimeframe`** | 一个整数值，表示用于过滤数据以用于培训实验的分钟数。 例如，训练实 `"10080"` 验运行将使用过去10080分钟或168小时的均值数据。 请注意，值不会过 `"0"` 滤数据，数据集中的所有数据都将用于培训。 |
| **`scoringDataSetId`** | 引用用于计划评分实验运行的特定数据集的标识。 |
| **`scoringTimeframe`** | 一个整数值，表示用于过滤数据以用于评分“实验运行”的分钟数。 例如，每个计划的 `"10080"` 评分实验运行将使用过去10080分钟或168小时的均值数据。 请注意，值不会过 `"0"` 滤数据，数据集中的所有数据都将用于评分。 |
| **`scoringSchedule`** | 包含有关计划评分实验运行的详细信息。 |

**响应**

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

根据响 `JSON` 应，键和建议 `trainingExperimentId` 为 `scoringExperimentId` 此ML服务创建了一个新的培训和评分实验实体。 对象的存在引 `scoringSchedule` 用了有关评分实验运行计划的详细信息。 响 `id` 应中的键指您刚刚创建的ML服务。

### ML服务（包含针对培训和评分的定期实验）

要将现有ML实例作为具有计划培训和评分实验运行的ML服务发布，您需要提供培训和评分计划。 创建此配置的ML服务时，还会为培训和评分创建计划的实验实体。 请注意，培训和评分计划不一定相同。 在评分作业执行期间，将获取由计划培训实验运行生成的最新培训模型并将其用于计划的评分运行。

要创建ML服务，请使 `POST` 用表示 `/mlServices` 要添加 `{JSON_PAYLOAD}` 的ML服务对象的请求。 请确保 `mlInstanceId`、 `trainingDataSetId`和 `scoringDataSetId` 存在且为有效值。

**请求**

```SHELL
curl -X POST "https://platform-int.adobe.io/data/sensei/mlServices" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{API_KEY}` :您在独特的Adobe Experience Platform集成中可找到特定API密钥价值。
- `{IMS_ORG}` : 您的IMS组织ID位于Adobe I/O控制台的集成详细信息下。
- `{ACCESS_TOKEN}` :身份验证后提供的特定承载令牌值。
- `{JSON_PAYLOAD}` :JSON有效负荷格式示例如下：

```JSON
{
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
}
```

| JSON密钥 | 描述 |
| --- | --- |
| **`mlInstanceId`** | 现有ML实例标识，表示用于创建ML服务的ML实例。 |
| **`trainingDataSetId`** | 参考用于培训实验的特定数据集的标识。 |
| **`trainingTimeframe`** | 一个整数值，表示用于过滤数据以用于培训实验的分钟数。 例如，训练实 `"10080"` 验运行将使用过去10080分钟或168小时的均值数据。 请注意，值不会过 `"0"` 滤数据，数据集中的所有数据都将用于培训。 |
| **`scoringDataSetId`** | 引用用于计划评分实验运行的特定数据集的标识。 |
| **`scoringTimeframe`** | 一个整数值，表示用于过滤数据以用于评分“实验运行”的分钟数。 例如，每个计划的 `"10080"` 评分实验运行将使用过去10080分钟或168小时的均值数据。 请注意，值不会过 `"0"` 滤数据，数据集中的所有数据都将用于评分。 |
| **`trainingSchedule`** | 包含有关计划培训实验运行的详细信息。 |
| **`scoringSchedule`** | 包含有关计划评分实验运行的详细信息。 |

**响应**

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

在响应体中 `trainingExperimentId` 加入 `scoringExperimentId` 和加入，表明为培训和得分创建了实验实体。 上述用于培 `trainingSchedule` 训和评 `scoringSchedule` 分的实验实体是预定的实验。 响 `id` 应中的键指您刚刚创建的ML服务。

## 检索ML服务

检索现有ML服务与向端点发出请求一样 `GET` 简单 `/mlServices` 。 确保您尝试检索的特定ML服务具有ML服务标识。

**请求**

```SHELL
curl -X GET "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: Bearer {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
```

- `{API_KEY}` :您在独特的Adobe Experience Platform集成中可找到特定API密钥价值。
- `{IMS_ORG}` : 您的IMS组织ID位于Adobe I/O控制台的集成详细信息下。
- `{ACCESS_TOKEN}` :身份验证后提供的特定承载令牌值。

**响应**

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

JSON响应表示ML服务对象。 此对象等效于创建ML服务时的响应。 请注意，检索不同的ML服务可能会返回具有或多或少键值对的响应。 以上响应是具有计划培训和 [评分实验运行的ML服务的表示](#ml-service-with-scheduled-experiments-for-training-and-scoring)。


## 计划培训或评分

假设您要计划已发布的ML服务的评分和培训，可以通过更新现有ML服务并在上发出请 `PUT` 求来完成 `/mlServices`。 确保拥有要更新的ML服务标识。 检索要更 [新的ML服务](#retrieving-ml-services) ，可能是有用的第一步。

**请求**

```SHELL
curl -X PUT "https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}" 
  -H "Authorization: {ACCESS_TOKEN}" 
  -H "x-api-key: {API_KEY}" 
  -H "x-gw-ims-org-id: {IMS_ORG}" 
  -d "{JSON_PAYLOAD}"
```

- `{SERVICE_ID}` :唯一标识，指要更新的ML服务。
- `{API_KEY}` :您在独特的Adobe Experience Platform集成中可找到特定API密钥价值。
- `{IMS_ORG}` : 您的IMS组织ID位于Adobe I/O控制台的集成详细信息下。
- `{ACCESS_TOKEN}` :身份验证后提供的特定承载令牌值。
- `{JSON_PAYLOAD}` :JSON有效负荷格式示例如下：

```JSON
{
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
}
```

通过添加和键及其各自的键，可以 `trainingSchedule` 执行培 `scoringSchedule` 训和评分 `startTime`的计划 `endTime`和 `cron` 计分。

>[!NOTE] 上的 `PUT` 请求 `mlServices` 允许您使用现有的预定实验运行修改服务。 请 **勿尝试修改现有计划**`startTime` 培训和评分作业上的作业。 如果必须 `startTime` 修改模型，请考虑发布相同的模型并重新计划培训和评分任务。

**响应**

响应将是对象， `{JSON_PAYLOAD}` 但对象中 `id`有 `created`额外的、 `updated` 和键。

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

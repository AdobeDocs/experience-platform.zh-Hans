---
keywords: Experience Platform；培训和评估；数据科学工作区；热门主题；Sensei机器学习API
solution: Experience Platform
title: 利用Sensei机器学习API训练和评估模型
topic-legacy: tutorial
type: Tutorial
description: 本教程将向您展示如何使用Sensei机器学习API调用创建、培训和评估模型。
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 1%

---

# 使用 [!DNL Sensei Machine Learning] API


本教程将向您展示如何使用API调用创建、培训和评估模型。 请参阅 [本文档](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) ，以获取API文档的详细列表。

## 先决条件

关注 [使用API导入打包的方法](./import-packaged-recipe-api.md) 用于创建引擎，需要使用API来训练和评估模型。

关注 [Experience PlatformAPI身份验证教程](https://www.adobe.com/go/platform-api-authentication-en) 以开始进行API调用。

在教程中，您现在应该具有以下值：

- `{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。
- `{ORG_ID}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。
- `{API_KEY}`:您在独特的Adobe Experience Platform集成中找到的特定API密钥值。

- 链接到智能服务的Docker图像

## API工作流

我们将使用API来创建用于培训的实验运行。 在本教程中，我们将重点介绍引擎、MLInstance和实验端点。 下图概述了三者之间的关系，还介绍了“运行”(Run)和“模型”(Model)的概念。

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>术语“Engine”、“MLInstance”、“MLService”、“Experiment”和“Model”在UI中被称为不同的术语。 如果您来自UI，下表会映射差异。

| UI术语 | API术语 |
| --- | --- |
| 方法 | 引擎 |
| 模型 | MLInstance |
| 培训运行 | 实验 |
| 服务 | MLService |

### 创建MLInstance

可使用以下请求创建MLInstance。 您将使用 `{ENGINE_ID}` 从创建引擎时返回的 [使用API导入打包的方法](./import-packaged-recipe-ui.md) 教程。

**请求**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
`{ORG_ID}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中找到的特定API密钥值。\
`{JSON_PAYLOAD}`:MLInstance的配置。 下面显示了我们在教程中使用的示例：

```JSON
{
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [
                {
                    "key": "numFeatures",
                    "value": "10"
                },
                {
                    "key": "maxIter",
                    "value": "2"
                },
                {
                    "key": "regParam",
                    "value": "0.15"
                },
                {
                    "key": "trainingDataLocation",
                    "value": "sample_training_data.csv"
                }
            ]
        },
        {
            "name": "score",
            "parameters": [
                {
                    "key": "scoringDataLocation",
                    "value": "sample_scoring_data.csv"
                },
                {
                    "key": "scoringResultsLocation",
                    "value": "scoring_results.net"
                }
            ]
        }
    ]
}
```

>[!NOTE]
>
>在 `{JSON_PAYLOAD}`，我们将定义用于在 `tasks` 数组。 的 `{ENGINE_ID}` 是要使用的引擎的ID，以及 `tag` 字段是用于标识实例的可选参数。

响应包含 `{INSTANCE_ID}` 表示所创建的MLInstance。 可以创建具有不同配置的多模型MLInstance。

**响应**

```JSON
{
    "id": "{INSTANCE_ID}",
    "name": "Retail - Instance",
    "description": "Instance for ML Instance",
    "engineId": "{ENGINE_ID}",
    "created": "2018-21-21T11:11:11.111Z",
    "createdBy": {
        "displayName": "John Doe",
        "userId": "johnd"
    },
    "updated": "2018-21-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "purpose": "tutorial"
    },
    "tasks": [
        {
            "name": "train",
            "parameters": [...]
        },
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{ENGINE_ID}`:此ID表示在下创建MLInstance的引擎。\
`{INSTANCE_ID}`:表示MLInstance的ID。

### 创建实验

数据科学家在训练时使用实验来获得高性能模型。 多个实验包括更改数据集、功能、学习参数和硬件。 以下是创建实验的示例。

**请求**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{ORG_ID}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。\
`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中找到的特定API密钥值。\
`{JSON_PAYLOAD}`:创建的实验对象。 下面显示了我们在教程中使用的示例：

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`:表示MLInstance的ID。

实验创建的响应如下所示。

**响应**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-01-01T11:11:11.111Z",
    "updated": "2018-01-01T11:11:11.111Z",
    "deleted": false,
    "tags": {
        "test": "guide"
    }
}
```

`{EXPERIMENT_ID}`:表示您刚刚创建的实验的ID。
`{INSTANCE_ID}`:表示MLInstance的ID。

### 为培训创建计划实验

使用了计划实验，这样我们便无需通过API调用创建每个单次实验运行。 相反，我们会在实验创建期间提供所有必需的参数，并且每次运行都将定期创建。

要指示创建计划实验，我们必须添加 `template` 请求正文中的部分。 在 `template`，则包含计划运行的所有必需参数，例如 `tasks`，指示什么操作和 `schedule`，表示计划运行的时间。

**请求**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{ORG_ID}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。\
`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中找到的特定API密钥值。\
`{JSON_PAYLOAD}`:要发布的数据集。 下面显示了我们在教程中使用的示例：

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "train",
            "parameters": [
                   {
                        "value": "1000",
                        "key": "numFeatures"
                    }
            ],
            "specification": {
                "type": "SparkTaskSpec",
                "executorCores": 5,
                "numExecutors": 5
            }
        }],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-11-11",
            "endTime": "2019-11-11"
        }
    }
}
```

当我们创建实验时，身体， `{JSON_PAYLOAD}`，应包含 `mlInstanceId` 或 `mlInstanceQuery` 参数。 在此示例中，计划实验将每20分钟调用一次运行，该运行在 `cron` 参数，从 `startTime` 直到 `endTime`.

**响应**

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "created": "2018-11-11T11:11:11.111Z",
    "updated": "2018-11-11T11:11:11.111Z",
    "deleted": false,
    "workflowId": "endid123_0379bc0b_8f7e_4706_bcd9_1a2s3d4f5g_abcdf",
    "template": {
        "tasks": [
            {
                "name": "train",
                "parameters": [...],
                "specification": {
                    "type": "SparkTaskSpec",
                    "executorCores": 5,
                    "numExecutors": 5
                }
            }
        ],
        "schedule": {
            "cron": "*/20 * * * *",
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{EXPERIMENT_ID}`:表示实验的ID。\
`{INSTANCE_ID}`:表示MLInstance的ID。


### 创建用于培训的实验运行

创建实验实体后，可以使用以下调用创建并运行培训运行。 您将需要 `{EXPERIMENT_ID}` 说明 `mode` 要在请求正文中触发。

**请求**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{EXPERIMENT_ID}`:与要定位的实验对应的ID。 这可在创建实验时的响应中找到。\
`{ORG_ID}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。\
`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中找到的特定API密钥值。\
`{JSON_PAYLOAD}`:要创建培训运行，您必须在正文中包含以下内容：

```JSON
{
    "mode":"Train"
}
```

您还可以通过在 `tasks` 数组：

```JSON
{
   "mode":"Train",
   "tasks": [
        {
           "name": "train",
           "parameters": [
                {
                   "key": "numFeatures",
                   "value": "2"
                }
            ]
        }
    ]
}
```

您将收到以下响应，该响应将告知您 `{EXPERIMENT_RUN_ID}` 和 `tasks`.

**响应**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "train",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.903Z",
    "updated": "2018-01-01T11:11:11.903Z",
    "deleted": false,
    "tasks": [
        {
            "name": "Train",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`:表示实验运行的ID。\
`{EXPERIMENT_ID}`:表示“实验运行”所在实验的ID。

### 检索实验运行状态

可以使用 `{EXPERIMENT_RUN_ID}`.

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`:表示实验的ID。\
`{EXPERIMENT_RUN_ID}`:表示实验运行的ID。\
`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
`{ORG_ID}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中找到的特定API密钥值。

**响应**

GET调用将提供 `state` 参数，如下所示：

```JSON
{
    "id": "{EXPERIMENT_ID}",
    "name": "RunStatus for experimentRunId {EXPERIMENT_RUN_ID}",
    "experimentRunId": "{EXPERIMENT_RUN_ID}",
    "deleted": false,
    "status": {
        "tasks": [
            {
                "id": "{MODEL_ID}",
                "state": "DONE",
                "tasklogs": [
                    {
                        "name": "execution",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stderr",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    },
                    {
                        "name": "stdout",
                        "url": "https://mlbaprod1sapwd7jzid.file.core.windows.net/..."
                    }
                ]
            }
        ]
    }
}
```

`{EXPERIMENT_RUN_ID}`:表示实验运行的ID。\
`{EXPERIMENT_ID}`:表示“实验运行”所在实验的ID。

除 `DONE` 状态，其他状态包括：
- `PENDING`
- `RUNNING`
- `FAILED`

要获取更多信息，详细日志可在 `tasklogs` 参数。

### 检索已训练的模型

为了在培训期间创建上述培训模型，我们提出以下请求：

**请求**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_RUN_ID}`:与要定位的“实验运行”对应的ID。 创建“实验运行”时，可在响应中找到该响应。\
`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
`{ORG_ID}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。

响应表示已创建的受训模型。

**响应**

```JSON
{
    "children": [
        {
            "id": "{MODEL_ID}",
            "name": "Tutorial trained Model",
            "experimentId": "{EXPERIMENT_ID}",
            "experimentRunId": "{EXPERIMENT_RUN_ID}",
            "description": "trained model for ID",
            "modelArtifactUri": "wasb://test-models@mlpreprodstorage.blob.core.windows.net/{MODEL_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z",
            "deleted": false
        }
    ],
    "_page": {
        "property": "ExperimentRunId=={EXPERIMENT_RUN_ID},deleted!=true",
        "count": 1
    }
}
```

`{MODEL_ID}`:与模型对应的ID。\
`{EXPERIMENT_ID}`:与“实验运行”(Experience Run)对应的ID在下。\
`{EXPERIMENT_RUN_ID}`:与“实验运行”对应的ID。

### 停止和删除计划的实验

如果要在计划实验之前停止执行该实验 `endTime`，可通过查询向 `{EXPERIMENT_ID}`

**请求**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`:与实验对应的ID。\
`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
`{ORG_ID}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。

>[!NOTE]
>
>API调用将禁用创建新的实验运行。 但是，它不会停止执行已在运行的实验运行。

以下是通知实验已成功删除的响应。

**响应**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## 后续步骤

本教程介绍了如何使用API创建引擎、实验、计划实验运行和培训的模型。 在 [下一次练习](./score-model-api.md)，您将使用性能最佳的训练模型对新数据集进行评分，从而做出预测。

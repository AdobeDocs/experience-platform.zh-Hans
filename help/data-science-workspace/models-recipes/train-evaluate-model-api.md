---
keywords: Experience Platform;train and evaluate;Data Science Workspace;popular topics
solution: Experience Platform
title: 培训和评估模型(API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 培训和评估模型(API)


本教程将向您介绍如何使用API调用创建、培训和评估模型。 有关API [文档的详细列表](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) ，请参阅本文档。

## 先决条件

按照使 [用API导入打包的菜谱](./import-packaged-recipe-api.md) ，以创建引擎，该引擎需要使用API来培训和评估模型。

请阅读本 [教程](../../tutorials/authentication.md) ，了解授权进行API调用的开始。

在教程中，您现在应具有以下值：

- `{ACCESS_TOKEN}`:身份验证后提供的特定承载令牌值。
- `{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。
- `{API_KEY}`:您在独特的Adobe Experience Platform集成中可找到特定API密钥价值。

- 链接到智能服务的Docker图像

## API工作流程

我们将使用API创建用于培训的实验运行。 在本教程中，我们将重点介绍 **Engine**、 **MLInstances**&#x200B;和 **Experies** 端点。 下图概述了这三者之间的关系，并介绍了“运行”(Run)和“模型”(Model)的概念。

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE] 术语“引擎”、“MLInstance”、“MLService”、“实验”和“模型”在UI中称为不同术语。 如果您来自UI，下表将映射差异。
> 
> | UI期限 | API期限 |
> --- | ---
> | 菜谱 | 引擎 |
> | 模型 | MLInstance |
> | 培训运行 | 实验 |
> | 服务 | MLService |



### 创建MLInstance

可以使用以下请求创建MLI实例。 您将使用在使用 `{ENGINE_ID}` API教程从导入打包的菜谱中 [创建引擎时返回的引擎](./import-packaged-recipe-ui.md) 。

**请求**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/mlInstances \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=mlInstance.v1.json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d `{JSON_PAYLOAD}`
```

`{ACCESS_TOKEN}`:身份验证后提供的特定承载令牌值。\
`{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中可找到特定API密钥价值。\
`{JSON_PAYLOAD}`:MLI实例的配置。 我们在教程中使用的示例如下：

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

>[!NOTE] 在中，我 `{JSON_PAYLOAD}`们定义了用于阵列中训练和评分的参 `tasks` 数。 该字 `{ENGINE_ID}` 段是您要使用的引擎的ID，而该字段 `tag` 是用于标识实例的可选参数。

响应将包含表示 `{INSTANCE_ID}` 所创建MLI实例的响应。 可以创建具有不同配置的多模型MLI实例。

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

`{ENGINE_ID}`:此ID表示MLInstance创建于下的引擎。\
`{INSTANCE_ID}`:表示MLInstance的ID。

### 创建实验

数据科学家使用实验来在训练时获得高性能的模型。 多个实验包括更改数据集、功能、学习参数和硬件。 以下是创建实验的示例。

**请求**

```SHELL
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY' \
  -d `{JSON PAYLOAD}`
```

`{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。\
`{ACCESS_TOKEN}`:身份验证后提供的特定承载令牌值。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中可找到特定API密钥价值。\
`{JSON_PAYLOAD}`:实验创建的对象。 我们在教程中使用的示例如下：

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

“实验”创建的响应如下所示。

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

使用计划实验，这样我们就无需通过API调用创建每个实验运行。 相反，我们在实验创建过程中提供所有必需的参数，每次运行都将定期创建。

要指示创建计划实验，我们必须在请 `template` 求正文中添加一个部分。 在 `template`中，包含调度运行的所有必要参数，如 `tasks`，指示什么操作，以及 `schedule`，指示调度运行的时间。

**请求**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}`
```

`{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。\
`{ACCESS_TOKEN}`:身份验证后提供的特定承载令牌值。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中可找到特定API密钥价值。\
`{JSON_PAYLOAD}`:要发布的数据集。 我们在教程中使用的示例如下：

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

创建实验时，主体应 `{JSON_PAYLOAD}`包含或参 `mlInstanceId` 数 `mlInstanceQuery` 。 在此示例中，计划的实验将每20分钟调用一次运行，该运行在参数中设置， `cron` 从开始到 `startTime` 结束 `endTime`。

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


### 为培训创建实验运行

创建实验实体后，可以使用下面的调用创建并运行培训运行。 您需要在请 `{EXPERIMENT_ID}` 求主体中 `mode` 声明要触发的内容。

**请求**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{EXPERIMENT_ID}`:与要目标的实验对应的ID。 这可以在创建实验时的响应中找到。\
`{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。\
`{ACCESS_TOKEN}`:身份验证后提供的特定承载令牌值。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中可找到特定API密钥价值。\
`{JSON_PAYLOAD}`:要创建培训运行，您必须在正文中包含以下内容：

```JSON
{
    "mode":"Train"
}
```

您还可以通过包括数组来覆盖配置参 `tasks` 数：

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

您将收到以下响应，通知您下 `{EXPERIMENT_RUN_ID}` 的配置和配置 `tasks`。

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

`{EXPERIMENT_RUN_ID}`: 表示“实验运行”的ID。\
`{EXPERIMENT_ID}`:表示“实验运行”所在实验的ID。

### 检索“实验运行”状态

可以使用查询实验运行的状态 `{EXPERIMENT_RUN_ID}`。

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`:表示实验的ID。\
`{EXPERIMENT_RUN_ID}`:表示“实验运行”的ID。\
`{ACCESS_TOKEN}`:身份验证后提供的特定承载令牌值。\
`{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中可找到特定API密钥价值。

**响应**

GET调用将提供参数中的状 `state` 态，如下所示：

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

`{EXPERIMENT_RUN_ID}`: 表示“实验运行”的ID。\
`{EXPERIMENT_ID}`:表示“实验运行”所在实验的ID。

除了州之外， `DONE` 其他州还包括：
- `PENDING`
- `RUNNING`
- `FAILED`

要获取更多信息，可在参数下找到详细的日 `tasklogs` 志。

### 检索经过培训的模型

为了在培训期间创建上述培训模型，我们提出以下请求：

**请求**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_RUN_ID}`:与要目标的“实验运行”对应的ID。 这可以在创建实验运行时的响应中找到。\
`{ACCESS_TOKEN}`:身份验证后提供的特定承载令牌值。\
`{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。

响应表示已创建的经过培训的模型。

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

`{MODEL_ID}`:与“模型”(Model)对应的ID。\
`{EXPERIMENT_ID}`: 与“实验运行”对应的ID在“实验运行”下。\
`{EXPERIMENT_RUN_ID}`:与“实验运行”对应的ID。

### 停止和删除计划的实验

如果要在计划实验之前停止执行该实验， `endTime`可以通过向 `{EXPERIMENT_ID}`

**请求**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`: 与实验对应的ID。\
`{ACCESS_TOKEN}`:身份验证后提供的特定承载令牌值。\
`{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。

>[!NOTE] API调用将禁用新实验运行的创建。 但是，它不会停止执行已运行的实验运行。

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

本教程介绍了如何使用API创建引擎、实验、计划实验运行和经过培训的模型。 在下一 [个练习中](./score-model-api.md)，您将使用表现最好的培训模型对新数据集进行评分，从而做出预测。
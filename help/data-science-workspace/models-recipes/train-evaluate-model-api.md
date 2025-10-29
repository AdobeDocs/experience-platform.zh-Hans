---
keywords: Experience Platform；培训和评估；数据科学Workspace；热门主题；Sensei机器学习API
solution: Experience Platform
title: 使用Sensei机器学习API训练和评估模型
type: Tutorial
description: 本教程将向您展示如何使用Sensei机器学习API调用创建、训练和评估模型。
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 1%

---

# 使用[!DNL Sensei Machine Learning] API训练和评估模型

>[!NOTE]
>
>数据科学Workspace不再可供购买。
>
>本文档面向之前有权访问数据科学Workspace的现有客户。

本教程将向您展示如何使用API调用创建、训练和评估模型。 有关API文档的详细列表，请参阅[此文档](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/)。

## 先决条件

按照[使用API导入打包的方法](./import-packaged-recipe-api.md)创建引擎，使用API训练和评估模型需要该引擎。

按照[Experience Platform API身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)中的说明开始进行API调用。

在本教程中，您现在应该具有以下值：

- `{ACCESS_TOKEN}`：在身份验证后提供的特定持有者令牌值。
- `{ORG_ID}`：在独特的Adobe Experience Platform集成中找到您的组织凭据。
- `{API_KEY}`：在独特的Adobe Experience Platform集成中找到特定的API密钥值。

- 链接到智能服务的Docker图像

## API工作流

我们将使用API来创建用于训练的试验运行。 在本教程中，我们将重点介绍“引擎”、“实例”和“实验”端点。 下表概述了三者之间的关系，还介绍了运行和模型的想法。

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>术语“Engine”、“MLInstance”、“MLService”、“Experiment”和“Model”在UI中称为不同的术语。 如果您来自UI，下表将列出二者的差异。

| UI术语 | API术语 |
| --- | --- |
| 方法 | 引擎 |
| 模型 | MLInstance |
| 训练运行 | 试验 |
| 服务 | MLService |

### 创建MLInstance

可以使用以下请求来创建MLInstance。 您将使用通过`{ENGINE_ID}`使用API导入打包的处方[教程创建引擎时返回的](./import-packaged-recipe-ui.md)。

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

`{ACCESS_TOKEN}`：在身份验证后提供的特定持有者令牌值。\
`{ORG_ID}`：在独特的Adobe Experience Platform集成中找到您的组织凭据。\
`{API_KEY}`：在独特的Adobe Experience Platform集成中找到特定的API密钥值。\
`{JSON_PAYLOAD}`：我们的MLInstance的配置。 我们在本教程中使用的示例如下所示：

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
>在`{JSON_PAYLOAD}`中，我们定义用于在`tasks`数组中训练和评分的参数。 `{ENGINE_ID}`是要使用的引擎的ID，`tag`字段是用于标识实例的可选参数。

响应包含表示所创建的MLInstance的`{INSTANCE_ID}`。 可以创建具有不同配置的多个模型MLI实例。

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

`{ENGINE_ID}`：此ID表示MLInstance是在其下创建的引擎。\
`{INSTANCE_ID}`：表示MLInstance的ID。

### 创建试验

数据科学家使用实验在训练时得出高性能模型。 多项实验包括更改数据集、特征、学习参数和硬件。 以下是创建试验的一个示例。

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

`{ORG_ID}`：在独特的Adobe Experience Platform集成中找到您的组织凭据。\
`{ACCESS_TOKEN}`：在身份验证后提供的特定持有者令牌值。\
`{API_KEY}`：在独特的Adobe Experience Platform集成中找到特定的API密钥值。\
`{JSON_PAYLOAD}`：创建的试验对象。 我们在本教程中使用的示例如下所示：

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`：表示MLInstance的ID。

试验创建的响应如下所示。

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

`{EXPERIMENT_ID}`：表示您刚刚创建的试验的ID。
`{INSTANCE_ID}`：表示MLInstance的ID。

### 创建计划的试验以进行训练

使用计划的实验，因此我们不需要通过API调用创建每个单独的实验运行。 相反，我们在试验创建期间提供了所有必需的参数，每次运行都将定期创建。

要指示计划试验的创建，我们必须在请求正文中添加`template`部分。 在`template`中，包含计划运行的所有必要参数，如`tasks`和`schedule`，前者指示执行的操作，后者指示计划运行的时间。

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

`{ORG_ID}`：在独特的Adobe Experience Platform集成中找到您的组织凭据。\
`{ACCESS_TOKEN}`：在身份验证后提供的特定持有者令牌值。\
`{API_KEY}`：在独特的Adobe Experience Platform集成中找到特定的API密钥值。\
`{JSON_PAYLOAD}`：要发布的数据集。 我们在本教程中使用的示例如下所示：

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

创建试验时，正文`{JSON_PAYLOAD}`应包含`mlInstanceId`或`mlInstanceQuery`参数。 在此示例中，计划试验将调用从`cron`到`startTime`的每20分钟运行一次（在`endTime`参数中设置）。

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

`{EXPERIMENT_ID}`：表示试验的ID。\
`{INSTANCE_ID}`：表示MLInstance的ID。


### 创建用于训练的试验运行

在创建试验实体后，可以使用以下调用创建并运行训练运行。 您将需要`{EXPERIMENT_ID}`并指明要在请求正文中触发的`mode`。

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

`{EXPERIMENT_ID}`：对应于要定位的试验的ID。 可在创建试验时的响应中找到此响应。\
`{ORG_ID}`：在独特的Adobe Experience Platform集成中找到您的组织凭据。\
`{ACCESS_TOKEN}`：在身份验证后提供的特定持有者令牌值。\
`{API_KEY}`：在独特的Adobe Experience Platform集成中找到特定的API密钥值。\
`{JSON_PAYLOAD}`：要创建训练运行，您必须在正文中包含以下内容：

```JSON
{
    "mode":"Train"
}
```

您还可以通过包含`tasks`数组来覆盖配置参数：

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

您将获得以下响应，此响应将让您知道`{EXPERIMENT_RUN_ID}`以及`tasks`下的配置。

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

`{EXPERIMENT_RUN_ID}`：表示试验运行的ID。\
`{EXPERIMENT_ID}`：表示试验运行所在试验的ID。

### 检索试验运行状态

可使用`{EXPERIMENT_RUN_ID}`查询试验运行的状态。

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`：表示试验的ID。\
`{EXPERIMENT_RUN_ID}`：表示试验运行的ID。\
`{ACCESS_TOKEN}`：在身份验证后提供的特定持有者令牌值。\
`{ORG_ID}`：在独特的Adobe Experience Platform集成中找到您的组织凭据。\
`{API_KEY}`：在独特的Adobe Experience Platform集成中找到特定的API密钥值。

**响应**

GET调用将在`state`参数中提供状态，如下所示：

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

`{EXPERIMENT_RUN_ID}`：表示试验运行的ID。\
`{EXPERIMENT_ID}`：表示试验运行所在试验的ID。

除了`DONE`状态之外，其他状态包括：

- `PENDING`
- `RUNNING`
- `FAILED`

要获取更多信息，可以在`tasklogs`参数下找到详细的日志。

### 检索经过训练的模型

为了在培训期间获得上面创建的经过培训的模型，我们提出了以下请求：

**请求**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_RUN_ID}`：与要定位的试验运行相对应的ID。 这可以在创建试验运行时的响应中找到。\
`{ACCESS_TOKEN}`：在身份验证后提供的特定持有者令牌值。\
`{ORG_ID}`：在独特的Adobe Experience Platform集成中找到您的组织凭据。

响应表示已创建的经过训练的模型。

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

`{MODEL_ID}`：与模型对应的ID。\
`{EXPERIMENT_ID}`：与试验运行的试验相对应的ID。\
`{EXPERIMENT_RUN_ID}`：与试验运行对应的ID。

### 停止并删除计划的试验

如果要在计划试验`endTime`之前停止执行它，可以通过查询`{EXPERIMENT_ID}`的DELETE请求来完成

**请求**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`：与试验对应的ID。\
`{ACCESS_TOKEN}`：在身份验证后提供的特定持有者令牌值。\
`{ORG_ID}`：在独特的Adobe Experience Platform集成中找到您的组织凭据。

>[!NOTE]
>
>API调用将禁用创建新试验运行。 但是，它不会停止执行已运行的试验运行。

以下是“响应”，通知已成功删除试验。

**响应**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## 后续步骤

本教程介绍了如何使用API创建引擎、实验、计划的实验运行和经过训练的模型。 在[下一个练习](./score-model-api.md)中，您将通过使用表现最佳的训练模型来评分新的数据集，从而做出预测。

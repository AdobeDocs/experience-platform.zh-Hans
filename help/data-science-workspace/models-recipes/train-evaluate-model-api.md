---
keywords: Experience Platform；培训和评估；数据科学工作区；热门主题；Sensei机器学习API
solution: Experience Platform
title: 基于Sensei机器学习API的模型训练与评价
topic: tutorial
type: Tutorial
description: 本教程将向您展示如何使用Sensei机器学习API调用创建、培训和评估模型。
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 1%

---


# 使用[!DNL Sensei Machine Learning] API培训和评估模型


本教程将向您展示如何使用API调用创建、培训和评估模型。 有关API文档的详细列表，请参阅[此文档](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)。

## 先决条件

按照[使用API](./import-packaged-recipe-api.md)导入打包的菜谱以创建引擎，该引擎需要使用API来培训和评估模型。

按照[Experience PlatformAPI身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)进行API调用的开始。

在教程中，您现在应当具有以下值：

- `{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。
- `{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。
- `{API_KEY}`:您在独特的Adobe Experience Platform集成中找到的特定API密钥值。

- 链接到智能服务的Docker图像

## API工作流

我们将使用API创建培训的实验运行。 在本教程中，我们将重点介绍引擎、MLI实例和实验端点。 下图概述了这三者之间的关系，并介绍了“运行”(Run)和“模型”(Model)的概念。

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>术语“引擎”、“MLInstance”、“MLService”、“实验”和“模型”在UI中称为不同术语。 如果您来自UI，下表将映射差异。
> 
> | UI术语 | API术语 |
> --- | ---
> | 菜谱 | 引擎 |
> | 模型 | MLInstance |
> | 培训运行 | 实验 |
> | 服务 | MLService |



### 创建MLInstance

可以使用以下请求创建MLInstance。 您将使用在使用API](./import-packaged-recipe-ui.md)教程从[导入打包的菜谱创建引擎时返回的`{ENGINE_ID}`。

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

`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
`{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中找到的特定API密钥值。\
`{JSON_PAYLOAD}`:MLInstance的配置。我们在教程中使用的示例如下：

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
>在`{JSON_PAYLOAD}`中，我们定义用于`tasks`数组中培训和评分的参数。 `{ENGINE_ID}`是要使用的引擎的ID,`tag`字段是用于标识实例的可选参数。

该响应将包含表示所创建MLInstance的`{INSTANCE_ID}`。 可以创建具有不同配置的多模型MLI实例。

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

数据科学家利用实验来在训练时获得高性能模型。 多个实验包括更改数据集、功能、学习参数和硬件。 以下是创建实验的示例。

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
`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中找到的特定API密钥值。\
`{JSON_PAYLOAD}`:尝试创建的对象。我们在教程中使用的示例如下：

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

`{EXPERIMENT_ID}`:表示您刚刚创建的实验的ID。`{INSTANCE_ID}`:表示MLInstance的ID。

### 为培训创建计划实验

使用计划实验，这样我们就无需通过API调用创建每个实验运行。 相反，我们在创建实验时提供所有必要的参数，并且将定期创建每个运行。

要指示创建计划实验，我们必须在请求主体中添加`template`部分。 在`template`中，计划运行的所有必要参数包括`tasks`和`schedule`，前者指示什么操作，后者指示计划运行的时间。

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
`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中找到的特定API密钥值。\
`{JSON_PAYLOAD}`:要发布的数据集。我们在教程中使用的示例如下：

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

当我们创建实验时，主体`{JSON_PAYLOAD}`应包含`mlInstanceId`或`mlInstanceQuery`参数。 在此示例中，计划实验将每20分钟调用一次运行，该运行在`cron`参数中设置，从`startTime`开始，直到`endTime`。

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


### 创建培训的实验运行

创建实验实体后，可以使用下面的调用创建并运行培训运行。 您需要`{EXPERIMENT_ID}`并在请求主体中声明要触发的`mode`。

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

`{EXPERIMENT_ID}`:与要目标的实验对应的ID。这可以在创建实验时的响应中找到。\
`{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。\
`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中找到的特定API密钥值。\
`{JSON_PAYLOAD}`:要创建培训运行，您必须在正文中包含以下内容：

```JSON
{
    "mode":"Train"
}
```

您还可以通过包括`tasks`阵列来覆盖配置参数：

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

您将收到以下响应，它将告诉您`{EXPERIMENT_RUN_ID}`和`tasks`下的配置。

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

`{EXPERIMENT_RUN_ID}`:表示“实验运行”的ID。\
`{EXPERIMENT_ID}`:表示“实验运行”所处实验的ID。

### 检索实验运行状态

可以使用`{EXPERIMENT_RUN_ID}`查询实验运行的状态。

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
`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
`{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中找到的特定API密钥值。

**响应**

GET调用将提供`state`参数中的状态，如下所示：

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

`{EXPERIMENT_RUN_ID}`:表示“实验运行”的ID。\
`{EXPERIMENT_ID}`:表示“实验运行”所处实验的ID。

除了`DONE`状态，其他状态还包括：
- `PENDING`
- `RUNNING`
- `FAILED`

要获取详细信息，可以在`tasklogs`参数下找到详细日志。

### 检索已训练的模型

为了在培训期间创建上述培训模型，我们提出以下请求：

**请求**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_RUN_ID}`:与要目标的“实验运行”对应的ID。这可以在创建实验运行时的响应中找到。\
`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
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
`{EXPERIMENT_ID}`:与实验运行对应的ID在下。\
`{EXPERIMENT_RUN_ID}`:与实验运行对应的ID。

### 停止和删除计划实验

如果要在计划实验`endTime`之前停止执行该实验，可以通过向`{EXPERIMENT_ID}`查询DELETE请求来完成此操作

**请求**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`:与实验对应的ID。\
`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
`{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。

>[!NOTE]
>
>API调用将禁用创建新的Experice运行。 但是，它不会停止执行已运行的实验运行。

以下是响应，通知已成功删除该实验。

**响应**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## 后续步骤

本教程详细介绍了如何使用API创建引擎、实验、计划实验运行和经过培训的模型。 在[下一个练习](./score-model-api.md)中，您将使用表现最好的培训模型对新数据集进行评分，从而进行预测。
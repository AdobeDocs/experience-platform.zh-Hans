---
keywords: Experience Platform;Score a model;Data Science Workspace;popular topics;sensei machine learning api
solution: Experience Platform
title: 对模型(API)进行评分
topic: Tutorial
description: 本教程将向您展示如何利用Sensei机器学习API创建实验和实验运行。
translation-type: tm+mt
source-git-commit: 7615476c4b728b451638f51cfaa8e8f3b432d659
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 1%

---


# 对模型(API)进行评分

本教程将向您展示如何利用API创建实验和实验运行。 有关API文档的详细列表，请参 [阅此文档](https://www.adobe.io/apis/cloudplatform/dataservices/api-reference.html)。

## 创建用于评分的计划实验

与培训的计划实验相似，还通过在身体参数中加入一个节来创建计划 `template` 的评分实验。 此外， `name` 主体 `tasks` 中的字段设置为 `score`。

以下是创建实验的示例，该实验从开始每20分钟运行一次， `startTime` 并一直运行到 `endTime`。

**请求**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。\
`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中找到的特定API密钥值。\
`{JSON_PAYLOAD}`:尝试要发送的运行对象。 我们在教程中使用的示例如下：

```JSON
{
    "name": "Experiment for Retail",
    "mlInstanceId": "{INSTANCE_ID}",
    "template": {
        "tasks": [{
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
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
            "startTime": "2018-07-04",
            "endTime": "2018-07-06"
        }
    }
}
```

`{INSTANCE_ID}`:表示MLInstance的ID。\
`{MODEL_ID}`:表示已培训模型的ID。

以下是创建计划实验后的响应。

**响应**

```JSON
{
  "id": "{EXPERIMENT_ID}",
  "name": "Experiment for Retail",
  "mlInstanceId": "{INSTANCE_ID}",
  "created": "2018-11-11T11:11:11.111Z",
  "updated": "2018-11-11T11:11:11.111Z",
  "template": {
    "tasks": [
      {
        "name": "score",
        "parameters": [...],
        "specification": {
          "type": "SparkTaskSpec",
          "executorCores": 5,
          "numExecutors": 5
        }
      }
    ],
    "schedule": {
      "cron": "*\/20 * * * *",
      "startTime": "2018-07-04",
      "endTime": "2018-07-06"
    }
  }
}
```

`{EXPERIMENT_ID}`:表示实验的ID。\
`{INSTANCE_ID}`:表示MLInstance的ID。


### 创建评分的实验运行

现在，利用经过培训的模型，我们可以创建一个用于评分的实验运行。 参数的值是 `modelId` 上述GET `id` 模型请求中返回的参数。

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

`{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。\
`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中找到的特定API密钥值。\
`{EXPERIMENT_ID}`:与要目标的实验对应的ID。 这可以在创建实验时的响应中找到。\
`{JSON_PAYLOAD}`:要发布的数据。 我们在教程中使用的示例如下：

```JSON
{
   "mode":"score",
    "tasks": [
        {
            "name": "score",
            "parameters": [
                {
                    "key": "modelId",
                    "value": "{MODEL_ID}"
                }
            ]
        }
    ]
}
```

`{MODEL_ID}`:与“模型”(Model)对应的ID。

创建“实验运行”时的响应如下所示：

**响应**

```JSON
{
    "id": "{EXPERIMENT_RUN_ID}",
    "mode": "score",
    "experimentId": "{EXPERIMENT_ID}",
    "created": "2018-01-01T11:11:11.011Z",
    "updated": "2018-01-01T11:11:11.011Z",
    "deleted": false,
    "tasks": [
        {
            "name": "score",
            "parameters": [...]
        }
    ]
}
```

`{EXPERIMENT_ID}`: 与“运行”(Run)下的“实验”(Experice)对应的ID。\
`{EXPERIMENT_RUN_ID}`:与您刚刚创建的“Experience Run”对应的ID。


### 检索计划实验运行的实验运行状态

要获取计划实验的实验运行，查询如下所示：

**请求**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`: 与“运行”(Run)下的“实验”(Experice)对应的ID。\
`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
`{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。

由于特定实验有多个实验运行，因此返回的响应将具有一组运行ID。

**响应**

```JSON
{
    "children": [
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        },
        {
            "id": "{EXPERIMENT_RUN_ID}",
            "experimentId": "{EXPERIMENT_ID}",
            "created": "2018-01-01T11:11:11.011Z",
            "updated": "2018-01-01T11:11:11.011Z"
        }
    ]
}
```

`{EXPERIMENT_RUN_ID}`:与实验运行对应的ID。\
`{EXPERIMENT_ID}`: 与“运行”(Run)下的“实验”(Experice)对应的ID。

### 停止和删除计划实验

如果要在计划实验之前停止执行该 `endTime`实验，可以通过向 `{EXPERIMENT_ID}`

**请求**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`: 与实验对应的ID。\
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

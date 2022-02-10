---
keywords: Experience Platform；对模型进行评分；Data Science Workspace；热门主题；敏感的机器学习api
solution: Experience Platform
title: 使用Sensei机器学习API对模型进行评分
topic-legacy: tutorial
type: Tutorial
description: 本教程将向您展示如何利用Sensei机器学习API创建实验和实验运行。
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: 6ae6bbb5af0f007e483145dca5d4d505c388cc2c
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# 使用 [!DNL Sensei Machine Learning API]

本教程将向您展示如何利用API创建实验和实验运行。 有关Sensei机器学习API中所有端点的列表，请参阅 [本文档](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## 为评分创建计划实验

与培训的计划实验类似，还通过包含 `template` 部分。 此外， `name` 字段 `tasks` 在主体中设置为 `score`.

以下是创建一个实验的示例，该实验将从 `startTime` 将运行到 `endTime`.

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
`{JSON_PAYLOAD}`:要发送的Experience Run对象。 下面显示了我们在教程中使用的示例：

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


### 为评分创建实验运行

现在，利用训练好的模型，我们可以创建一个“实验运行”来打分。 的值 `modelId` 参数是 `id` 在上述GET模型请求中返回的参数。

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
`{EXPERIMENT_ID}`:与要定位的实验对应的ID。 这可在创建实验时的响应中找到。\
`{JSON_PAYLOAD}`:要发布的数据。 以下是我们在教程中使用的示例：

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

`{MODEL_ID}`:与模型对应的ID。

“实验运行”创建的响应如下所示：

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

`{EXPERIMENT_ID}`:与运行所在实验对应的ID。\
`{EXPERIMENT_RUN_ID}`:与您刚刚创建的“实验运行”对应的ID。


### 为计划的实验运行检索实验运行状态

要为计划实验运行体验，查询如下所示：

**请求**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`:与运行所在实验对应的ID。\
`{ACCESS_TOKEN}`:身份验证后提供的特定载体令牌值。\
`{IMS_ORG}`:您的IMS组织凭据可在独特的Adobe Experience Platform集成中找到。

由于特定实验存在多个实验运行，因此返回的响应将具有一组运行ID。

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

`{EXPERIMENT_RUN_ID}`:与“实验运行”对应的ID。\
`{EXPERIMENT_ID}`:与运行所在实验对应的ID。

### 停止和删除计划的实验

如果要在计划实验之前停止执行该实验 `endTime`，可通过查询向 `{EXPERIMENT_ID}`

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

---
keywords: Experience Platform;Score a model;Data Science Workspace;popular topics
solution: Experience Platform
title: 对模型进行评分(API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 对模型进行评分(API)

本教程将向您展示如何利用API创建实验和实验运行。 有关API文档的详细列表，请参阅 [本文档](https://www.adobe.io/apis/cloudplatform/dataservices/api-reference.html)。

## 创建计划的评分实验

与培训的计划实验相似，还可以通过在身体参数中加入一个部分来创建计划 `template` 的评分实验。 此外， `name` 主体中 `tasks` 的字段设置为 `score`。

以下是创建实验的示例，该实验从开始开始每20分钟运行一次， `startTime` 运行到结束 `endTime`。

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
`{ACCESS_TOKEN}`:身份验证后提供的特定承载令牌值。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中可找到特定API密钥价值。\
`{JSON_PAYLOAD}`:实验要发送的运行对象。 我们在教程中使用的示例如下：

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
`{MODEL_ID}`:表示经过培训的模型的ID。

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


### 创建用于评分的实验运行

现在，利用经过培训的模型，我们可以创建一个用于评分的实验运行。 参数的值是 `modelId` 上述GET Model请 `id` 求中返回的参数。

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
`{ACCESS_TOKEN}`:身份验证后提供的特定承载令牌值。\
`{API_KEY}`:您在独特的Adobe Experience Platform集成中可找到特定API密钥价值。\
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

创建“实验运行”的响应如下所示：

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

`{EXPERIMENT_ID}`: 与“运行”下的“实验”对应的ID。\
`{EXPERIMENT_RUN_ID}`:与您刚刚创建的Experice Run对应的ID。


### 检索计划实验运行的“实验运行”状态

要获取计划实验的实验运行，查询如下：

**请求**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

`{EXPERIMENT_ID}`: 与“运行”下的“实验”对应的ID。\
`{ACCESS_TOKEN}`:身份验证后提供的特定承载令牌值。\
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

`{EXPERIMENT_RUN_ID}`:与“实验运行”对应的ID。\
`{EXPERIMENT_ID}`: 与“运行”下的“实验”对应的ID。

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

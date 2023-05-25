---
keywords: Experience Platform；为模型评分；Data Science Workspace；热门主题；sensei机器学习api
solution: Experience Platform
title: 使用Sensei机器学习API为模型评分
type: Tutorial
description: 本教程将演示如何利用Sensei机器学习API创建实验并运行实验。
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 1%

---

# 使用为模型评分 [!DNL Sensei Machine Learning API]

本教程将向您展示如何利用API创建试验和执行试验。 有关Sensei机器学习API中所有端点的列表，请参阅 [本文档](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/).

## 创建计划的试验以进行评分

与计划的训练实验类似，为评分创建计划的实验也是通过包含 `template` 部分到body参数。 此外， `name` 字段在 `tasks` 在正文中，设置为 `score`.

以下示例介绍了如何创建一个试验，该试验将从开始每隔20分钟运行一次。 `startTime` 并且将运行到 `endTime`.

**请求**

```Shell
curl -X POST \
  https://platform.adobe.io/data/sensei/experiments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}' \
  -d '{JSON_PAYLOAD}'
```

`{ORG_ID}`：在独特的Adobe Experience Platform集成中找到您的组织凭据。\
`{ACCESS_TOKEN}`：在身份验证后提供的特定持有者令牌值。\
`{API_KEY}`：在独特的Adobe Experience Platform集成中找到的特定API密钥值。\
`{JSON_PAYLOAD}`：要发送的Experiment Run对象。 此处显示了我们在教程中使用的示例：

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

`{INSTANCE_ID}`：表示MLInstance的ID。\
`{MODEL_ID}`：表示经过训练的模型的ID。

以下是创建计划试验后的响应。

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

`{EXPERIMENT_ID}`：表示试验的ID。\
`{INSTANCE_ID}`：表示MLInstance的ID。


### 创建试验运行以进行评分

现在，使用经过训练的模型，我们可以创建一个用于评分的试验运行。 的值 `modelId` 参数为 `id` 参数会返回至上述GET模型请求中。

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

`{ORG_ID}`：在独特的Adobe Experience Platform集成中找到您的组织凭据。\
`{ACCESS_TOKEN}`：在身份验证后提供的特定持有者令牌值。\
`{API_KEY}`：在独特的Adobe Experience Platform集成中找到的特定API密钥值。\
`{EXPERIMENT_ID}`：与要定位的试验相对应的ID。 这可以在创建试验时的响应中找到。\
`{JSON_PAYLOAD}`：要发布的数据。 我们在本教程中使用的示例如下所示：

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

`{MODEL_ID}`：对应于模型的ID。

试验运行创建的响应如下所示：

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

`{EXPERIMENT_ID}`：与运行所依据的试验相对应的ID。\
`{EXPERIMENT_RUN_ID}`：与刚刚创建的试验运行相对应的ID。


### 检索计划试验运行的试验运行状态

要获取计划试验的试验运行，查询如下所示：

**请求**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`：与运行所依据的试验相对应的ID。\
`{ACCESS_TOKEN}`：在身份验证后提供的特定持有者令牌值。\
`{ORG_ID}`：在独特的Adobe Experience Platform集成中找到您的组织凭据。

由于特定试验存在多个试验运行，因此返回的响应将具有运行ID数组。

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

`{EXPERIMENT_RUN_ID}`：与试验运行对应的ID。\
`{EXPERIMENT_ID}`：与运行所依据的试验相对应的ID。

### 停止并删除计划的试验

如果您想在计划试验之前停止执行该试验 `endTime`，这可以通过向查询DELETE请求来完成 `{EXPERIMENT_ID}`

**请求**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`：对应于试验的ID。\
`{ACCESS_TOKEN}`：在身份验证后提供的特定持有者令牌值。\
`{ORG_ID}`：在独特的Adobe Experience Platform集成中找到您的组织凭据。

>[!NOTE]
>
>API调用将禁用创建新的试验运行。 但是，它不会停止执行已运行的试验运行。

以下是响应，通知已成功删除试验。

**响应**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

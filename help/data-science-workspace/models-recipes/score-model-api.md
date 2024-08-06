---
keywords: 体验平台;为模型评分;数据科学工作区;热门话题;Sensei 机器学习 API
solution: Experience Platform
title: 使用 Sensei 机器学习 API 对模型进行评分
type: Tutorial
description: 本教程将介绍如何利用 Sensei 机器学习 API 来创建实验和实验运行。
exl-id: 202c63b0-86d8-4a82-8ec8-d144a8911d08
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# 使用 [!DNL Sensei Machine Learning API]

>[!NOTE]
>
>不再可供购买数据科学工作区。
>
>本文档适用于先前有权访问数据科学工作区的现有客户。

本教程将介绍如何利用 API 创建试验和试验运行。 有关 Sensei 机器学习 API 中所有端点的列表，请参阅 [此文档](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/)。

## 创建用于评分的计划实验

与用于训练的计划实验类似，创建用于评分的计划实验也是通过在 body 参数中包含部分 `template` 来完成的。 此外，正文中`tasks`下的`name`字段设置为`score`。

以下示例用于创建从`startTime`开始每隔20分钟运行一次并一直运行到`endTime`的试验。

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
`{API_KEY}`：您的特定 API 密钥值，可在唯一的 Adobe Experience Platform 集成中找到。\
`{JSON_PAYLOAD}`：要发送的试验运行对象。 我们在本教程中使用的示例如下所示：

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
`{MODEL_ID}`：表示已训练模型的ID。

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

`{EXPERIMENT_ID}`：表示实验的 ID。\
`{INSTANCE_ID}`：表示 MLInstance 的 ID。


### 创建用于评分的试验运行

现在，使用经过训练的模型，我们可以创建用于评分的实验运行。 参数的值 `modelId` 是上述 GET 模型请求中返回的 `id` 参数。

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

`{ORG_ID}`：您的组织凭据可在唯一的 Adobe Experience Platform 集成中找到。\
`{ACCESS_TOKEN}`：身份验证后提供的特定持有者令牌值。\
`{API_KEY}`：您的特定 API 密钥值，可在唯一的 Adobe Experience Platform 集成中找到。\
`{EXPERIMENT_ID}`：与要定位的实验对应的 ID。 这可以在创建实验时的响应中找到。\
`{JSON_PAYLOAD}`：要发布的数据。 我们在本教程中使用的示例如下：

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

`{MODEL_ID}`：与模型对应的ID。

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
`{EXPERIMENT_RUN_ID}`：与刚刚创建的试验运行对应的 ID。


### 为计划的试验运行检索试验运行状态

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
`{ORG_ID}`：您的组织凭据可在唯一的 Adobe Experience Platform 集成中找到。

由于特定试验有多个试验运行，因此返回的响应将具有运行 ID 数组。

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

`{EXPERIMENT_RUN_ID}`：与实验运行对应的 ID。\
`{EXPERIMENT_ID}`：与运行所在的实验对应的 ID。

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

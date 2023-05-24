---
keywords: Experience Platform；訓練與評估；資料科學工作區；熱門主題；Sensei機器學習API
solution: Experience Platform
title: 使用Sensei Machine Learning API訓練和評估模型
type: Tutorial
description: 本教學課程將說明如何使用Sensei機器學習API呼叫來建立、訓練和評估模型。
exl-id: 8107221f-184c-426c-a33e-0ef55ed7796e
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 1%

---

# 使用訓練及評估模型 [!DNL Sensei Machine Learning] API


本教學課程將說明如何使用API呼叫建立、訓練和評估模型。 請參閱 [本檔案](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) 以取得API檔案的詳細清單。

## 先决条件

請遵循 [使用API匯入封裝的配方](./import-packaged-recipe-api.md) 建立引擎時，需要使用API來訓練和評估模型。

請遵循 [Experience PlatformAPI驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以開始進行API呼叫。

在教學課程中，您現在應該具備下列值：

- `{ACCESS_TOKEN}`：驗證後提供的特定持有人權杖值。
- `{ORG_ID}`：您在唯一Adobe Experience Platform整合中找到的組織憑證。
- `{API_KEY}`：您在唯一Adobe Experience Platform整合中找到的特定API金鑰值。

- 智慧型服務的Docker影像連結

## API工作流程

我們將使用API來建立用於訓練的Experiment Run。 在本教學課程中，我們將著重於引擎、MLInstances和Experiments端點。 下表概述三者之間的關係，並介紹「執行」和「模型」的概念。

![](../images/models-recipes/train-evaluate-api/engine_hierarchy_api.png)

>[!NOTE]
>
>術語「引擎」、「MLInstance」、「MLService」、「Experiment」和「Model」在UI中稱為不同的術語。 如果您是來自UI，下表會比較兩者的差異。

| UI詞語 | API詞語 |
| --- | --- |
| 指導方針 | 引擎 |
| 模型 | MLInstance |
| 訓練回合 | 试验 |
| 服务 | MLService |

### 建立MLInstance

建立MLInstance可使用以下請求完成。 您將使用 `{ENGINE_ID}` 從建立引擎時傳回的專案 [使用API匯入封裝的配方](./import-packaged-recipe-ui.md) 教學課程。

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

`{ACCESS_TOKEN}`：驗證後提供的特定持有人權杖值。\
`{ORG_ID}`：您在唯一Adobe Experience Platform整合中找到的組織憑證。\
`{API_KEY}`：您在唯一Adobe Experience Platform整合中找到的特定API金鑰值。\
`{JSON_PAYLOAD}`：MLInstance的設定。 我們會在教學課程中使用的範例顯示在這裡：

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
>在 `{JSON_PAYLOAD}`，我們會定義用來在中訓練和評分的引數 `tasks` 陣列。 此 `{ENGINE_ID}` 是要使用的引擎ID，以及 `tag` 欄位是用於識別執行個體的選用引數。

回應包含 `{INSTANCE_ID}` 代表建立的MLInstance。 可以建立具有不同設定的多個模型MLInstances。

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

`{ENGINE_ID}`：此ID代表建立MLInstance的引擎。\
`{INSTANCE_ID}`：代表MLInstance的ID。

### 建立實驗

資料科學家在訓練時會使用實驗來達成高績效模型。 多項實驗包括變更資料集、功能、學習引數和硬體。 以下是建立「實驗」的範例。

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

`{ORG_ID}`：您在唯一Adobe Experience Platform整合中找到的組織憑證。\
`{ACCESS_TOKEN}`：驗證後提供的特定持有人權杖值。\
`{API_KEY}`：您在唯一Adobe Experience Platform整合中找到的特定API金鑰值。\
`{JSON_PAYLOAD}`：建立的實驗物件。 我們會在教學課程中使用的範例顯示在這裡：

```JSON
{
    "name": "Experiment for Retail ",
    "mlInstanceId": "{INSTANCE_ID}",
    "tags": {
        "test": "guide"
    }
}
```

`{INSTANCE_ID}`：代表MLInstance的ID。

實驗建立的回應如下所示。

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

`{EXPERIMENT_ID}`：代表您剛剛建立的Experiment的ID。
`{INSTANCE_ID}`：代表MLInstance的ID。

### 建立排程的實驗以進行訓練

已排程實驗使用，因此我們不需要透過API呼叫建立每個實驗執行。 相反地，我們在實驗建立期間會提供所有必要的引數，而且每次執行都會定期建立。

若要指示已排程實驗的建立，我們必須新增 `template` 區段。 在 `template`，則包含排程執行所需的所有引數，例如 `tasks`，表示哪個動作，以及 `schedule`，代表排程執行的時間。

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

`{ORG_ID}`：您在唯一Adobe Experience Platform整合中找到的組織憑證。\
`{ACCESS_TOKEN}`：驗證後提供的特定持有人權杖值。\
`{API_KEY}`：您在唯一Adobe Experience Platform整合中找到的特定API金鑰值。\
`{JSON_PAYLOAD}`：要發佈的資料集。 我們會在教學課程中使用的範例顯示在這裡：

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

當我們建立實驗時，主體 `{JSON_PAYLOAD}`，應包含 `mlInstanceId` 或 `mlInstanceQuery` 引數。 在此範例中，排程的實驗將叫用每20分鐘執行一次，在 `cron` 引數，從 `startTime` 直到 `endTime`.

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

`{EXPERIMENT_ID}`：代表實驗的ID。\
`{INSTANCE_ID}`：代表MLInstance的ID。


### 建立實驗回合以進行訓練

建立實驗實體後，可以使用以下呼叫建立和執行訓練回合。 您將需要 `{EXPERIMENT_ID}` 並說明內容 `mode` 您想要在要求內文中觸發。

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

`{EXPERIMENT_ID}`：與您要鎖定之實驗相對應的ID。 這可在建立實驗時的回應中找到。\
`{ORG_ID}`：您在唯一Adobe Experience Platform整合中找到的組織憑證。\
`{ACCESS_TOKEN}`：驗證後提供的特定持有人權杖值。\
`{API_KEY}`：您在唯一Adobe Experience Platform整合中找到的特定API金鑰值。\
`{JSON_PAYLOAD}`：若要建立訓練回合，您必須在內文中包含以下內容：

```JSON
{
    "mode":"Train"
}
```

您也可以包含以覆寫配置引數 `tasks` 陣列：

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

您會收到下列回應，通知您 `{EXPERIMENT_RUN_ID}` 以及下的設定 `tasks`.

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

`{EXPERIMENT_RUN_ID}`：代表實驗回合的ID。\
`{EXPERIMENT_ID}`：代表「實驗執行」所在實驗的ID。

### 擷取實驗執行狀態

實驗回合的狀態可透過查詢 `{EXPERIMENT_RUN_ID}`.

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}/runs/{EXPERIMENT_RUN_ID}/status \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-api-key: {API_KEY}'
```

`{EXPERIMENT_ID}`：代表實驗的ID。\
`{EXPERIMENT_RUN_ID}`：代表實驗回合的ID。\
`{ACCESS_TOKEN}`：驗證後提供的特定持有人權杖值。\
`{ORG_ID}`：您在唯一Adobe Experience Platform整合中找到的組織憑證。\
`{API_KEY}`：您在唯一Adobe Experience Platform整合中找到的特定API金鑰值。

**响应**

GET呼叫將會在 `state` 引數，如下所示：

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

`{EXPERIMENT_RUN_ID}`：代表實驗回合的ID。\
`{EXPERIMENT_ID}`：代表「實驗執行」所在實驗的ID。

除了 `DONE` 州別，其他州別包括：
- `PENDING`
- `RUNNING`
- `FAILED`

若要取得詳細資訊，您可以在下列位置找到詳細記錄： `tasklogs` 引數。

### 擷取經過訓練的模型

為了取得上述在訓練期間建立的訓練模型，我們提出以下要求：

**请求**

```Shell
curl -X GET \
  'https://platform.adobe.io/data/sensei/models/?property=experimentRunId=={EXPERIMENT_RUN_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_RUN_ID}`：與您要鎖定的實驗回合相對應的ID。 這可在建立實驗回合時的回應中找到。\
`{ACCESS_TOKEN}`：驗證後提供的特定持有人權杖值。\
`{ORG_ID}`：您在唯一Adobe Experience Platform整合中找到的組織憑證。

回應代表已建立的已訓練模型。

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

`{MODEL_ID}`：與模型相對應的ID。\
`{EXPERIMENT_ID}`：對應至實驗執行所在實驗的ID。\
`{EXPERIMENT_RUN_ID}`：與實驗回合相對應的ID。

### 停止並刪除排程的實驗

如果您想要在排程實驗之前停止執行 `endTime`，這可透過向查詢DELETE請求來完成 `{EXPERIMENT_ID}`

**请求**

```Shell
curl -X DELETE \
  'https://platform.adobe.io/data/sensei/experiments/{EXPERIMENT_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

`{EXPERIMENT_ID}`：與實驗相對應的ID。\
`{ACCESS_TOKEN}`：驗證後提供的特定持有人權杖值。\
`{ORG_ID}`：您在唯一Adobe Experience Platform整合中找到的組織憑證。

>[!NOTE]
>
>API呼叫將停用建立新的實驗執行。 但是，它不會停止執行已執行的實驗回合。

以下是「回應」，通知實驗已成功刪除。

**响应**

```JSON
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## 后续步骤

本教學課程說明如何使用API來建立引擎、實驗、已排程的實驗執行和訓練的模型。 在 [下一個練習](./score-model-api.md)，您將會透過使用表現最佳的訓練模型來評分新資料集來進行預測。

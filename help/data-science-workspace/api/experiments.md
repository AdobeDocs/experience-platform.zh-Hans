---
keywords: Experience Platform；開發人員指南；端點；Data Science Workspace；熱門主題；實驗；sensei機器學習api
solution: Experience Platform
title: 實驗API端點
description: 模型開發和訓練會在實驗層級進行，其中實驗包括MLInstance、訓練回合和評分回合。
exl-id: 6ca5106e-896d-4c03-aecc-344632d5307d
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 4%

---

# 實驗端點

模型開發和訓練會在實驗層級進行，其中實驗包括MLInstance、訓練回合和評分回合。

## 建立實驗 {#create-an-experiment}

您可以在要求裝載中提供名稱和有效的MLInstance ID時，透過執行POST要求來建立實驗。

>[!NOTE]
>
>與UI中的模型訓練不同，透過明確API呼叫建立實驗不會自動建立和執行訓練回合。

**API格式**

```http
POST /experiments
```

**请求**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiment.v1.json' \
    -d '{
        "name": "a name for this Experiment",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda"
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 實驗所需的名稱。 與此實驗對應的訓練回合將繼承此值，以作為訓練回合名稱顯示在UI中。 |
| `mlInstanceId` | 有效的MLInstance ID。 |

**响应**

成功回應會傳回包含新建立實驗詳細資訊的裝載，包括其唯一識別碼(`id`)。

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## 建立並執行訓練或評分回合 {#experiment-training-scoring}

您可以透過執行POST請求並提供有效的實驗ID和指定執行任務來建立訓練或評分回合。 只有在實驗具有現有且成功的訓練回合時，才能建立評分回合。 成功建立訓練回合將初始化模型訓練程式，其成功完成將生成訓練好的模型。 產生經過訓練的模型將取代任何先前存在的模型，因此實驗在任何給定時間都只能利用單一經過訓練的模型。

**API格式**

```http
POST /experiments/{EXPERIMENT_ID}/runs
```

| 参数 | 描述 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的實驗ID。 |

**请求**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experimentRun.v1.json' \
    -d '{
        "mode": "{TASK}"
    }'
```

| 属性 | 描述 |
| --- | --- |
| `{TASK}` | 指定執行的工作。 將此值設定為 `train` 訓練方面， `score` 評分，或 `featurePipeline` 用於功能管道。 |

**响应**

成功回應會傳回包含新建立回合詳細資訊的裝載，包括繼承的預設訓練或評分引數，以及回合的唯一ID (`{RUN_ID}`)。

```json
{
    "id": "33408593-2871-4198-a812-6d1b7d939cda",
    "mode": "{TASK}",
    "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdBySchedule": false,
    "tasks": [
        {
            "name": "{TASK}",
            "parameters": [
                {
                    "key": "parameter",
                    "value": "parameter value"
                }
            ]
        }
    ]
}
```

## 擷取實驗清單

您可以執行單一GET要求，並提供有效的MLInstance ID作為查詢引數，以擷取屬於特定MLInstance的實驗清單。 如需可用查詢的清單，請參閱附錄 [用於資產擷取的查詢引數](./appendix.md#query).


**API格式**

```http
GET /experiments
GET /experiments?property=mlInstanceId=={MLINSTANCE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MLINSTANCE_ID}` | 提供有效的MLInstance ID以擷取屬於該特定MLInstance的實驗清單。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功回應會傳回共用相同MLInstance ID (`{MLINSTANCE_ID}`)。

```json
{
    "children": [
        {
            "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "A name for this Experiment",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "6cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 1",
            "mlInstanceId": "46986c8f-7839-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        },
        {
            "id": "7cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "name": "Training Run 2",
            "mlInstanceId": "46986c8f-7939-4376-8509-0178bdf32cda",
            "created": "2019-01-01T00:00:00.000Z",
            "updated": "2019-01-01T00:00:00.000Z",
            "createdByService": false
        }
    ],
    "_page": {
        "property": "deleted==false",
        "count": 3
    }
}
```

## 擷取特定實驗 {#retrieve-specific}

您可以透過執行GET請求，在請求路徑中包含所需的實驗ID，來擷取特定實驗的詳細資訊。

**API格式**

```http
GET /experiments/{EXPERIMENT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的實驗ID。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回包含所請求實驗詳細資訊的裝載。

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "createdByService": false
}
```

## 擷取實驗回合清單

您可以執行單一GET要求並提供有效的實驗ID，以擷取屬於特定實驗的訓練或評分回合清單。 若要協助篩選結果，您可以在請求路徑中指定查詢引數。 如需可用查詢引數的完整清單，請參閱 [用於資產擷取的查詢引數](./appendix.md#query).

>[!NOTE]
>
>合併多個查詢引數時，必須以&amp;符號分隔。

**API格式**

```http
GET /experiments/{EXPERIMENT_ID}/runs
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER}={VALUE}
GET /experiments/{EXPERIMENT_ID}/runs?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 参数 | 描述 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的實驗ID。 |
| `{QUERY_PARAMETER}` | 其中一項 [可用的查詢引數](./appendix.md#query) 用於篩選結果。 |
| `{VALUE}` | 上一個查詢引數的值。 |

**请求**

以下請求包含一個查詢，並擷取屬於某些實驗的訓練回合清單。

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b/runs?property=mode==train \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回一個裝載，其中包含執行清單及其每個詳細資訊，包括其實驗執行ID (`{RUN_ID}`)。

```json
{
    "children": [
        {
            "id": "33408593-2871-4198-a812-6d1b7d939cda",
            "mode": "train",
            "experimentId": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "createdBySchedule": false
        }
    ],
    "_page": {
        "property": "mode==train,experimentId==5cb25a2d-2cbd-4c99-a619-8ddae5250a7b,deleted==false",
        "totalCount": 1,
        "count": 1
    }
}
```

## 更新實驗

您可以透過PUT請求（請求路徑中包含目標實驗ID）來覆寫現有實驗的屬性，並提供包含已更新屬性的JSON裝載，藉此更新現有實驗。

>[!TIP]
>
>為確保此PUT請求成功，建議您先執行GET請求 [依ID擷取實驗](#retrieve-specific). 接著，修改並更新傳回的JSON物件，並將整個修改過的JSON物件套用為PUT請求的裝載。

以下範例API呼叫最初具有這些屬性時會更新實驗的名稱：

```json
{
    "name": "A name for this Experiment",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "createdByService": false
}
```

**API格式**

```http
PUT /experiments/{EXPERIMENT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的實驗ID。 |

**请求**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=experiments.v1.json' \
    -d '{
        "name": "An upated name",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "created": "2019-01-01T00:00:00.000Z",
        "createdBy": {
            "userId": "Jane_Doe@AdobeID"
        },
        "createdByService": false
    }'
```

**响应**

成功的回應會傳回包含實驗更新詳細資訊的裝載。

```json
{
    "id": "5cb25a2d-2cbd-4c99-a619-8ddae5250a7b",
    "name": "An updated name",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "createdByService": false
}
```

## 刪除實驗

您可以透過執行DELETE請求（請求路徑中包含目標實驗ID）來刪除單一實驗。

**API格式**

```http
DELETE /experiments/{EXPERIMENT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{EXPERIMENT_ID}` | 有效的實驗ID。 |

**请求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments/5cb25a2d-2cbd-4c99-a619-8ddae5250a7b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Experiment successfully deleted"
}
```

## 依MLInstance ID刪除實驗

您可以執行包含MLInstance ID作為查詢引數的DELETE要求，以刪除屬於特定MLInstance的所有實驗。

**API格式**

```http
DELETE /experiments?mlInstanceId={MLINSTANCE_ID}
```

| 参数 | 描述 |
| --- | ---|
| `{MLINSTANCE_ID}` | 有效的MLInstance ID。 |

**请求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/experiments?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Experiments successfully deleted"
}
```

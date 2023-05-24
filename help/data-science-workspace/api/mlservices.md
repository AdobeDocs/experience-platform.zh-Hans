---
keywords: Experience Platform；開發人員指南；端點；Data Science Workspace；熱門主題；mlservices；sensei機器學習api
solution: Experience Platform
title: MLServices API端點
description: MLService是已發佈的經訓練模型，讓您的組織能夠存取及重複使用先前開發的模型。 MLServices的主要功能是能依排程自動執行訓練和評分。 排程的訓練回合有助於維持模型的效率和正確性，而排程的評分回合則可確保一致地產生新的見解。
exl-id: cd236e0b-3bfc-4d37-83eb-432f6ad5c5b6
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---

# MLServices端點

MLService是已發佈的經訓練模型，讓您的組織能夠存取及重複使用先前開發的模型。 MLServices的主要功能是能依排程自動執行訓練和評分。 排程的訓練回合有助於維持模型的效率和正確性，而排程的評分回合則可確保一致地產生新的見解。

自動訓練和評分排程的定義包含開始時間戳記、結束時間戳記和以表示的頻率 [cron運算式](https://en.wikipedia.org/wiki/Cron). 排程可在以下情況下定義： [建立MLService](#create-an-mlservice) 或套用者 [更新現有的MLService](#update-an-mlservice).

## 建立MLService {#create-an-mlservice}

您可以執行POST要求以及提供服務名稱和有效MLInstance ID的裝載，以建立MLService。 用來建立MLService的MLInstance不需要有現有的訓練實驗，但您可以藉由提供對應的實驗ID和訓練回合ID，選擇使用現有的訓練模型建立MLService。

**API格式**

```http
POST /mlServices
```

**请求**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/mlServices \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingExperimentRunId": "33408593-2871-4198-a812-6d1b7d939cda",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 所需的MLService名稱。 與此MLService對應的服務將繼承此值，以作為服務名稱顯示在「服務庫」UI中。 |
| `description` | MLService的選擇性說明。 與此MLService對應的服務將繼承此值，以作為服務的說明顯示在「服務庫」UI中。 |
| `mlInstanceId` | 有效的MLInstance ID。 |
| `trainingDataSetId` | 如果提供，訓練資料集ID將覆寫MLInstance的預設資料集ID。 如果用來建立MLService的MLInstance未定義訓練資料集，您必須提供適當的訓練資料集ID。 |
| `trainingExperimentId` | 您可以選擇提供的實驗ID。 如果未提供此值，則建立MLService也將使用MLInstance的預設設定來建立新的實驗。 |
| `trainingExperimentRunId` | 您可以選擇提供的訓練回合ID。 如果未提供此值，則建立MLService也會使用MLInstance的預設訓練引數來建立和執行訓練回合。 |
| `trainingSchedule` | 自動化訓練回合排程。 如果定義了此屬性，則MLService將會依排程自動執行訓練回合。 |
| `trainingSchedule.startTime` | 排程的訓練回合將開始的時間戳記。 |
| `trainingSchedule.endTime` | 排程的訓練回合將結束的時間戳記。 |
| `trainingSchedule.cron` | 定義自動訓練執行頻率的cron運算式。 |
| `scoringSchedule` | 自動評分回合的排程。 如果已定義此屬性，則MLService將會依排程自動執行評分回合。 |
| `scoringSchedule.startTime` | 排定的評分回合將開始的時間戳記。 |
| `scoringSchedule.endTime` | 排定的評分回合將結束的時間戳記。 |
| `scoringSchedule.cron` | 定義自動評分執行頻率的cron運算式。 |

**响应**

成功回應會傳回包含新建立MLService詳細資訊的裝載，包括其唯一識別碼(`id`)，用於訓練的實驗ID (`trainingExperimentId`)，評分的實驗ID (`scoringExperimentId`)，以及輸入訓練資料集ID (`trainingDataSetId`)。

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## 擷取MLServices清單 {#retrieve-a-list-of-mlservices}

您可以透過執行單一GET要求來擷取MLServices清單。 若要協助篩選結果，您可以在請求路徑中指定查詢引數。 如需可用查詢的清單，請參閱附錄 [用於資產擷取的查詢引數](./appendix.md#query).

**API格式**

```http
GET /mlServices
GET /mlServices?{QUERY_PARAMETER}={VALUE}
GET /mlServices?{QUERY_PARAMETER_1}={VALUE_1}&{QUERY_PARAMETER_2}={VALUE_2}
```

| 参数 | 描述 |
| --- | --- |
| `{QUERY_PARAMETER}` | 其中一項 [可用的查詢引數](./appendix.md#query) 用於篩選結果。 |
| `{VALUE}` | 上一個查詢引數的值。 |

**请求**

以下請求包含一個查詢，並擷取共用相同MLInstance ID (`{MLINSTANCE_ID}`)。

```shell
curl -X GET \
    'https://platform.adobe.io/data/sensei/mlServices?property=mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回MLServices清單及其詳細資料，包括其MLService ID (`{MLSERVICE_ID}`)，用於訓練的實驗ID (`{TRAINING_ID}`)，評分的實驗ID (`{SCORING_ID}`)，以及輸入訓練資料集ID (`{DATASET_ID}`)。

```json
{
    "children": [
        {
            "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
            "name": "A service created in UI",
            "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
            "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
            "trainingDataSetId": "5ee3cd7f2d34011913c56941",
            "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "displayName": "Jane Doe",
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "mlInstanceId==46986c8f-7739-4376-8509-0178bdf32cda,deleted==false",
        "count": 1
    }
}
```

## 擷取特定MLService {#retrieve-a-specific-mlservice}

您可以透過執行GET請求，在請求路徑中包含所需的MLService ID，來擷取特定實驗的詳細資訊。

**API格式**

```http
GET /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`：有效的MLService ID。

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回包含所請求MLService詳細資訊的裝載。

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z"
}
```

## 更新MLService {#update-an-mlservice}

您可以透過PUT請求（請求路徑中包含目標MLService的ID）來覆寫其屬性，並提供包含已更新屬性的JSON裝載，以更新現有的MLService。

>[!TIP]
>
>為確保此PUT請求成功，建議您先執行GET請求 [依ID擷取MLService](#retrieve-a-specific-mlservice). 接著，修改並更新傳回的JSON物件，並將整個修改過的JSON物件套用為PUT請求的裝載。

**API格式**

```http
PUT /mlServices/{MLSERVICE_ID}
```

* `{MLSERVICE_ID}`：有效的MLService ID。

**请求**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json; profile=mlService.v1.json' \
    -d '{
        "name": "A name for this MLService",
        "description": "A description for this MLService",
        "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
        "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
        "trainingDataSetId": "5ee3cd7f2d34011913c56941",
        "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
        "trainingSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        },
        "scoringSchedule": {
            "startTime": "2019-01-01T00:00",
            "endTime": "2019-12-31T00:00",
            "cron": "20 * * * *"
        }
    }'
```

**响应**

成功的回應會傳回包含MLService更新詳細資訊的裝載。

```json
{
    "id": "68d936d8-17e6-44ef-a4b6-c7502055638b",
    "name": "A name for this MLService",
    "description": "A description for this MLService",
    "mlInstanceId": "46986c8f-7739-4376-8509-0178bdf32cda",
    "trainingExperimentId": "014d8acf-08fb-421c-8b65-760c8799c627",
    "trainingDataSetId": "5ee3cd7f2d34011913c56941",
    "scoringExperimentId": "76c2b1b-fad7-4b31-8c54-19ecc18b1ea0",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "trainingSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "scoringSchedule": {
        "startTime": "2019-01-01T00:00",
        "endTime": "2019-12-31T00:00",
        "cron": "20 * * * *"
    },
    "updated": "2019-01-02T00:00:00.000Z"
}
```

## 刪除MLService

您可以透過執行DELETE請求（請求路徑中包含目標MLService的ID）來刪除單一MLService。

**API格式**

```http
DELETE /mlServices/{MLSERVICE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MLSERVICE_ID}` | 有效的MLService ID。 |

**请求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices/68d936d8-17e6-44ef-a4b6-c7502055638b \
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
    "detail": "MLService deletion was successful"
}
```

## 依MLInstance ID刪除MLServices

您可以執行將MLInstance ID指定為查詢引數的DELETE要求，來刪除屬於特定MLInstance的所有MLServices。

**API格式**

```http
DELETE /mlServices?mlInstanceId={MLINSTANCE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{MLINSTANCE_ID}` | 有效的MLInstance ID。 |

**请求**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/mlServices?mlInstanceId=46986c8f-7739-4376-8509-0178bdf32cda \
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
    "detail": "MLServices deletion was successful"
}
```

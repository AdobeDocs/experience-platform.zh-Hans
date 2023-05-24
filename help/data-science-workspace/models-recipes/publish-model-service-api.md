---
keywords: Experience Platform；發佈模型；Data Science Workspace；熱門主題；sensei機器學習api
solution: Experience Platform
title: 使用Sensei Machine Learning API發佈模型作為服務
type: Tutorial
description: 本教學課程涵蓋使用Sensei機器學習API將模型發佈為服務的程式。
exl-id: f78b1220-0595-492d-9f8b-c3a312f17253
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 1%

---

# 使用將模型發佈為服務 [!DNL Sensei Machine Learning API]

本教學課程說明使用將模型發佈為服務的程式 [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml).

## 快速入门

此教學課程需要您實際瞭解Adobe Experience Platform資料科學工作區。 在開始本教學課程之前，請檢閱 [資料科學工作區概觀](../home.md) 瞭解此服務的概略介紹。

若要進行本教學課程，您必須擁有現有的ML引擎、ML例項和實驗。 如需如何在API中建立這些專案的步驟，請參閱以下主題中的教學課程： [匯入封裝的配方](./import-packaged-recipe-api.md).

最後，在開始本教學課程之前，請檢閱 [快速入門](../api/getting-started.md) 開發人員指南的區段，瞭解成功對 [!DNL Sensei Machine Learning] API，包括本教學課程使用的必要標頭：

- `{ACCESS_TOKEN}`
- `{ORG_ID}`
- `{API_KEY}`

所有POST、PUT和PATCH請求都需要額外的標頭：

- Content-Type： application/json

### 重要條款

下表概述本教學課程中使用的一些常見術語：

| 搜索词 | 定义 |
| --- | --- |
| **機器學習執行個體（ML執行個體）** | 的例項 [!DNL Sensei] 特定租使用者的引擎，包含特定資料、引數和 [!DNL Sensei] 程式碼。 |
| **试验** | 用來存放訓練實驗回合、評分實驗回合或兩者的傘狀實體。 |
| **排定的實驗** | 說明訓練或評分實驗回合自動化程度的術語，由使用者定義的排程管理。 |
| **實驗執行** | 訓練或評分實驗的特定例項。 特定實驗的多次實驗回合中，用於訓練或評分的資料集值可能有所不同。 |
| **已訓練模型** | 一種機器學習模型，在到達驗證、評估及最終完成的模型之前，由實驗和功能工程程式建立。 |
| **已發佈模型** | 經過訓練、驗證和評估後，最終確定和版本化的模型已送達。 |
| **機器學習服務（ML服務）** | 部署為服務的ML執行個體，以支援使用API端點訓練和評分的隨選請求。 ML服務也可以使用現有的已訓練實驗回合來建立。 |

## 使用現有的訓練實驗回合和已排程的評分建立ML服務

當您以ML服務形式發佈訓練實驗回合時，您可以透過提供評分實驗回合的詳細資訊來排程評分，執行POST請求的裝載。 這會導致建立用於評分的排程實驗實體。

**API格式**

```http
POST /mlServices
```

**请求**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'Content-Type: application/json'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "trainingExperimentId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingExperimentRunId": "5c5af39c73fcec153117eed1",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| 属性 | 描述 |
| --- | --- |
| `mlInstanceId` | 現有的ML執行個體識別碼，用來建立ML服務的訓練實驗回合應與此特定的ML執行個體相對應。 |
| `trainingExperimentId` | 與ML執行個體識別相對應的實驗識別。 |
| `trainingExperimentRunId` | 用於發佈ML服務的特定訓練實驗回合。 |
| `scoringDataSetId` | 參考要用於已排程評分實驗回合的特定資料集的身分識別。 |
| `scoringTimeframe` | 一個整數值，代表篩選要用於評分實驗回合的資料的分鐘數。 例如，值 `10080` 表示過去10080分鐘或168小時的資料將用於每個已排程的評分實驗回合。 請注意，值 `0` 不會篩選資料，資料集內的所有資料都會用於評分。 |
| `scoringSchedule` | 包含有關已排程評分實驗回合的詳細資訊。 |
| `scoringSchedule.startTime` | 指出何時開始評分的日期時間。 |
| `scoringSchedule.endTime` | 指出何時開始評分的日期時間。 |
| `scoringSchedule.cron` | Cron值，表示對「實驗執行」評分的間隔。 |

**响应**

成功的回應會傳回新建立的ML服務的詳細資料，包括其唯一的 `id` 和 `scoringExperimentId` 以取得其對應的評分實驗。


```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingExperimentRunId": "string",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-03-13T00:00",
    "endTime": "2019-03-14T00:00",
    "cron": "30 * * * *"
  },
  "created": "2019-04-08T14:45:25.981Z",
  "updated": "2019-04-08T14:45:25.981Z"
}
```

## 從現有ML執行處理建立ML服務

根據您的特定使用案例和需求，使用ML執行個體建立ML服務在排程訓練和評分實驗執行方面是有彈性的。 本教學課程將逐步解說下列特定案例：

- [您不需要排程訓練，但需要排程評分。](#ml-service-with-scheduled-experiment-for-scoring)
- [訓練和評分都需要排程的實驗回合。](#ml-service-with-scheduled-experiments-for-training-and-scoring)

請注意，您可以使用ML執行個體建立ML服務，而不需要排程任何訓練或評分實驗。 此類ML服務將建立普通實驗實體和單一實驗回合，用於訓練和評分。

### 具有已排程實驗以進行評分的ML服務 {#ml-service-with-scheduled-experiment-for-scoring}

您可以發佈ML執行個體來建立ML服務，其中包含已排程的實驗回合以進行評分，這會建立用於訓練的普通實驗實體。 訓練實驗回合已產生，並將用於所有已排程的評分實驗回合。 確保您擁有 `mlInstanceId`， `trainingDataSetId`、和 `scoringDataSetId` 建立ML服務所需，而且它們存在且是有效值。

**API格式**

```http
POST /mlServices
```

**请求**

```SHELL
curl -X POST 
  https://platform.adobe.io/data/sensei/mlServices
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "Service name",
        "description": "Service description",
        "mlInstanceId": "c4155146-b38f-4a8b-86d8-1de3838c8d87",
        "trainingDataSetId": "5c5af39c73fcec153117eed1",
        "trainingTimeframe": "10000",
        "scoringDataSetId": "5c5af39c73fcec153117eed1",
        "scoringTimeframe": "20000",
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| JSON金鑰 | 描述 |
| --- | --- |
| `mlInstanceId` | 現有的ML執行個體識別碼，代表用來建立ML服務的ML執行個體。 |
| `trainingDataSetId` | 參考要用於訓練實驗的特定資料集的身分識別。 |
| `trainingTimeframe` | 一個整數值，代表篩選要用於訓練實驗之資料的分鐘數。 例如，值 `"10080"` 表示過去10080分鐘或168小時的資料將用於訓練實驗回合。 請注意，值 `"0"` 不會篩選資料，資料集內的所有資料都會用於訓練。 |
| `scoringDataSetId` | 參考要用於已排程評分實驗回合的特定資料集的身分識別。 |
| `scoringTimeframe` | 一個整數值，代表篩選要用於評分實驗回合的資料的分鐘數。 例如，值 `"10080"` 表示過去10080分鐘或168小時的資料將用於每個已排程的評分實驗回合。 請注意，值 `"0"` 不會篩選資料，資料集內的所有資料都會用於評分。 |
| `scoringSchedule` | 包含有關已排程評分實驗回合的詳細資訊。 |
| `scoringSchedule.startTime` | 指出何時開始評分的日期時間。 |
| `scoringSchedule.endTime` | 指出何時開始評分的日期時間。 |
| `scoringSchedule.cron` | Cron值，表示對「實驗執行」評分的間隔。 |

**响应**

成功的回應會傳回新建立的ML服務的詳細資訊。 這包括服務的獨特 `id`，以及 `trainingExperimentId` 和 `scoringExperimentId` 分別用於其對應的訓練和評分實驗。

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

### 具有已排程實驗的ML服務，用於訓練和評分 {#ml-service-with-scheduled-experiments-for-training-and-scoring}

若要將現有的ML執行個體發佈為ML服務，並包含排程的訓練和評分實驗回合，您必須提供訓練和評分排程。 建立此設定的ML服務時，也會建立用於訓練和評分的排程實驗實體。 請注意，訓練和評分排程不一定要相同。 在評分工作執行期間，將會擷取由排程的訓練實驗回合產生的最新訓練模型，並用於排程的評分回合。

**API格式**

```http
POST /mlServices
```

**请求**

```SHELL
curl -X POST 'https://platform.adobe.io/data/sensei/mlServices' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "string",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-10T00:00",
          "cron": "10 * * * *"
        }
      }'
```

| JSON金鑰 | 描述 |
| --- | --- |
| `mlInstanceId` | 現有的ML執行個體識別碼，代表用來建立ML服務的ML執行個體。 |
| `trainingDataSetId` | 參考要用於訓練實驗的特定資料集的身分識別。 |
| `trainingTimeframe` | 一個整數值，代表篩選要用於訓練實驗之資料的分鐘數。 例如，值 `"10080"` 表示過去10080分鐘或168小時的資料將用於訓練實驗回合。 請注意，值 `"0"` 不會篩選資料，資料集內的所有資料都會用於訓練。 |
| `scoringDataSetId` | 參考要用於已排程評分實驗回合的特定資料集的身分識別。 |
| `scoringTimeframe` | 一個整數值，代表篩選要用於評分實驗回合的資料的分鐘數。 例如，值 `"10080"` 表示過去10080分鐘或168小時的資料將用於每個已排程的評分實驗回合。 請注意，值 `"0"` 不會篩選資料，資料集內的所有資料都會用於評分。 |
| `trainingSchedule` | 包含有關已排程的訓練實驗回合的詳細資訊。 |
| `scoringSchedule` | 包含有關已排程評分實驗回合的詳細資訊。 |
| `scoringSchedule.startTime` | 指出何時開始評分的日期時間。 |
| `scoringSchedule.endTime` | 指出何時開始評分的日期時間。 |
| `scoringSchedule.cron` | Cron值，表示對「實驗執行」評分的間隔。 |

**响应**

成功的回應會傳回新建立的ML服務的詳細資訊。 這包括服務的獨特 `id`，以及 `trainingExperimentId` 和 `scoringExperimentId` 和評分實驗的相關資訊。 在下列範例回應中， `trainingSchedule` 和 `scoringSchedule` 建議用於訓練和評分的實驗實體是已排程的實驗。

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",,
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T08:58:10.956Z"
}
```

## 查詢ML服務 {#retrieving-ml-services}

您可以透過建立 `GET` 要求至 `/mlServices` 並提供唯一的 `id` 路徑中的ML服務路徑。

**API格式**

```http
GET /mlServices/{SERVICE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SERVICE_ID}` | 唯一 `id` ML服務的檔案名稱。 |

**请求**

```SHELL
curl -X GET 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回ML服務的詳細資料。

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-10T00:00",
    "cron": "10 * * * *"
  },
  "created": "2019-05-13T23:46:03.478Z",
  "updated": "2019-05-13T23:46:03.478Z"
}
```

>[!NOTE]
>
>擷取不同的ML服務可能會傳回包含更多或更少機碼值組的回應。 上述回應是 [具有已排程的訓練和評分實驗回合的ML服務](#ml-service-with-scheduled-experiments-for-training-and-scoring).


## 排程訓練或評分

如果您想要在已發佈的ML服務上排程評分和訓練，您可以透過更新現有的ML服務來完成此操作。 `PUT` 請求日期 `/mlServices`.

**API格式**

```http
PUT /mlServices/{SERVICE_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SERVICE_ID}` | 唯一 `id` 正在更新的ML服務之URL。 |

**请求**

以下請求會新增「 」，以排程現有ML服務的訓練和評分 `trainingSchedule` 和 `scoringSchedule` 金鑰及其各自的 `startTime`， `endTime`、和 `cron` 金鑰。

```SHELL
curl -X PUT 'https://platform.adobe.io/data/sensei/mlServices/{SERVICE_ID}' 
  -H 'Authorization: {ACCESS_TOKEN}' 
  -H 'x-api-key: {API_KEY}' 
  -H 'x-gw-ims-org-id: {ORG_ID}' 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "name": "string",
        "description": "string",
        "mlInstanceId": "string",
        "trainingExperimentId": "string",
        "trainingDataSetId": "string",
        "trainingTimeframe": "integer",
        "scoringExperimentId": "string",
        "scoringDataSetId": "string",
        "scoringTimeframe": "integer",
        "trainingSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        },
        "scoringSchedule": {
          "startTime": "2019-04-09T00:00",
          "endTime": "2019-04-11T00:00",
          "cron": "20 * * * *"
        }
      }'
```

>[!WARNING]
>
>請勿嘗試修改 `startTime` 關於現有的排程訓練和評分工作。 如果 `startTime` 必須修改，請考慮發佈相同的模型，並重新排程訓練和評分工作。

**响应**

成功的回應會傳回已更新ML服務的詳細資料。

```JSON
{
  "id": "string",
  "name": "string",
  "description": "string",
  "mlInstanceId": "string",
  "trainingExperimentId": "string",
  "trainingDataSetId": "string",
  "trainingTimeframe": "integer",
  "scoringExperimentId": "string",
  "scoringDataSetId": "string",
  "scoringTimeframe": "integer",
  "trainingSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "scoringSchedule": {
    "startTime": "2019-04-09T00:00",
    "endTime": "2019-04-11T00:00",
    "cron": "20 * * * *"
  },
  "created": "2019-04-09T08:58:10.956Z",
  "updated": "2019-04-09T09:43:55.563Z"
}
```

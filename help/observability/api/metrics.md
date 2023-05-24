---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 量度API端點
description: 瞭解如何使用可觀察性深入分析API在Experience Platform中擷取可觀察性量度。
exl-id: 08d416f0-305a-44e2-a2b7-d563b2bdd2d2
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 3%

---

# 量度端點

可觀察性量度可針對Adobe Experience Platform中的各種功能，提供使用狀況統計資料、歷史趨勢和績效指標的深入分析。 此 `/metrics` 中的端點 [!DNL Observability Insights API] 可讓您以程式設計方式擷取您組織活動的量度資料，位置在： [!DNL Platform].

>[!NOTE]
>
>已棄用舊版的量度端點(V1)。 本檔案專注在目前版本(V2)。 有關舊版實作的V1端點的詳細資訊，請參閱 [API參考](https://www.adobe.io/experience-platform-apis/references/observability-insights/#operation/retrieveMetricsV1).

## 快速入门

本指南中使用的API端點是 [[!DNL Observability Insights] API](https://www.adobe.io/experience-platform-apis/references/observability-insights/). 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功對任一檔案發出呼叫所需必要標題的重要資訊 [!DNL Experience Platform] API。

## 擷取可觀察性量度

您可以透過向以下專案發出POST請求來擷取量度資料： `/metrics` 端點，指定您要在裝載中擷取的量度。

**API格式**

```http
POST /metrics
```

**请求**

```sh
curl -X POST \
  https://platform.adobe.io/data/infrastructure/observability/insights/metrics \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "start": "2020-07-14T00:00:00.000Z",
        "end": "2020-07-22T00:00:00.000Z",
        "granularity": "day",
        "metrics": [
          {
            "name": "timeseries.ingestion.dataset.recordsuccess.count",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
                "groupBy": true
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          },
          {
            "name": "timeseries.ingestion.dataset.dailysize",
            "filters": [
              {
                "name": "dataSetId",
                "value": "5eddb21420f516191b7a8dad",
                "groupBy": false
              }
            ],
            "aggregator": "sum",
            "downsample": "sum"
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `start` | 擷取量度資料的最早日期/時間。 |
| `end` | 擷取量度資料的最新日期/時間。 |
| `granularity` | 選擇性欄位，指出量度資料除以的時間間隔。 例如，值 `DAY` 傳回介於以下日期之間的每日量度： `start` 和 `end` 日期，而值 `MONTH` 會改為按月分組量度結果。 使用此欄位時，對應欄位 `downsample` 也必須提供屬性，以指示用來群組資料的彙總函式。 |
| `metrics` | 一個物件陣列，您要擷取的每個量度各一個。 |
| `name` | 「可觀察性深入分析」所識別的量度名稱。 請參閱 [附錄](#available-metrics) 以取得接受的量度名稱完整清單。 |
| `filters` | 選擇性欄位，可讓您依據特定資料集篩選量度。 欄位是一個物件陣列（每個濾鏡各一個），每個物件包含下列屬性： <ul><li>`name`：要篩選量度的實體型別。 目前，僅限 `dataSets` 支援。</li><li>`value`：一或多個資料集的ID。 多個資料集ID可作為單一字串提供，每個ID都以垂直長條字元(`\|`)。</li><li>`groupBy`：設為true時，代表對應的 `value` 代表應個別傳回其量度結果的多個資料集。 如果設為false，則這些資料集的量度結果會分組在一起。</li></ul> |
| `aggregator` | 指定用來將多個時間序列記錄分組為單一結果的彙總函式。 如需可用彙總的詳細資訊，請參閱 [OpenTSDB檔案](https://docs.w3cub.com/opentsdb/user_guide/query/aggregators). |
| `downsample` | 此選用欄位可讓您指定彙總函式，將欄位排序為間隔（或「貯體」），以降低量度資料的取樣率。 縮減取樣間隔由 `granularity` 屬性。 如需縮減取樣的相關詳細資訊，請參閱 [OpenTSDB檔案](https://docs.w3cub.com/opentsdb/user_guide/query/aggregators). |

{style="table-layout:auto"}

**响应**

成功的回應會針對請求中指定的量度和篩選器傳回產生的資料點。

```json
{
  "metricResponses": [
    {
      "metric": "timeseries.ingestion.dataset.recordsuccess.count",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5edcfb2fbb642119194c7d94|5eddb21420f516191b7a8dad",
          "groupBy": true
        }
      ],
      "datapoints": [
        {
          "groupBy": {
            "dataSetId": "5edcfb2fbb642119194c7d94"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        },
        {
          "groupBy": {
            "dataSetId": "5eddb21420f516191b7a8dad"
          },
          "dps": {
            "2020-07-14T00:00:00Z": 44.0,
            "2020-07-15T00:00:00Z": 46.0,
            "2020-07-16T00:00:00Z": 36.0,
            "2020-07-17T00:00:00Z": 50.0,
            "2020-07-18T00:00:00Z": 38.0,
            "2020-07-19T00:00:00Z": 40.0,
            "2020-07-20T00:00:00Z": 42.0,
            "2020-07-21T00:00:00Z": 42.0,
            "2020-07-22T00:00:00Z": 50.0
          }
        }
      ],
      "granularity": "DAY"
    },
    {
      "metric": "timeseries.ingestion.dataset.dailysize",
      "filters": [
        {
          "name": "dataSetId",
          "value": "5eddb21420f516191b7a8dad",
          "groupBy": false
        }
      ],
      "datapoints": [
        {
          "groupBy": {},
          "dps": {
            "2020-07-14T00:00:00Z": 38455.0,
            "2020-07-15T00:00:00Z": 40213.0,
            "2020-07-16T00:00:00Z": 31476.0,
            "2020-07-17T00:00:00Z": 43705.0,
            "2020-07-18T00:00:00Z": 33227.0,
            "2020-07-19T00:00:00Z": 34977.0,
            "2020-07-20T00:00:00Z": 36735.0,
            "2020-07-21T00:00:00Z": 36737.0,
            "2020-07-22T00:00:00Z": 43715.0
          }
        }
      ],
      "granularity": "DAY"
    }
  ]
}
```

| 属性 | 描述 |
| --- | --- |
| `metricResponses` | 一個陣列，其物件代表要求中指定的每個度量。 每個物件都包含有關篩選設定和傳回量度資料的資訊。 |
| `metric` | 請求中提供的其中一個量度的名稱。 |
| `filters` | 指定量度的篩選器設定。 |
| `datapoints` | 一個陣列，其物件代表指定量度和篩選器的結果。 陣列中的物件數目取決於請求中提供的篩選選項。 如果未提供任何篩選器，則陣列將僅包含代表所有資料集的單一物件。 |
| `groupBy` | 如果在以下專案指定了多個資料集： `filter` 量度的屬性，以及 `groupBy` 選項在請求中設為true，此物件將包含對應資料集的識別碼 `dps` 屬性套用至。<br><br>如果此物件在回應中顯示為空白，則對應的 `dps` 屬性會套用至 `filters` 陣列（或中的所有資料集） [!DNL Platform] （若未提供任何篩選器）。 |
| `dps` | 針對指定的量度、篩選器和時間範圍傳回的資料。 此物件中的每個索引鍵都代表一個時間戳記，其中包含指定量度的對應值。 每個資料點之間的時段取決於 `granularity` 請求中指定的值。 |

{style="table-layout:auto"}

## 附录

下節包含有關使用的其他資訊 `/metrics` 端點。

### 可用量度 {#available-metrics}

下表列出以下對象公開的所有量度： [!DNL Observability Insights]，劃分依據 [!DNL Platform] 服務。 每個量度都包含說明和接受的ID查詢引數。

>[!NOTE]
>
>除非另有說明，否則所有列出的ID查詢引數均為選用引數。

#### [!DNL Data Ingestion] {#ingestion}

下表概述Adobe Experience Platform的量度 [!DNL Data Ingestion]. 中的量度 **粗體** 是串流擷取量度。

| 深入分析量度 | 描述 | ID查詢引數 |
| ---- | ---- | ---- |
| timeseries.ingestion.dataset.size | 針對一個資料集或所有資料集擷取的所有資料累計大小。 | 数据集 ID |
| timeseries.ingestion.dataset.dailysize | 針對一個資料集或所有資料集根據每日使用量擷取的資料大小。 | 数据集 ID |
| timeseries.ingestion.dataset.batchfailed.count | 一個資料集或所有資料集失敗的批次數量。 | 数据集 ID |
| timeseries.ingestion.dataset.batchsuccess.count | 為一個資料集或所有資料集擷取的批次數。 | 数据集 ID |
| timeseries.ingestion.dataset.recordsuccess.count | 為一個資料集或所有資料集擷取的記錄數。 | 数据集 ID |
| **timeseries.data.collection.validation.category.presence.count** | 一個資料集或所有資料集的無效「存在」訊息總數。 | 数据集 ID |
| **timeseries.data.collection.inlet.total.messages.received** | 針對一個資料輸入或所有資料輸入所接收的訊息總數。 | 入口ID |
| **timeseries.data.collection.inlet.total.messages.size.received** | 針對一個資料輸入點或所有資料輸入點所接收的總資料大小。 | 入口ID |
| **timeseries.data.collection.inlet.success** | 成功呼叫一個資料輸入點或所有資料輸入點的HTTP呼叫總數。 | 入口ID |
| **timeseries.data.collection.inlet.failure** | 對單一資料匯入點或所有資料匯入點發出失敗的HTTP呼叫總數。 | 入口ID |

{style="table-layout:auto"}

#### [!DNL Identity Service] {#identity}

下表概述Adobe Experience Platform的量度 [!DNL Identity Service].

| 深入分析量度 | 描述 | ID查詢引數 |
| ---- | ---- | ---- |
| timeseries.identity.dataset.recordsuccess.count | 寫入其資料來源的記錄數 [!DNL Identity Service]，適用於一個資料集或所有資料集。 | 数据集 ID |
| timeseries.identity.dataset.recordfailed.count | 失敗的記錄數，依據為 [!DNL Identity Service]，適用於一個資料集或所有資料集。 | 数据集 ID |
| timeseries.identity.dataset.namespacecode.recordfailed.count | 名稱空間失敗的身分記錄數目。 | 名稱空間ID (**必填**) |
| timeseries.identity.dataset.namespacecode.recordskipped.count | 名稱空間略過的身分記錄數。 | 名稱空間ID (**必填**) |
| timeseries.identity.graph.imsorg.uniqueidentities.count | 貴組織儲存在身分圖表中的唯一身分數量。 | 不适用 |
| timeseries.identity.graph.imsorg.namespacecode.uniqueidentities.count | 為名稱空間儲存在身分圖表中的唯一身分數目。 | 名稱空間ID (**必填**) |
| timeseries.identity.graph.imsorg.graphstrength.uniqueidentities.count | 針對特定圖表強度（「未知」、「弱」或「強」）儲存在身分圖表中的獨特身分數量。 | 圖表強度(**必填**) |

{style="table-layout:auto"}

#### [!DNL Real-Time Customer Profile] {#profile}

下表概述以下專案的量度 [!DNL Real-Time Customer Profile].

| 深入分析量度 | 描述 | ID查詢引數 |
| ---- | ---- | ---- |
| timeseries.profiles.dataset.recordread.count | 從「 」讀取的記錄數 [!DNL Data Lake] 作者： [!DNL Profile]，適用於一個資料集或所有資料集。 | 数据集 ID |
| timeseries.profiles.dataset.recordsuccess.count | 寫入其資料來源的記錄數 [!DNL Profile]，適用於一個資料集或所有資料集。 | 数据集 ID |
| timeseries.profiles.dataset.batchsuccess.count | 數量 [!DNL Profile] 為資料集或所有資料集擷取的批次。 | 数据集 ID |

{style="table-layout:auto"}

### 错误消息

來自 `/metrics` 端點在某些情況下可能會傳回錯誤訊息。 這些錯誤訊息會以下列格式傳回：

```json
{
    "type": "http://ns.adobe.com/aep/errors/INSGHT-1000-400",
    "title": "Bad Request - Start date cannot be after end date.",
    "status": 400,
    "report": {
        "tenantInfo": {
            "sandboxName": "prod",
            "sandboxId": "49f58060-5d47-34rd-aawf-a5384333ff12",
            "imsOrgId": "{ORG_ID}"
        },
        "additionalContext": null
    },
    "error-chain": [
        {
            "serviceId": "INSGHT",
            "errorCode": "INSGHT-1000-400",
            "invokingServiceId": "INSGHT",
            "unixTimeStampMs": 1602095177129
        }
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `title` | 包含錯誤訊息及其可能發生原因的字串。 |
| `report` | 包含有關錯誤的內容相關資訊，包括觸發錯誤的作業中使用的沙箱和組織。 |

{style="table-layout:auto"}

下表列出API可傳回的不同錯誤代碼：

| 错误代码 | 标题 | 描述 |
| --- | --- | --- |
| `INSGHT-1000-400` | 錯誤請求承載 | 請求承載發生問題。 請確定您完全符合顯示的裝載格式 [以上](#v2). 任何可能的原因都會觸發此錯誤：<ul><li>缺少必填欄位，例如 `aggregator`</li><li>無效的量度</li><li>請求包含無效的彙總</li><li>開始日期發生在結束日期之後</li></ul> |
| `INSGHT-1001-400` | 量度查詢失敗 | 嘗試查詢量度資料庫時發生錯誤，因為錯誤請求或查詢本身無法剖析。 在重試之前，請確定您的請求格式正確。 |
| `INSGHT-1001-500` | 量度查詢失敗 | 嘗試查詢量度資料庫時發生錯誤，因為伺服器發生錯誤。 請再次嘗試該請求，如果問題仍然存在，請聯絡Adobe支援。 |
| `INSGHT-1002-500` | 服務錯誤 | 由於內部錯誤，無法處理該請求。 請再次嘗試該請求，如果問題仍然存在，請聯絡Adobe支援。 |
| `INSGHT-1003-401` | 沙箱驗證錯誤 | 由於沙箱驗證錯誤，無法處理該請求。 確定您在中提供的沙箱名稱 `x-sandbox-name` 標題代表貴組織在重試請求之前啟用的有效沙箱。 |

{style="table-layout:auto"}

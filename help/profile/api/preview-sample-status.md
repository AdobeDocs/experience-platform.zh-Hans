---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；預覽；範例
title: 預覽範例狀態（設定檔預覽） API端點
description: Real-Time Customer Profile API的預覽範例狀態端點可讓您預覽設定檔資料的最新成功範例、依資料集和身分列出設定檔分佈，並產生顯示資料集重疊、身分重疊和未拼接設定檔的報告。
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2873'
ht-degree: 1%

---

# 預覽範例狀態端點（設定檔預覽）

Adobe Experience Platform可讓您從多個來源擷取客戶資料，以便為個別客戶建立強大且統一的設定檔。 將資料內嵌至Platform後，會執行範例工作以更新設定檔計數和其他即時客戶設定檔資料相關量度。

此範例工作的結果可以使用檢視 `/previewsamplestatus` 端點，即時客戶設定檔API的一部分。 此端點也可用來依資料集和身分名稱空間列出設定檔分佈，以及產生多個報表，以瞭解貴組織設定檔存放區的組成。 本指南會逐步說明使用檢視這些量度所需的步驟。 `/previewsamplestatus` api端點。

>[!NOTE]
>
>Adobe Experience Platform Segmentation Service API提供預估和預覽端點，可讓您檢視關於區段定義的摘要層級資訊，以協助確保您隔離預期對象。 若要尋找使用區段預覽和估計端點的詳細步驟，請造訪 [預覽和估計端點指南](../../segmentation/api/previews-and-estimates.md)，的一部分 [!DNL Segmentation] API開發人員指南。

## 快速入门

本指南中使用的API端點是 [[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). 在繼續之前，請檢閱 [快速入門手冊](getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功對任一檔案發出呼叫所需必要標題的重要資訊 [!DNL Experience Platform] API。

## 設定檔片段與合併的設定檔

本指南同時參考了「設定檔片段」和「合併的設定檔」。 在繼續之前，請務必瞭解這些辭彙之間的差異。

每個個別客戶設定檔都由多個設定檔片段組成，這些片段已合併以形成該客戶的單一檢視。 例如，如果客戶跨多個管道與您的品牌互動，您的組織可能會有多個與該單一客戶相關的設定檔片段出現在多個資料集中。

將設定檔片段擷取至Platform時，會合併這些片段（根據合併原則），以為該客戶建立單一設定檔。 因此，由於每個設定檔都是由多個片段所組成，因此設定檔片段的總數可能一律高於合併的設定檔總數。

若要進一步瞭解設定檔及其在Experience Platform中的角色，請先閱讀 [即時客戶個人檔案總覽](../home.md).

## 如何觸發範例工作

當啟用即時客戶設定檔的資料內嵌到時 [!DNL Platform]，會儲存在設定檔資料存放區中。 當將記錄擷取至設定檔存放區增加或減少總設定檔計數超過5%時，會觸發取樣工作以更新計數。 範例的觸發方式取決於所使用的擷取型別：

* 對象 **串流資料工作流程**，會每小時進行一次檢查，以判斷是否已達到5%的增加或減少臨界值。 如果有，則會自動觸發範例工作以更新計數。
* 對象 **批次擷取**，在成功將批次擷取至設定檔存放區後15分鐘內，如果符合5%增加或減少臨界值，則會執行工作以更新計數。 使用設定檔API，您可以預覽最新成功的範例作業，以及依資料集和身分名稱空間列出設定檔分佈。

依名稱空間量度的設定檔計數和設定檔也可在 [!UICONTROL 設定檔] Experience PlatformUI的區段。 如需有關如何使用UI存取設定檔資料的資訊，請造訪 [[!DNL Profile] UI指南](../ui/user-guide.md).

## 檢視上一個範例狀態 {#view-last-sample-status}

您可以對執行GET要求 `/previewsamplestatus` 端點可檢視您的組織上一次成功執行之範例工作的詳細資訊。 這包括範例中的設定檔總數，以及設定檔計數量度，或您的組織在Experience Platform內擁有的設定檔總數。

設定檔計數是在合併設定檔片段後產生，以為每個個別客戶形成單一設定檔。 換言之，當設定檔片段合併在一起時，它們會傳回「1」設定檔計數，因為它們都與同一個人相關。

設定檔計數也包含具有屬性（記錄資料）的設定檔，以及僅包含時間序列（事件）資料(例如Adobe Analytics設定檔)的設定檔。 範例工作會在擷取設定檔資料時定期重新整理，以提供Platform內最新的設定檔總數。

**API格式**

```http
GET /previewsamplestatus
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

回應包含針對組織執行的最後一個成功範例工作的詳細資訊。

>[!NOTE]
>
>在此範例回應中， `numRowsToRead` 和 `totalRows` 彼此相等。 根據貴組織在Experience Platform中的設定檔數量，情況可能會如此。 不過，這兩個數字通常不同，而且 `numRowsToRead` 是較小的數字，因為它代表範例為設定檔總數的子集(`totalRows`)。

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "cosmosDocCount": "\"300803\"",
  "totalFragmentCount": 47429,
  "lastSuccessfulBatchTimestamp": "\"null\"",
  "streamingDriven": "\"false\"",
  "totalRows": "41003",
  "lastBatchId": "\"null\"",
  "status": "TASK_FINISHED",
  "samplingRatio": 1.0,
  "mergeStrategy": "timestampOrdered_auto",
  "lastSampledTimestamp": "2020-08-01 17:57:57.0"
}
```

| 属性 | 描述 |
|---|---|
| `numRowsToRead` | 範例中合併的設定檔總數。 |
| `sampleJobRunning` | 傳回的布林值 `true` 當範例工作正在進行時。 將批次檔案上傳至時，實際新增至設定檔存放區時，產生的延遲可透明化。 |
| `cosmosDocCount` | Cosmos中的檔案總數。 |
| `totalFragmentCount` | 設定檔存放區中的設定檔片段總數。 |
| `lastSuccessfulBatchTimestamp` | 上次成功的批次擷取時間戳記。 |
| `streamingDriven` | *此欄位已棄用，且未包含回應的任何重要意義。* |
| `totalRows` | Experience Platform中合併的設定檔總數，也稱為「設定檔計數」。 |
| `lastBatchId` | 上次批次擷取ID。 |
| `status` | 上一個範例的狀態。 |
| `samplingRatio` | 合併設定檔取樣比例(`numRowsToRead`)至合併的設定檔總數(`totalRows`)，以十進位格式的百分比表示。 |
| `mergeStrategy` | 範例中使用的合併策略。 |
| `lastSampledTimestamp` | 上次成功的範例時間戳記。 |

## 依資料集列出設定檔分佈

GET若要依資料集檢視設定檔的分佈，您可以對 `/previewsamplestatus/report/dataset` 端點。

**API格式**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在該日期執行了多個報表，則會傳回該日期的最新報表。 如果指定日期不存在報表，則會傳回404 （找不到）錯誤。 如果未指定日期，則會傳回最近的報告。 格式：YYYY-MM-DD。 示例：`date=2024-12-31` |

**请求**

以下請求使用 `date` 引數以傳回指定日期的最新報告。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

回應包括 `data` 陣列，包含資料集物件清單。 顯示的回應已截斷，顯示三個資料集。

>[!NOTE]
>
>如果日期存在多個報表，則僅傳回最新的報表。 如果提供的日期不存在資料集報告，則會傳回HTTP狀態404 （找不到）。

```json
{
  "data": [
    {
      "sampleCount": 12577,
      "samplePercentage": 0.306734,
      "fullIDsCount": 20988,
      "fullIDsPercentage": 0.511865,
      "name": "CRM Profiles",
      "description": "Profiles from the CRM.",
      "value": "5f160106be34361915754b9c",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697",
    },
    {
      "sampleCount": 12938,
      "samplePercentage": 0.315538,
      "fullIDsCount": 21796,
      "fullIDsPercentage": 0.531571,
      "name": "AAM Authenticated Profiles",
      "description": "This data set contains AAM authenticated profiles.",
      "value": "5dc77ec6eed47f18a796ca90",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    },
    {
      "sampleCount": 22725,
      "samplePercentage": 0.554228,
      "fullIDsCount": 41003,
      "fullIDsPercentage": 1.0,
      "name": "Loyalty Program Members",
      "description": "Members of the loyalty program at all levels.",
      "value": "5d0fda92274e55144d4de620",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| 属性 | 描述 |
|---|---|
| `sampleCount` | 使用此資料集ID的抽樣合併設定檔總數。 |
| `samplePercentage` | 此 `sampleCount` 佔抽樣合併設定檔總數的百分比( `numRowsToRead` 中傳回的值 [上一個範例狀態](#view-last-sample-status))，以十進位格式表示。 |
| `fullIDsCount` | 具有此資料集ID的合併設定檔總數。 |
| `fullIDsPercentage` | 此 `fullIDsCount` 佔合併的設定檔總數的百分比( `totalRows` 中傳回的值 [上一個範例狀態](#view-last-sample-status))，以十進位格式表示。 |
| `name` | 資料集的名稱，在資料集建立期間提供。 |
| `description` | 資料集的說明，如資料集建立期間所提供。 |
| `value` | 資料集的ID。 |
| `streamingIngestionEnabled` | 資料集是否已啟用串流擷取。 |
| `createdUser` | 建立資料集之使用者的使用者ID。 |
| `reportTimestamp` | 報表的時間戳記。 若為 `date` 引數是在請求期間提供，而傳回的報表是對應於提供的日期。 若否 `date` 引數之後，會傳回最新的報表。 |

## 依身分名稱空間列出設定檔分佈

您可以對執行GET要求 `/previewsamplestatus/report/namespace` 端點，用來檢視設定檔存放區中所有合併設定檔的依身分名稱空間劃分。 這包括Adobe提供的標準身分識別，以及貴組織定義的自訂身分識別。

身分識別名稱空間是Adobe Experience Platform Identity Service的重要元件，可做為客戶資料相關內容的指標。 若要進一步瞭解，請先閱讀 [身分名稱空間總覽](../../identity-service/namespaces.md).

>[!NOTE]
>
>依名稱空間區分的設定檔總數（加總針對每個名稱空間顯示的值）可能會高於設定檔計數量度，因為一個設定檔可能會與多個名稱空間建立關聯。 例如，如果客戶在多個頻道上與您的品牌互動，則多個名稱空間會與該個別客戶相關聯。

**API格式**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在該日期執行了多個報表，則會傳回該日期的最新報表。 如果指定日期不存在報表，則會傳回404 （找不到）錯誤。 如果未指定日期，則會傳回最近的報告。 格式：YYYY-MM-DD。 示例：`date=2024-12-31` |

**请求**

以下請求未指定 `date` 引數，因此將傳回最新的報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

回應包括 `data` 陣列，包含每個名稱空間的詳細資訊的個別物件。 顯示的回應已截斷，顯示四個名稱空間。

```json
{
  "data": [
    {
      "sampleCount": 12148,
      "samplePercentage": 0.296271,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 13141,
      "fullIDsCount": 12631,
      "fullIDsPercentage": 0.308051,
      "code": "Email",
      "value": "6"
    },
    {
      "sampleCount": 6989,
      "samplePercentage": 0.170451,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 7543,
      "fullIDsCount": 7042,
      "fullIDsPercentage": 0.171744,
      "code": "ECID",
      "value": "4"
    },
    {
      "sampleCount": 888,
      "samplePercentage": 0.021657,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 3801,
      "fullIDsCount": 3206,
      "fullIDsPercentage": 0.078189,
      "code": "AAID",
      "value": "10"
    },
    {
      "sampleCount": 21809,
      "samplePercentage": 0.531888,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 27023,
      "fullIDsCount": 21936,
      "fullIDsPercentage": 0.534985,
      "code": "Phone",
      "value": "7"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| 属性 | 描述 |
|---|---|
| `sampleCount` | 名稱空間中抽樣合併的設定檔總數。 |
| `samplePercentage` | 此 `sampleCount` 以抽樣合併設定檔的百分比表示( `numRowsToRead` 中傳回的值 [上一個範例狀態](#view-last-sample-status))，以十進位格式表示。 |
| `reportTimestamp` | 報表的時間戳記。 若為 `date` 引數是在請求期間提供，而傳回的報表是對應於提供的日期。 若否 `date` 引數之後，會傳回最新的報表。 |
| `fullIDsFragmentCount` | 名稱空間中的設定檔片段總數。 |
| `fullIDsCount` | 名稱空間中合併的設定檔總數。 |
| `fullIDsPercentage` | 此 `fullIDsCount` 佔合併的設定檔總數的百分比( `totalRows` 中傳回的值 [上一個範例狀態](#view-last-sample-status))，以十進位格式表示。 |
| `code` | 此 `code` 用於名稱空間。 這可以在使用名稱空間時找到 [Adobe Experience Platform Identity服務API](../../identity-service/api/list-namespaces.md) 也稱為 [!UICONTROL 身分符號] 在Experience PlatformUI中。 若要進一步瞭解，請造訪 [身分名稱空間總覽](../../identity-service/namespaces.md). |
| `value` | 此 `id` 名稱空間的值。 這可以在使用名稱空間時找到 [身分識別服務API](../../identity-service/api/list-namespaces.md). |

## 產生資料集重疊報告

資料集重疊報表可公開對可定址對象貢獻最大的資料集（合併的設定檔），讓您檢視組織設定檔存放區的組成。 除了提供您資料的深入分析，此報表還能協助您採取動作來最佳化授權使用，例如設定特定資料集的到期時間。

您可以透過對「 」執行GET請求來產生資料集重疊報表。 `/previewsamplestatus/report/dataset/overlap` 端點。

如需逐步指示，瞭解如何使用命令列或Postman UI產生資料集重疊報告，請參閱 [產生資料集重疊報表教學課程](../tutorials/dataset-overlap-report.md).

**API格式**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在相同日期執行了多個報表，則會傳回該日期的最新報表。 如果指定日期不存在報表，則會傳回404 （找不到）錯誤。 如果未指定日期，則會傳回最近的報告。 格式：YYYY-MM-DD。 示例：`date=2024-12-31` |

**请求**

以下請求使用 `date` 引數以傳回指定日期的最新報告。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**响应**

成功的請求會傳回HTTP狀態200 （確定）和資料集重疊報表。

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-12-29T19:55:31.147"
}
```

| 属性 | 描述 |
|---|---|
| `data` | 此 `data` 物件包含以逗號分隔的資料集清單及其各自的設定檔計數。 |
| `reportTimestamp` | 報表的時間戳記。 若為 `date` 引數是在請求期間提供，而傳回的報表是對應於提供的日期。 若否 `date` 引數之後，會傳回最新的報表。 |

### 解譯資料集重疊報表

報表的結果可從回應中的資料集和設定檔計數中解譯。 考量下列範例報告 `data` 物件：

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

此報表提供下列資訊：

* 有123個設定檔包含來自以下資料集的資料： `5d92921872831c163452edc8`， `5da7292579975918a851db57`， `5eb2cdc6fa3f9a18a7592a98`.
* 共有454,412個設定檔包含來自這兩個資料集的資料： `5d92921872831c163452edc8` 和 `5eb2cdc6fa3f9a18a7592a98`.
* 有107個設定檔僅由資料集中的資料組成 `5eeda0032af7bb19162172a7`.
* 組織內共有454,642個設定檔。

## 產生身分名稱空間重疊報表 {#identity-overlap-report}

身分名稱空間重疊報表可公開對可定址對象貢獻最大的身分名稱空間（合併的設定檔），讓您檢視組織設定檔存放區的組成。 這包括Adobe提供的標準身分名稱空間，以及貴組織定義的自訂身分名稱空間。

您可以透過對「 」執行GET要求，產生身分名稱空間重疊報表。 `/previewsamplestatus/report/namespace/overlap` 端點。

**API格式**

```http
GET /previewsamplestatus/report/namespace/overlap
GET /previewsamplestatus/report/namespace/overlap?{QUERY_PARAMETERS}
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在相同日期執行了多個報表，則會傳回該日期的最新報表。 如果指定日期不存在報表，則會傳回404 （找不到）錯誤。 如果未指定日期，則會傳回最近的報告。 格式：YYYY-MM-DD。 示例：`date=2024-12-31` |

**请求**

以下請求使用 `date` 引數以傳回指定日期的最新報告。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**响应**

成功的請求會傳回HTTP狀態200 （確定）和身分名稱空間重疊報表。

```json
{
    "data": {
        "Email,crmid,loyal": 2,
        "ECID,Email,crmid": 7,
        "ECID,Email,mobilenr": 12,
        "AAID,ECID,loyal": 1,
        "mobilenr": 25,
        "AAID,ECID": 1508,
        "ECID,crmid": 1,
        "AAID,ECID,crmid": 2,
        "Email,crmid": 328,
        "CORE": 49,
        "AAID": 446,
        "crmid,loyal": 20988,
        "Email": 10904,
        "crmid": 249,
        "ECID,Email": 74,
        "Phone": 40,
        "Email,Phone,loyal": 48,
        "AAID,AVID,ECID": 85,
        "Email,loyal": 1002,
        "AAID,ECID,Email,Phone,crmid": 5,
        "AAID,ECID,Email,crmid,loyal": 23,
        "AAID,AVID,ECID,Email,crmid": 2,
        "AVID": 3,
        "AAID,ECID,Phone": 1,
        "loyal": 43,
        "ECID,Email,crmid,loyal": 6,
        "AAID,ECID,Email,Phone,crmid,loyal": 1,
        "AAID,ECID,Email": 2,
        "AAID,ECID,Email,crmid": 142,
        "AVID,ECID": 24,
        "ECID": 6565
    },
    "reportTimestamp": "2021-12-29T16:55:03.624"
}
```

| 属性 | 描述 |
|---|---|
| `data` | 此 `data` 物件包含以逗號分隔的清單，其中包含身分名稱空間程式碼及其各自設定檔計數的唯一組合。 |
| 名稱空間程式碼 | 此 `code` 是每個身分名稱空間名稱的簡短形式。 每個專案的對應 `code` 至其 `name` 可使用找到 [Adobe Experience Platform Identity服務API](../../identity-service/api/list-namespaces.md). 此 `code` 也稱為 [!UICONTROL 身分符號] 在Experience PlatformUI中。 若要進一步瞭解，請造訪 [身分名稱空間總覽](../../identity-service/namespaces.md). |
| `reportTimestamp` | 報表的時間戳記。 若為 `date` 引數是在請求期間提供，而傳回的報表是對應於提供的日期。 若否 `date` 引數之後，會傳回最新的報表。 |

### 解讀身分名稱空間重疊報表

報表的結果可從回應中的身分和個人資料計數中解譯。 每一列的數值可告訴您有多少設定檔是由標準和自訂身分名稱空間的精確組合所組成。

請考量以下摘錄自 `data` 物件：

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

此報表提供下列資訊：

* 共有142個設定檔組成 `AAID`， `ECID`、和 `Email` 標準身分以及自訂 `crmid` 身分名稱空間。
* 共有24個設定檔組成 `AAID` 和 `ECID` 身分名稱空間。
* 有6,565個設定檔僅包含 `ECID` 身分。

## 產生未拼接的設定檔報告

您可以透過未拼接的設定檔報表，進一步瞭解組織設定檔存放區的構成。 「未拼接」設定檔是僅包含一個設定檔片段的設定檔。 「未知」設定檔是與假名身分名稱空間相關聯的設定檔，例如 `ECID` 和 `AAID`. 未知的設定檔處於非使用中狀態，這表示它們未在指定的時段內新增事件。 「未拼接的設定檔」報表提供7、30、60、90和120天期間的設定檔劃分。

您可以透過對執行GET請求來產生未拼接的設定檔報告 `/previewsamplestatus/report/unstitchedProfiles` 端點。

**API格式**

```http
GET /previewsamplestatus/report/unstitchedProfiles
```

**请求**

以下請求會傳回未拼接的設定檔報表。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/unstitchedProfiles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**响应**

成功的請求會傳回HTTP狀態200 （確定）和未拼接的設定檔報表。

>[!NOTE]
>
>出於本指南的目的，報表已截斷為僅包含 `"120days"` 和&quot;`7days`&quot;時段。 完整未拼接設定檔報告提供7、30、60、90和120天期間的設定檔劃分。

```json
{
  "data": {
      "totalNumberOfProfiles": 63606,
      "totalNumberOfEvents": 130977,
      "unstitchedProfiles": {
          "120days": {
              "countOfProfiles": 1644,
              "eventsAssociated": 26824,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 18,
                      "eventsAssociated": 95
                  },
                  "loyal": {
                      "countOfProfiles": 26,
                      "eventsAssociated": 71
                  },
                  "ECID": {
                      "countOfProfiles": 1600,
                      "eventsAssociated": 26658
                  }
              }
          },
          "7days": {
              "countOfProfiles": 1782,
              "eventsAssociated": 29151,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 19,
                      "eventsAssociated": 97
                  },
                  "ECID": {
                      "countOfProfiles": 1734,
                      "eventsAssociated": 28591
                  },
                  "loyal": {
                      "countOfProfiles": 29,
                      "eventsAssociated": 463
                  }
              }
          }
      }
  },
  "reportTimestamp": "2025-08-25T22:14:55.186"
}
```

| 属性 | 描述 |
|---|---|
| `data` | 此 `data` 物件包含針對未拼接設定檔報告傳回的資訊。 |
| `totalNumberOfProfiles` | 設定檔存放區中的不重複設定檔總數。 這等同於可定址對象計數。 它包含已知和未拼接的設定檔。 |
| `totalNumberOfEvents` | 設定檔存放區中的ExperienceEvents總數。 |
| `unstitchedProfiles` | 包含依時段劃分之未拼接設定檔的物件。 「未拼接的設定檔」報表提供7、30、60、90和120天時間週期的設定檔劃分。 |
| `countOfProfiles` | 時段內未拼接的設定檔計數，或名稱空間未拼接的設定檔計數。 |
| `eventsAssociated` | 時間範圍的ExperienceEvents數目或名稱空間的事件數目。 |
| `nsDistribution` | 包含個別身分名稱空間的物件，會針對每個名稱空間分配未拼接的設定檔和事件。 注意：將總計相加 `countOfProfiles` 中每個身分名稱空間的 `nsDistribution` 物件等於 `countOfProfiles` 用於時段。 下列專案也同樣如此： `eventsAssociated` 每個名稱空間和總計 `eventsAssociated` 每個時段。 |
| `reportTimestamp` | 報表的時間戳記。 |

### 解譯未拼接的設定檔報告

報表結果可讓您深入瞭解貴組織在其設定檔存放區中有多少未拼接和非作用中的設定檔。

請考量以下摘錄自 `data` 物件：

```json
  "7days": {
    "countOfProfiles": 1782,
    "eventsAssociated": 29151,
    "nsDistribution": {
      "Email": {
        "countOfProfiles": 19,
        "eventsAssociated": 97
      },
      "ECID": {
        "countOfProfiles": 1734,
        "eventsAssociated": 28591
      },
      "loyal": {
        "countOfProfiles": 29,
        "eventsAssociated": 463
      }
    }
  }
```

此報表提供下列資訊：

* 有1,782個設定檔僅包含一個設定檔片段，且過去七天沒有新事件。
* 有29,151個ExperienceEvents與1,782個未拼接的設定檔相關聯。
* 有1,734個未拼接的設定檔包含ECID的身分名稱空間中的單一設定檔片段。
* 有28,591個事件與1,734個未拼接的設定檔相關聯，這些設定檔包含ECID的身分名稱空間中的單一設定檔片段。

## 后续步骤

現在您知道如何在設定檔存放區中預覽範例資料，並對資料執行多個報告，您也可以使用Segmentation Service API的估計和預覽端點，檢視有關區段定義的摘要層級資訊。 此資訊可協助您確保區段中的預期對象已隔離。 若要進一步瞭解如何使用分段API進行區段預覽和預估，請造訪 [預覽和估算端點指南](../../segmentation/api/previews-and-estimates.md).


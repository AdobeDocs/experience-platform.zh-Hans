---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；報表；資料集重疊報表；設定檔資料
title: 產生資料集重疊報表
type: Tutorial
description: 本教學課程概述使用即時客戶設定檔API產生資料集重疊報表的必要步驟。
exl-id: 90894ed3-b09e-435d-a9e3-18fd6dc8e907
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 1%

---

# 產生資料集重疊報告

資料集重疊報表可讓您檢視組織內 [!DNL Profile] 透過公開對可定址對象（設定檔）貢獻最大的資料集進行儲存。

除了提供您資料的深入分析，此報表還可協助您採取動作以最佳化授權使用，例如設定特定資料的有效期限限制。

本教學課程概述使用產生資料集重疊報告所需的步驟。 [!DNL Real-Time Customer Profile] API和解讀貴組織的結果。

## 快速入门

若要使用Adobe Experience Platform API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以收集所需標題的值。 若要進一步瞭解Experience PlatformAPI，請參閱 [Platform API快速入門檔案](../../landing/api-guide.md).

本教學課程中所有API呼叫的必要標題為：

* `Authorization: Bearer {ACCESS_TOKEN}`：此 `Authorization` 標頭需要前置詞語的存取權杖 `Bearer`. 新的存取權杖值必須每24小時產生一次。
* `x-api-key: {API_KEY}`：此 `API Key` 也稱為 `Client ID` 而是一個只需產生一次的值。
* `x-gw-ims-org-id: {ORG_ID}`：組織ID只需產生一次。

完成驗證教學課程並收集所需標題的值後，您就可以開始對Real-Time Customer API發出呼叫了。

## 使用命令列產生資料集重疊報告

如果您熟悉如何使用命令列，您可以透過對執行GET請求，使用以下cURL請求來產生資料集重疊報表 `/previewsamplestatus/report/dataset/overlap`.

**请求**

以下請求使用 `date` 引數以傳回指定日期的最新報告。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| 参数 | 描述 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在該日期執行了多個報表，則會傳回該日期的最新報表。 如果指定日期不存在報表，則會傳回HTTP狀態404 （找不到）錯誤。 如果未指定日期，則會傳回最近的報告。 格式：YYYY-MM-DD。 示例：`date=2024-12-31` |

**响应**

成功的請求會傳回HTTP狀態200 （確定）和資料集重疊報表。 報表包含 `data` 物件，包含以逗號分隔的資料集清單及其各自的設定檔計數。 如需如何閱讀報告的詳細資訊，請參閱以下章節： [解譯資料集重疊報表資料](#interpret-the-report) 在本教學課程的稍後章節中說明。

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-04-19T19:55:31.147"
}
```

### 使用Postman產生資料集重疊報表

Postman是API開發的合作平台，對API呼叫的視覺化相當實用。 您可從以下網址免費下載： [Postman網站](https://www.postman.com) 和提供易於使用的UI來執行API呼叫。 下列熒幕擷取畫面會使用Postman介面。

**请求**

若要使用Postman請求資料集重疊報表，請完成以下步驟：

* 使用下拉式清單，選取GET作為請求型別。
* 在「 」中輸入所需的標頭 `KEY` 欄：
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* 將驗證期間產生的值輸入到 `VALUE` 欄，取代大括弧(`{{ }}`)以及大括弧內的任何內容。
* 輸入請求路徑，無論是否使用選填 `date` 引數：
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   或
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| 参数 | 描述 |
|---|---|
| `date` | 指定要傳回的報表日期。 如果在該日期執行了多個報表，則會傳回該日期的最新報表。 如果指定日期不存在報表，則會傳回HTTP狀態404 （找不到）錯誤。 如果未指定日期，則會傳回最近的報告。 <br/>格式：YYYY-MM-DD。 示例：`date=2024-12-31` |

完成請求型別、標頭、值和路徑後，選取 **傳送** 傳送API要求並產生報表。

![](../images/dataset-overlap-report/postman-request.png)

**响应**

成功的請求會傳回HTTP狀態200 （確定）和資料集重疊報表。 報表包含 `data` 物件，包含以逗號分隔的資料集清單及其各自的設定檔計數。 如需如何閱讀報告的詳細資訊，請參閱以下章節： [解譯資料集重疊報表資料](#interpret-the-report).

![](../images/dataset-overlap-report/postman-response.png)

## 解釋資料集重疊報表資料 {#interpret-the-report}

產生的資料集重疊報表提供顯示報表日期和時間的時間戳記，以及資料物件，其中包含以逗號分隔的清單資料集ID的唯一組合。 以下小節提供有關報表元件的其他資訊。

### 報告時間戳記

此 `reportTimestamp` 符合API請求中提供的日期，如果沒有提供日期，則為最近報表的時間戳記。

### 資料集識別碼清單

此 `data` 物件包括資料集ID的不重複組合，以逗號分隔清單，以及該資料集組合的個別設定檔計數。

>[!NOTE]
>
>與資料集重疊報表每一列相關聯的所有設定檔計數總和，應等於貴組織中的設定檔總數。

若要解譯報表的結果，請考量下列範例：

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

## 后续步骤

完成本教學課程後，您現在可以使用即時客戶設定檔API產生資料集重疊報表。 若要進一步瞭解如何在API和Experience Platform UI中使用設定檔資料，請從閱讀 [設定檔概述檔案](../home.md).

---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；預覽；預估；預覽和預估；預估和預覽；API；
solution: Experience Platform
title: 預覽和預估API端點
description: 開發區段定義時，您可以使用Adobe Experience Platform中的預估和預覽工具來檢視摘要層級的資訊，以協助確保您隔離了預期的受眾。
exl-id: 2c204f29-825f-4a5e-a7f6-40fc69263614
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 2%

---

# 預覽和估計端點

當您開發區段定義時，可以使用Adobe Experience Platform中的預估和預覽工具來檢視摘要層級的資訊，以協助確保您隔離預期的對象。

* **預覽** 提供符合區段定義之設定檔的編頁清單，讓您比較結果與預期。

* **預估** 提供有關區段定義的統計資訊，例如預計對象人數、信賴區間和誤差標準差。

>[!NOTE]
>
>若要存取與即時客戶個人檔案資料相關的類似量度，例如特定名稱空間或整體個人檔案資料存放區中的個人檔案片段和合併個人檔案總數，請參閱 [設定檔預覽（預覽範例狀態）端點指南](../../profile/api/preview-sample-status.md)，設定檔API開發人員指南的一部分。

## 快速入门

本指南中使用的端點是 [!DNL Adobe Experience Platform Segmentation Service] API。 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需成功呼叫API所需的重要資訊，包括必要的標頭及如何讀取範例API呼叫。

## 如何產生預估值

當將記錄擷取至設定檔存放區增加或減少總設定檔計數超過5%時，會觸發取樣工作以更新計數。 資料取樣觸發的方式取決於擷取方法：

* **批次擷取：** 對於批次擷取，在成功將批次擷取到設定檔存放區後15分鐘內，如果符合5%增加或減少臨界值，則會執行工作以更新計數。
* **串流擷取：** 對於串流資料工作流程，會每小時進行一次檢查，以判斷是否符合增加或減少5%的臨界值。 如果有的話，系統會自動觸發工作以更新計數。

掃描的樣本大小取決於設定檔存放區中的實體總數。 這些範例大小如下表所示：

| 設定檔存放區中的實體 | 樣本大小 |
| ------------------------- | ----------- |
| 少於100萬 | 完整資料集 |
| 1到2000萬 | 100萬 |
| 超過2,000萬 | 佔總數的5% |

>[!NOTE]
>
>預估通常需要10到15秒來執行，從粗略的估計開始，並隨著閱讀更多記錄而調整。

## 建立新的預覽 {#create-preview}

您可以透過向以下發出POST請求來建立新的預覽： `/preview` 端點。

>[!NOTE]
>
>建立預覽作業時，會自動建立預估作業。 這兩個工作將共用相同的ID。

**API格式**

```http
POST /preview
```

**请求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
    {
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "none"
    }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `predicateExpression` | 查詢資料所依據的PQL運算式。 |
| `predicateType` | 下方的查詢運算式的述詞型別 `predicateExpression`. 目前，此屬性唯一接受的值是 `pql/text`. |
| `predicateModel` | 的名稱 [!DNL Experience Data Model] 設定檔資料所根據的(XDM)結構描述類別。 |
| `graphType` | 您要從中取得叢集的圖表型別。 支援的值包括 `none` （不執行身分拼接）和 `pdg` （根據您的私人身分圖表執行身分拼接）。 |

**响应**

成功的回應會傳回HTTP狀態201 （已建立）以及新建立預覽的詳細資訊。

```json
{
    "state": "NEW",
    "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
    "previewQueryStatus": "NEW",
    "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
    "previewExecutionId": 0
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `state` | 預覽工作的目前狀態。 最初建立時，它將處於「新」狀態。 接著，處理完成前，它會一直處於「執行中」狀態，到此時會變成「RESULT_READY」或「FAILED」。 |
| `previewId` | 預覽作業的ID，在檢視預估或預覽時用於查詢，如下節所述。 |

## 擷取特定預覽的結果 {#get-preview}

您可以透過向「 」發出GET請求來擷取有關特定預覽的詳細資訊。 `/preview` 端點並在請求路徑中提供預覽ID。

**API格式**

```http
GET /preview/{PREVIEW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 此 `previewId` 要擷取的預覽值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含指定預覽的詳細資訊。

```json
{
   "results": [{
        "XID_ADOBE-MARKETING-CLOUD-ID-1": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1",
            "endCustomerIds": {
                "XID_COOKIE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_1"
                },
                "XID_PROFILE_ID_1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_1"
                }
            }
        }
    },
    {
        "XID_COOKIE-ID-2": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE-ID-2",
            "endCustomerIds": {
                "XID_COOKIE_ID_2-1": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_2-1"

                },
                "XID_PROFILE_ID_2": {
                    "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_2"
                }
            }
        },
        "XID_ADOBE-MARKETING-CLOUD-ID-3": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1000"
        }
    }],
    "state": "RESULT_READY",
    "links": {
        "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
        "next": "",
        "prev": ""
    },
    "page": {
        "offset": 0,
        "size": 3
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `results` | 實體ID及其相關身分的清單。 提供的連結可用於透過以下方式查詢指定的實體： [設定檔存取API端點](../../profile/api/entities.md). |

## 擷取特定估算工作的結果 {#get-estimate}

建立預覽作業後，您可以使用其 `previewId` 在GET請求的路徑中 `/estimate` 端點，以檢視關於區段定義的統計資訊，包括預計對象人數、信賴區間和誤差標準差。

**API格式**

```http
GET /estimate/{PREVIEW_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{PREVIEW_ID}` | 只有在建立預覽作業時，才會觸發預估作業，且兩個作業會共用相同的ID值以進行查詢。 具體來說，這就是 `previewId` 建立預覽作業時傳回的值。 |

**请求**

下列請求會擷取特定估算作業的結果。

```shell
curl -X GET https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態200以及估計工作的詳細資訊。

```json
{
    "estimatedSize": 4275,
    "numRowsToRead": 4275,
    "estimatedNamespaceDistribution": [
        {
            "namespaceId": "4",
            "profilesMatchedSoFar": 35
        },
        {
            "namespaceId": "6",
            "profilesMatchedSoFar": 4275
        }
    ],
    "state": "RESULT_READY",
    "profilesReadSoFar": 4275,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 4275,
    "totalRows": 4275,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview/app-32be0328-3f31-4b64-8d84-acd0c4fbdad3/execution/0?previewQueryId=e890068b-f5ca-4a8f-a6b5-af87ff0caac3"
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `estimatedNamespaceDistribution` | 一個物件陣列，顯示區段內依身分名稱空間劃分的設定檔數目。 依名稱空間區分的設定檔總數（加總針對每個名稱空間顯示的值）可能會高於設定檔計數量度，因為一個設定檔可能會與多個名稱空間建立關聯。 例如，如果客戶在多個頻道上與您的品牌互動，則多個名稱空間會與該個別客戶相關聯。 |
| `state` | 預覽工作的目前狀態。 狀態將為「執行中」，直到處理完成，此時會變成「RESULT_READY」或「FAILED」。 |
| `_links.preview` | 當 `state` 為「RESULT_READY」，此欄位會提供一個URL來檢視預估值。 |

## 后续步骤

閱讀本指南後，您應該更瞭解如何使用分段API來處理預覽和估算。 若要瞭解如何存取與您的即時客戶設定檔資料相關的量度，例如特定名稱空間內的設定檔片段總數和合併的設定檔總數，或是設定檔資料存放區整體，請造訪 [設定檔預覽(`/previewsamplestatus`)端點指南](../../profile/api/preview-sample-status.md).

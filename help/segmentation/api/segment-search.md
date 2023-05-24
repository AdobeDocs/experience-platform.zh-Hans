---
keywords: Experience Platform；細分；細分服務；疑難排解；API；seg；區段；區段；搜尋；區段搜尋；
title: 區段搜尋API端點
description: Adobe Experience Platform Segmentation Service API中，區段搜尋是用來搜尋各種資料來源包含的欄位，並近乎即時地傳回欄位。 本指南提供的資訊可協助您更清楚瞭解區段搜尋，並提供使用API執行基本動作的範例API呼叫。
exl-id: bcafbed7-e4ae-49c0-a8ba-7845d8ad663b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 2%

---

# 區段搜尋端點

區段搜尋可用來搜尋各種資料來源包含的欄位，並近乎即時地傳回這些欄位。

本指南提供的資訊可協助您更清楚瞭解區段搜尋，並提供使用API執行基本動作的範例API呼叫。

## 快速入门

本指南中使用的端點是 [!DNL Adobe Experience Platform Segmentation Service] API。 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需成功呼叫API所需的重要資訊，包括必要的標頭及如何讀取範例API呼叫。

除了快速入門一節中概述的必要標題外，對區段搜尋端點的所有請求都需要以下額外標題：

- x-ups-search-version： &quot;1.0&quot;

### 跨多個名稱空間搜尋

此搜尋端點可用於跨不同名稱空間搜尋，並傳回搜尋計數結果清單。 可使用多個引數，以&amp;分隔。

**API格式**

```http
GET /search/namespaces?schema.name={SCHEMA}
GET /search/namespaces?schema.name={SCHEMA}&s={SEARCH_TERM}
```

| 参数 | 描述 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必要）** 其中{SCHEMA}代表與搜尋物件相關聯的結構描述類別值。 目前，僅限 `_xdm.context.segmentdefinition` 支援。 |
| `s={SEARCH_TERM}` | *（可選）* 其中{SEARCH_TERM}代表符合Microsoft實施的查詢 [Lucene的搜尋語法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). 如果未指定搜尋字詞，則所有與關聯的記錄 `schema.name` 將會傳回。 如需更詳細的說明，請參閱 [附錄](#appendix) 本檔案的所有檔案。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/namespaces?schema.name=_xdm.context.segmentdefinition \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**响应**

成功的回應會傳回HTTP狀態200，並提供下列資訊。

```json
{
  "namespaces": [
    {
      "namespace": "AAMTraits",
      "displayName": "AAMTraits",
      "count": 45
    },
    {
      "namespace": "AAMSegments",
      "displayName": "AAMSegment",
      "count": 10
    },
    {
      "namespace": "SegmentsAISegments",
      "displayName": "SegmentSAISegment",
      "count": 3
    }
  ],
  "totalCount": 3,
  "status": {
    "message": "Success"
  }
}
```

### 搜尋個別實體

此搜尋端點可用於擷取指定名稱空間內所有全文檢索索引物件的清單。 可使用多個引數，以&amp;分隔。

**API格式**

```http
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&s={SEARCH_TERM}
GET /search/entities?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 参数 | 描述 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必要）** 其中{SCHEMA}包含與搜尋物件相關聯的結構描述類別值。 目前，僅限 `_xdm.context.segmentdefinition` 支援。 |
| `namespace={NAMESPACE}` | **（必要）** 其中{NAMESPACE}包含您要搜尋的名稱空間。 |
| `s={SEARCH_TERM}` | *（可選）* 其中{SEARCH_TERM}包含符合Microsoft實施的查詢 [Lucene的搜尋語法](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). 如果未指定搜尋字詞，則所有與關聯的記錄 `schema.name` 將會傳回。 如需更詳細的說明，請參閱 [附錄](#appendix) 本檔案的所有檔案。 |
| `entityId={ENTITY_ID}` | *（可選）* 將搜尋限制在指定的資料夾內（以{ENTITY_ID}指定）。 |
| `limit={LIMIT}` | *（可選）* 其中{LIMIT}代表要傳回的搜尋結果數目。 默认值为 50。 |
| `page={PAGE}` | *（可選）* 其中{PAGE}代表用於分頁搜尋之查詢結果的頁碼。 請注意，頁碼的開頭為 **0**. |


**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/entities?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**响应**

成功的回應會傳回HTTP狀態200，且結果符合搜尋查詢。

```json
{
  "entities": [
    {
       "id": "1012667",
       "base64EncodedSourceId": "RFVGamdydHpEdy01ZTE1ZGJlZGE4YjAxMzE4YWExZWY1MzM1",
       "sourceId": "DUFjgrtzDw-5e15dbeda8b01318aa1ef533",
       "isFolder": true,
       "parentFolderId": "974139",
       "name": "aam-47995 verification (100)"
    },
    {
       "id": "14653311",
       "base64EncodedSourceId": "REVGamduLVgzdy01ZTE2ZjRhNjc1ZDZhMDE4YThhZDM3NmY1",
       "sourceId": "DEFjgn-X3w-5e16f4a675d6a018a8ad376f",
       "isFolder": false,
       "parentFolderId": "324050",
       "name": "AAM - Heavy equipment",
       "description": "AAM - Acme Equipment"
    }
 
 ],
  "page": {
    "totalCount": 2,
    "totalPages": 1,
    "pageOffset": 0,
    "pageSize": 10
  },
  "status": {
    "message": "Success"
  }
}
```

### 取得搜尋物件的結構資訊

此搜尋端點可用於取得請求搜尋物件的結構資訊。

**API格式**

```http
GET /search/taxonomy?schema.name={SCHEMA}&namespace={NAMESPACE}&entityId={ENTITY_ID}
```

| 参数 | 描述 |
| ---------- | ----------- | 
| `schema.name={SCHEMA}` | **（必要）** 其中{SCHEMA}包含與搜尋物件相關聯的結構描述類別值。 目前，僅限 `_xdm.context.segmentdefinition` 支援。 |
| `namespace={NAMESPACE}` | **（必要）** 其中{NAMESPACE}包含您要搜尋的名稱空間。 |
| `entityId={ENTITY_ID}` | **（必要）** 您想要取得結構資訊之搜尋物件的ID，以{ENTITY_ID}指定。 |

**请求**

```shell
curl -X GET \
    https://platform.adobe.io/data/core/ups/search/taxonomy?schema.name=_xdm.context.segmentdefinition&namespace=AAMSegments&entityId=porsche11037 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'Content-Type: application/json' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'x-ups-search-version: 1.0' 
```

**响应**

成功的回應會傳回HTTP狀態200，其中包含請求搜尋物件的詳細結構資訊。

```json
{
    "taxonomy": [
        {
            "id": "0",
            "base64EncodedSourceId": "RFVGZ01BLTVlNjgzMGZjMzk3YjQ1MThhYWExYTA4Zg2",
            "name": "AAMTraits for Cars",
            "parentFolderId": "root"
        },
        {
            "id": "150561",
            "base64EncodedSourceId": "RFVGamdpRk1BZy01ZTY4MzBmYzM5N2I0NTE4YWFhMWEwOGY1",
            "name": "Fast Cars",
            "parentFolderId": "carTraits"
        },
        {
            "id": "porsche11037",
            "base64EncodedSourceId": "REFGZ01CLTVlNjczMGZjMzk3YjQ1MThhZGIxYTA4Zg==",
            "name": "Porsche",
            "parentFolderId": "redCarsFolderId"
        }
    ],
    "status": {
        "message": "Success"
    }
}
```

## 后续步骤

閱讀本指南後，您現在已能更清楚瞭解區段搜尋的運作方式。

## 附录 {#appendix}

以下小節提供有關搜尋詞如何運作的其他資訊。 搜尋查詢的編寫方式如下： `s={FieldName}:{SearchExpression}`. 舉例來說，若要搜尋名為AAM的區段，或是 [!DNL Platform]，您會使用下列搜尋查詢： `s=segmentName:AAM%20OR%20Platform`.

> !![NOTE] 為達到最佳實務，搜尋運算式應使用HTML編碼，如上例所示。

### 搜尋欄位 {#search-fields}

下表列出可在搜尋查詢引數中搜尋的欄位。

| 字段名称 | 描述 |
| ---------- | ----------- |
| folderId | 具有您指定之搜尋的資料夾ID的資料夾。 |
| folderLocation | 具有您指定之搜尋的資料夾位置的一個或多個位置。 |
| parentFolderId | 具有指定搜尋之父資料夾ID的區段或資料夾。 |
| segmentId | 區段符合您指定之搜尋的區段ID。 |
| segmentName | 區段符合您指定搜尋的區段名稱。 |
| segmentDescription | 區段符合您指定之搜尋的區段說明。 |

### 搜尋運算式 {#search-expression}

下表列出使用區段搜尋API時，搜尋查詢運作方式的詳細資訊。

>!![NOTE] 以下範例以非HTML編碼格式顯示，以提供更好的清晰度。 為求最佳實務，請HTML編碼您的搜尋運算式。

| 範例搜尋運算式 | 描述 |
| ------------------------- | ----------- |
| foo | 搜尋任何字詞。 如果在任何可搜尋欄位中找到「foo」一詞，則會傳回結果。 |
| Foo和BAR | 布林值搜尋。 這將傳回結果，如果 **兩者** 字詞「foo」和「bar」可在任何可搜尋欄位中找到。 |
| foo或bar | 布林值搜尋。 這將傳回結果，如果 **兩者之一** 「foo」或「bar」字樣可在任何可搜尋欄位中找到。 |
| foo NOT列 | 布林值搜尋。 如果找到「foo」一詞，但在任何可搜尋欄位中找不到「bar」一詞，則會傳回結果。 |
| 名稱： foo AND列 | 布林值搜尋。 這將傳回結果，如果 **兩者** 在「名稱」欄位中可找到「foo」和「bar」這兩個字。 |
| 執行* | 萬用字元搜尋。 使用星號(*)會符合0或更多字元，這表示如果任何可搜尋欄位的內容包含以「run」開頭的單字，則會傳回結果。 例如，如果出現「runs」、「running」、「runner」或「runt」等字，就會傳回結果。 |
| 凸輪？ | 萬用字元搜尋。 使用問號(？) 只符合一個字元，這表示如果任何可搜尋欄位的內容以「cam」和其他字母開頭，則會傳回結果。 例如，如果出現&quot;camp&quot;或&quot;cams&quot;字詞，這將傳回結果，但如果&quot;camera&quot;或&quot;campfire&quot;字詞出現，將不會傳回結果。 |
| &quot;藍色雨傘&quot; | 片語搜尋。 如果任何可搜尋欄位的內容包含完整的片語「藍色雨傘」，則會傳回結果。 |
| 藍色\~ | 模糊搜尋。 或者，您也可以在波狀符號(~)後面加上一個介於0到2之間的數字，以指定編輯距離。 例如，「blue\~1」會傳回「blue」、「blues」或「glue」。 模糊搜尋可以 **僅限** 套用至辭彙，而非詞句。 不過，您可以在片語中每個字詞的結尾附加波狀符號。 舉例來說，「夏令營」與「夏令營」並不相符。 |
| 「飯店機場」\~5 | 近似程度搜尋。 此搜尋型別用於尋找檔案中彼此接近的字詞。 例如，片語 `"hotel airport"~5` 會在檔案中找到5個字串內分別出現的「hotel」和「airport」字詞。 |
| `/a[0-9]+b$/` | 規則運算式搜尋。 這類搜尋會根據正斜線「/」之間的內容尋找相符專案，如RegExp類別中所述。 例如，若要尋找包含「motel」或「hotel」的檔案，請指定 `/[mh]otel/`. 規則運算式搜尋會根據單一字詞進行比對。 |

如需查詢語法的詳細檔案，請參閱 [Lucene查詢語法檔案](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax).

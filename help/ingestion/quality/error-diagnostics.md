---
keywords: Experience Platform；首頁；熱門主題；批次擷取；批次擷取；部分擷取；擷取錯誤；擷取錯誤；部分批次擷取；部分批次擷取；部分；擷取；擷取；錯誤診斷；擷取錯誤診斷；取得錯誤診斷；取得錯誤；擷取錯誤；
solution: Experience Platform
title: 正在擷取資料擷取錯誤診斷
description: 本檔案提供有關監控批次擷取、管理部分批次擷取錯誤的資訊，以及部分批次擷取型別的參考。
exl-id: b885fb00-b66d-453b-80b7-8821117c2041
source-git-commit: edd285c3d0638b606876c015dffb18309887dfb5
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 2%

---

# 正在擷取資料擷取錯誤診斷

Adobe Experience Platform提供兩種上傳和擷取資料的方法。 您可以使用批次擷取(可讓您使用各種檔案型別（例如CSV）插入資料)或串流擷取（可讓您將其資料插入） [!DNL Platform] 即時使用串流端點。

本檔案提供有關監控批次擷取、管理部分批次擷取錯誤的資訊，以及部分批次擷取型別的參考。

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
- [[!DNL Adobe Experience Platform Data Ingestion]](../home.md)：資料可傳送至的方法 [!DNL Experience Platform].

### 讀取範例API呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括屬於 [!DNL Schema Registry]，會隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

- `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

## 正在下載錯誤診斷 {#download-diagnostics}

Adobe Experience Platform可讓使用者下載輸入檔案的錯誤診斷。 診斷將保留在 [!DNL Platform] 最多30天。

### 列出輸入檔案 {#list-files}

下列請求會擷取已完成批次中提供的所有檔案清單。

**API格式**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 您要查詢之批次的ID。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應將傳回JSON物件，詳細說明診斷的儲存位置。

```json
{
    "_page": {
        "count": 1,
        "limit": 100
    },
    "data": [
        {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json"
                }
            },
            "length": "1337",
            "name": "fileMetaData1.json"
        },
                {
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2}/meta?path=input_files/fileMetaData2.json"
                }
            },
            "length": "1042",
            "name": "fileMetaData2.json"
        }
    ]
}
```

### 擷取輸入檔案診斷 {#retrieve-diagnostics}

擷取所有不同輸入檔案的清單後，您可以使用以下請求來擷取個別檔案的診斷。

**API格式**

```shell
GET /batches/{BATCH_ID}/meta?path=input_files/{FILE}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 您要查詢之批次的ID。 |
| `{FILE}` | 您正在存取的檔案名稱。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/af838510-2233-11ea-acf0-f3edfcded2d2/meta?path=input_files/fileMetaData1.json \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應將傳回包含的JSON物件 `path` 詳細說明診斷儲存位置的物件。 回應會傳回 `path` 中的物件 [JSON行](https://jsonlines.readthedocs.io/en/latest/) 格式。

```json
{"path": "F1.json"}
{"path": "etc/F2.json"}
```

## 擷取批次擷取錯誤 {#retrieve-errors}

如果批次包含失敗，您應該擷取有關這些失敗的錯誤資訊，以便您可以重新擷取資料。

### 檢查狀態 {#check-status}

若要檢查所擷取批次的狀態，您必須在GET請求的路徑中提供批次ID。 若要進一步瞭解如何使用此API呼叫，請閱讀 [目錄端點指南](../../catalog/api/list-objects.md).

**API格式**

```http
GET /catalog/batches/{BATCH_ID}
GET /catalog/batches/{BATCH_ID}?{FILTER}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 此 `id` 要檢查其狀態的批次值。 |
| `{FILTER}` | 用來篩選回應中傳回結果的查詢引數。 多個引數以&amp;符號(`&`)。 如需詳細資訊，請閱讀 [篩選目錄資料](../../catalog/api/filter-data.md). |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/catalog/batches/af838510-2233-11ea-acf0-f3edfcded2d2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**無錯誤回應**

成功回應會傳回批次狀態的詳細資訊。

```json
{
    "af838510-2233-11ea-acf0-f3edfcded2d2": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "externalId": "af838510-2233-11ea-acf0-f3edfcded2d2",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{ORG_ID}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 497,
            "failedRecordCount": 0
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5"
    }    
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `metrics.failedRecordCount` | 由於剖析、轉換或驗證而無法處理的列數。 此值可透過減去 `inputRecordCount` 從 `outputRecordCount`. 此值會在所有批次上產生，無論是否為 `errorDiagnostics` 已啟用。 |

**有錯誤的回應**

如果批次發生一或多個錯誤，且已啟用錯誤診斷，回應會傳回有關錯誤的更多資訊，包括有效負載本身以及可下載的錯誤檔案。 請注意，包含錯誤的批次狀態可能仍具有成功狀態。

```json
{
    "01E8043CY305K2MTV5ANH9G1GC": {
        "status": "success",
        "tags": {
            "acp_enableErrorDiagnostics": true,
            "acp_partialIngestionPercent": 5
        },
        "relatedObjects": [
            {
                "type": "dataSet",
                "id": "5deac2648a19d218a888d2b1"
            }
        ],
        "id": "01E8043CY305K2MTV5ANH9G1GC",
        "externalId": "01E8043CY305K2MTV5ANH9G1GC",
        "inputFormat": {
            "format": "parquet"
        },
        "imsOrg": "{ORG_ID}",
        "started": 1576741718543,
        "metrics": {
            "inputByteSize": 568,
            "inputFileCount": 4,
            "inputRecordCount": 519,
            "outputRecordCount": 514,
            "failedRecordCount": 5
        },
        "completed": 1576741722026,
        "created": 1576741597205,
        "createdClient": "{API_KEY}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1576741722644,
        "version": "1.0.5",
        "errors": [
           {
             "code": "INGEST-1212-400",
             "description": "Encountered 5 errors in the data. Successfully ingested 514 rows. Please review the associated diagnostic files for more details."
           },
           {
             "code": "INGEST-1401-400",
             "description": "The row has corrupted data and cannot be read or parsed. Fix the corrupted data and try again.",
             "recordCount": 2
           },
           {
             "code": "INGEST-1555-400",
             "description": "A required field is either missing or has a value of null. Add the required field to the input row and try again.",
             "recordCount": 3
           }
        ]
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `metrics.failedRecordCount` | 由於剖析、轉換或驗證而無法處理的列數。 此值可透過減去 `inputRecordCount` 從 `outputRecordCount`. 此值會在所有批次上產生，無論是否為 `errorDiagnostics` 已啟用。 |
| `errors.recordCount` | 指定錯誤碼失敗的列數。 此值為 **僅限** 產生條件 `errorDiagnostics` 已啟用。 |

>[!NOTE]
>
>如果無法使用錯誤診斷，則會顯示下列錯誤訊息：
>
```json
>{
>       "errors": [{
>               "code": "INGEST-1211-400",
>               "description": "Encountered errors while parsing, converting or otherwise validating the data. Please resend the data with error diagnostics enabled to collect additional information on failure types"
>       }]
>}
>```

## 后续步骤 {#next-steps}

本教學課程說明如何監控部分批次擷取錯誤。 如需批次擷取的詳細資訊，請閱讀 [批次擷取開發人員指南](../batch-ingestion/api-overview.md).

## 附录 {#appendix}

本節提供有關內嵌錯誤型別的補充資訊。

### 部分批次擷取錯誤型別 {#partial-ingestion-types}

擷取資料時，部分批次擷取有三種不同的錯誤型別：

- [無法讀取的檔案](#unreadable)
- [無效的結構描述或標頭](#schemas-headers)
- [無法剖析的列](#unparsable)

### 無法讀取的檔案 {#unreadable}

如果擷取的批次有無法讀取的檔案，該批次的錯誤將附加到該批次本身。 有關擷取失敗批次的更多資訊，請參閱 [擷取失敗的批次指南](../quality/retrieve-failed-batches.md).

### 無效的結構描述或標頭 {#schemas-headers}

如果擷取的批次具有無效的結構描述或無效的標頭，批次的錯誤將附加在批次本身。 有關擷取失敗批次的更多資訊，請參閱 [擷取失敗的批次指南](../quality/retrieve-failed-batches.md).

### 無法剖析的列 {#unparsable}

如果您擷取的批次有無法剖析的列，您可以使用以下請求來檢視包含錯誤的檔案清單。

**API格式**

```http
GET /export/batches/{BATCH_ID}/meta?path=row_errors
```

| 参数 | 描述 |
| --------- | ----------- |
| `{BATCH_ID}` | 此 `id` 您正在擷取錯誤資訊之批次的值。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回含有錯誤的檔案清單。

```json
{
    "data": [
        {
            "name": "conversion_errors_0.json",
            "length": "1162",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fconversion_errors_0.json"
                }
            }
        },
        {
            "name": "parsing_errors_0.json",
            "length": "153",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/01EFZ7W203PEKSAMVJC3X99VHQ/meta?path=row_errors%2Fparsing_errors_0.json"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 2
    }
}
```

然後，您就可以使用 [診斷擷取端點](#retrieve-diagnostics).

擷取錯誤檔案的範例回應如下所示：

```json
{
    "_corrupt_record": "{missingQuotes: 'v1'}",
    "_errors": [{
        "code": "1401",
        "message": "Row is corrupted and cannot be read, please fix and resend."
    }],
    "_filename": "parsing_errors_0.json"
}
```

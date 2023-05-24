---
keywords: Experience Platform；首頁；熱門主題；擷取失敗的批次；失敗的批次；批次擷取；批次擷取；失敗的批次；取得失敗的批次；取得失敗的批次；下載失敗的批次；下載失敗的批次；
solution: Experience Platform
title: 使用資料存取API擷取失敗的批次
type: Tutorial
description: 本教學課程涵蓋使用資料擷取API擷取失敗批次相關資訊的步驟。
exl-id: 5fb9f28d-091e-4124-8d8e-b8a675938d3a
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 2%

---

# 使用資料存取API擷取失敗的批次

Adobe Experience Platform提供兩種上傳和擷取資料的方法。 您可以使用批次擷取(可讓您使用各種檔案型別（例如CSV）插入其資料)或串流擷取（可讓您將其資料插入） [!DNL Platform] 即時使用串流端點。

本教學課程涵蓋使用擷取失敗批次相關資訊的步驟 [!DNL Data Ingestion] API。

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
- [[!DNL Data Ingestion]](../home.md)：資料可傳送至的方法 [!DNL Experience Platform].

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

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的標頭：

- `Content-Type: application/json`

### 失敗的批次範例

本教學課程將使用具有錯誤格式時間戳記的範例資料，該錯誤時間戳記會將月份值設為 **00**，如下所示：

```json
{
    "body": {
        "xdmEntity": {
            "id": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": "2018-00-10T22:07:56Z",
            "environment": {
                "browserDetails": {
                    "userAgent": "Mozilla\/5.0 (Windows NT 5.1) AppleWebKit\/537.36 (KHTML, like Gecko) Chrome\/29.0.1547.57 Safari\/537.36 OPR\/16.0.1196.62",
                    "acceptLanguage": "en-US",
                    "cookiesEnabled": true,
                    "javaScriptVersion": "1.6",
                    "javaEnabled": true
                },
                "colorDepth": 32,
                "viewportHeight": 799,
                "viewportWidth": 414
            }
        }
    }
}
```

由於格式錯誤的時間戳記，上述裝載將不會針對XDM結構正確驗證。

## 擷取失敗的批次

**API格式**

```http
GET /batches/{BATCH_ID}/failed
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 您要查詢之批次的ID。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{
    "data": [
        {
            "name": "_SUCCESS",
            "length": "0",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=_SUCCESS"
                }
            }
        },
        {
            "name": "part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json",
            "length": "1800",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/batches/{BATCH_ID}/failed?path=part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json"
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

透過上述回應，您可以檢視批次的哪些區塊成功和失敗。 從這個回應中，您可以看到檔案 `part-00000-44c7b669-5e38-43fb-b56c-a0686dabb982-c000.json` 包含失敗的批次。

## 下載失敗的批次

知道批次中的哪個檔案失敗後，您可以下載失敗的檔案並檢視錯誤訊息。

**API格式**

```http
GET /batches/{BATCH_ID}/failed?path={FAILED_FILE}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 包含失敗檔案的批次識別碼。 |
| `{FAILED_FILE}` | 格式設定失敗的檔案名稱。 |

**请求**

以下請求可讓您下載發生內嵌錯誤的檔案。

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/failed?path={FAILED_FILE}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

由於前一個擷取的批次有無效的日期時間，將會顯示以下驗證錯誤。

```json
{
    "_validationErrors": [
        {
            "causingExceptions": [],
            "keyword": "format",
            "message": "[2018-00-23T22:07:01Z] is not a valid date-time. Expected [yyyy-MM-dd'T'HH:mm:ssZ, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1-9}Z, yyyy-MM-dd'T'HH:mm:ss[+-]HH:mm, yyyy-MM-dd'T'HH:mm:ss.[0-9]{1,9}[+-]HH:mm]",
            "pointerToViolation": "#/timestamp",
            "schemaLocation": "#/properties/timestamp"
        }
    ]
}
```

## 后续步骤

閱讀本教學課程後，您已瞭解如何從失敗的批次中擷取錯誤。 如需批次擷取的詳細資訊，請參閱 [批次擷取開發人員指南](../batch-ingestion/overview.md). 如需串流擷取的詳細資訊，請閱讀 [建立串流連線教學課程](../tutorials/create-streaming-connection.md).

## 附录

本節包含可能發生的其他擷取錯誤型別相關資訊。

### XDM格式不正確

如同上一個範例流程中的時間戳記錯誤，這些錯誤是由於XDM的格式不正確。 這些錯誤訊息會因問題性質而異。 因此，無法顯示特定錯誤範例。

### 組織ID遺失或無效

如果承載中缺少組織ID或組織識別碼無效，便會顯示此錯誤。

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has an absent or wrong ims org in the header"
    }
}
```

### 缺少XDM結構描述

如果出現以下情況，則會顯示此錯誤： `schemaRef` 的 `xdmMeta` 遺失。

```json
{
    "type": "http://ns.adobe.com/adobecloud/problem/data-collection-service/inlet",
    "status": 400,
    "title": "Invalid XDM Message Format",
    "report": {
        "message": "inletId: [{INLET_ID}] imsOrgId: [{ORG_ID}@AdobeOrg] Message has unknown xdm format"
    }
}
```

### 缺少來源名稱

如果出現以下情況，則會顯示此錯誤： `source` 標頭中缺少其 `name`.

```json
{
    "_errors":{
        "_streamingValidation": [
            {
                "message": "Payload header is missing Source Name"
            }
        ]
    }
}
```

### 缺少XDM實體

如果沒有其他專案，則會顯示此錯誤 `xdmEntity` 存在。

```json
{
    "_validationErrors": [
        {
            "message": "Payload body is missing xdmEntity"
        }
    ]
}
```

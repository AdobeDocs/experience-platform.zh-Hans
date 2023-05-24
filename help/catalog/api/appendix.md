---
keywords: Experience Platform；首頁；熱門主題；目錄服務；目錄api；附錄
solution: Experience Platform
title: 目錄服務API指南附錄
description: 本檔案包含協助您在Adobe Experience Platform中使用目錄API的其他資訊。
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 1%

---

# [!DNL Catalog Service] API指南附錄

本檔案包含可協助您使用的其他資訊 [!DNL Catalog] API。

## 檢視相互關聯的物件 {#view-interrelated-objects}

部分 [!DNL Catalog] 物件可以與其他物件相互關聯 [!DNL Catalog] 物件。 前置詞為的任何欄位 `@` 回應中裝載表示相關物件。 這些欄位的值採用URI的形式，可用於單獨的GET請求中，以檢索它們表示的相關物件。

檔案傳回的範例資料集，於 [查詢特定資料集](look-up-object.md) 包含 `files` 具有下列URI值的欄位： `"@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"`. 的內容 `files` 欄位可透過使用此URI作為新GET請求的路徑來檢視。

**API格式**

```http
GET {OBJECT_URI}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_URI}` | 相互關聯的物件欄位提供的URI (不包括 `@` 符號)。 |

**请求**

以下請求會使用範例資料集的URI `files` 屬性，可擷取資料集關聯檔案的清單。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回相關物件的清單。 在此範例中，會傳回資料集檔案清單。

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573256315368,
        "updated": 1573256315368
    },
    "148ac690-0280-11ea-8d23-8571a35dce49-1": {
        "id": "148ac690-0280-11ea-8d23-8571a35dce49-1",
        "batchId": "148ac690-0280-11ea-8d23-8571a35dce49",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573255982433,
        "updated": 1573255982433
    },
    "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1": {
        "id": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1",
        "batchId": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## 在單一呼叫中提出多個請求

的根端點 [!DNL Catalog] API允許在單一呼叫中提出多個請求。 請求承載包含物件陣列，代表通常會依序執行的個別請求。

如果這些請求是對的修改或新增 [!DNL Catalog] 而任何一項變更都會失敗，所有變更都會還原。

**API格式**

```http
POST /
```

**请求**

以下請求會建立新的資料集，然後為該資料集建立相關的檢視。 此範例示範如何使用範本語言來存取先前呼叫中傳回的值，以用於後續呼叫。

例如，如果您想要參照從先前的子請求傳回的值，您可以以下列格式建立參照： `<<{REQUEST_ID}.{ATTRIBUTE_NAME}>>` (其中 `{REQUEST_ID}` 是子請求的使用者提供ID （如下所示）。 您可以使用這些範本，參照前一個子請求回應物件內文中的任何可用屬性。

>[!NOTE]
>
>當執行的子請求僅傳回物件的參考時(目錄API中大多數POST和PUT請求的預設值)，此參考將以值的別名顯示 `id` 和可以用作  `<<{OBJECT_ID}.id>>`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    {
      "id": "firstObjectId",
      "resource": "/dataSets",
      "method": "post",
      "body": {
        "type": "raw",
        "name": "First Dataset"
      }
    }, 
    {
      "id": "secondObjectId",
      "resource": "/datasetViews",
      "method": "post",
      "body": {
        "status": "enabled",
        "dataSetId": "<<firstObjectId.id>>"
      }
    }
  ]'
```

| 属性 | 描述 |
| --- | --- |
| `id` | 附加至回應物件的使用者提供的ID，讓您可以將請求與回應比對。 [!DNL Catalog] 不會儲存此值，而只是將其傳回回應以供參考。 |
| `resource` | 相對於根目錄的資源路徑 [!DNL Catalog] API。 通訊協定和網域不應包含在此值中，而且應加上前置詞「/」。 <br/><br/> 使用PATCH或DELETE作為子請求時 `method`，請在資源路徑中包含物件ID。 不要與使用者提供的混淆 `id`，則資源路徑會使用 [!DNL Catalog] 物件本身(例如， `resource: "/dataSets/1234567890"`)。 |
| `method` | 和要求中發生的動作相關的方法名稱(GET、PUT、POST、PATCH或DELETE)。 |
| `body` | 通常作為POST、PUT或PATCH請求中的裝載傳遞的JSON檔案。 GET或DELETE請求不需要此屬性。 |

**响应**

成功的回應會傳回一個物件陣列，其中包含 `id` 您指派給每個請求的HTTP狀態碼、個別請求和回應 `body`. 由於三個範例要求都是要建立新物件， `body` 每個物件的都是一個只包含新建立物件ID的陣列，此為中大多數成功POST回應的標準 [!DNL Catalog].

```json
[
    {
        "id": "firstObjectId",
        "code": 200,
        "body": [
            "@/dataSets/5be230aef5b02914cd52dbfa"
        ]
    },
    {
        "id": "secondObjectId",
        "code": 200,
        "body": [
            "@/dataSetViews/5be230aef5b02914cd52dbfb"
        ]
    }
]
```

檢查多重請求的回應時請務必謹慎，因為您需要驗證每個個別子請求的程式碼，而非僅依賴父POST請求的HTTP狀態程式碼。  單一子請求可能會傳回404 (例如對無效資源的GET請求)，而整體請求會傳回200。

## 其他請求標頭

[!DNL Catalog] 提供數個標題慣例，協助您在更新期間維持資料的完整性。

### If-Match

使用物件版本設定是很好的做法，以防止當多個使用者幾乎同時儲存物件時發生的資料損毀型別。

更新物件時的最佳實務是先進行API呼叫以檢視(GET)要更新的物件。 包含在回應中（以及任何回應包含單一物件的呼叫）是 `E-Tag` 包含物件版本的標頭。 將物件版本新增為名為的請求標頭 `If-Match` 只有在版本仍相同的情況下，更新(PUT或PATCH)呼叫才會導致更新成功，有助於防止資料衝突。

如果版本不符（物件在您擷取之後被其他處理序修改），您將會收到HTTP狀態412 （先決條件失敗），表示存取目標資源已被拒絕。

### Pragma

有時您可能會想要驗證物件而不儲存資訊。 使用 `Pragma` 值為的標頭 `validate-only` 可讓您傳送POST或PUT請求，但僅供驗證之用，以防止保留對資料的任何變更。

## 資料壓縮

壓縮是 [!DNL Experience Platform] 此服務可將小型檔案中的資料合併至大型檔案，而不需變更任何資料。 基於效能考量，將一組小型檔案合併成大型檔案有時會有好處，這樣就能在查詢時更快速地存取資料。

當已壓縮所擷取批次中的檔案時，其相關聯的 [!DNL Catalog] 物件會更新以供監控之用。

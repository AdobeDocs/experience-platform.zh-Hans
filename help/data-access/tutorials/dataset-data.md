---
keywords: Experience Platform；首頁；熱門主題；資料存取；資料存取api；查詢資料存取
solution: Experience Platform
title: 使用資料存取API檢視資料集資料
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform中的資料存取API，尋找、存取和下載儲存在資料集中的資料。 此外，我們也會向您介紹資料存取API的一些獨特功能，例如分頁和部分下載。
exl-id: 1c1e5549-d085-41d5-b2c8-990876000f08
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 3%

---

# 檢視資料集資料，使用 [!DNL Data Access] API

本檔案提供逐步教學課程，說明如何使用，尋找、存取和下載儲存在資料集中的資料。 [!DNL Data Access] Adobe Experience Platform中的API。 此外，我們也會向您介紹 [!DNL Data Access] API，例如分頁和部分下載。

## 快速入门

此教學課程需要深入瞭解如何建立和填入資料集。 請參閱 [資料集建立教學課程](../../catalog/datasets/create.md) 以取得詳細資訊。

以下章節提供您成功呼叫Platform API所需的其他資訊。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：持有人 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的標頭：

- Content-Type： application/json

## 序列圖

本教學課程遵循下列順序圖中所列的步驟，突顯 [!DNL Data Access] API。</br>
![](../images/sequence_diagram.png)

此 [!DNL Catalog] API可讓您擷取有關批次和檔案的資訊。 此 [!DNL Data Access] API可讓您透過HTTP存取及下載這些檔案，作為完整或部分下載，視檔案大小而定。

## 找出資料

開始使用之前 [!DNL Data Access] API的環境中，您必須識別要存取之資料的位置。 在 [!DNL Catalog] API中，有兩個端點可用來瀏覽組織的中繼資料，以及擷取您要存取的批次或檔案的ID：

- `GET /batches`：傳回組織下的批次清單
- `GET /dataSetFiles`：傳回組織下方的檔案清單

如需中端點的完整清單 [!DNL Catalog] API，請參閱 [API參考](https://www.adobe.io/experience-platform-apis/references/catalog/).

## 擷取組織下的批次清單

使用 [!DNL Catalog] api下，您可以傳回組織下的批次清單：

**API格式**

```http
GET /batches
```

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

回應包含列出與組織相關之所有批次的物件，每個頂層值代表批次。 個別批次物件包含該特定批次的詳細資訊。 以下的回應已最小化空間。

```json
{
    "{BATCH_ID_1}": {
        "imsOrg": "{ORG_ID}",
        "created": 1516640135526,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1516640135526,
        "status": "processing",
        "version": "1.0.0",
        "availableDates": {}
    },
    "{BATCH_ID_2}": {
    ...
    }
}
```

### 篩選批次清單

篩選器通常需要尋找特定批次，以擷取特定使用案例的相關資料。 引數可新增至 `GET /batches` 以篩選傳回的回應。 以下請求會傳回特定資料集內指定時間後建立的所有批次，依其建立時間排序。

**API格式**

```http
GET /batches?createdAfter={START_TIMESTAMP}&dataSet={DATASET_ID}&sort={SORT_BY}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{START_TIMESTAMP}` | 以毫秒為單位的開始時間戳記(例如1514836799000)。 |
| `{DATASET_ID}` | 資料集識別碼。 |
| `{SORT_BY}` | 依提供的值排序回應。 例如， `desc:created` 依建立日期遞減排序物件。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1521053542579&dataSet=5cd9146b21dae914b71f654f&orderBy=desc:created' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{   "{BATCH_ID_3}": {
        "imsOrg": "{ORG_ID}",
        "relatedObjects": [
            {
                "id": "5c01a91863540f14cd3d0439",
                "type": "dataSet"
            },
            {
                "id": "00998255b4a148a2bfd4804c2f327324",
                "type": "batch"
            }
        ],
        "status": "success",
        "metrics": {
            "recordsFailed": 0,
            "recordsWritten": 2,
            "startTime": 1550791835809,
            "endTime": 1550791994636
        },
        "errors": [],
        "created": 1550791457173,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1550792060301,
        "version": "1.0.116"
    },
    "{BATCH_ID_4}": {
        "imsOrg": "{ORG_ID}",
        "status": "success",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "00aff31a9ae84a169d69b886cc63c063"
            },
            {
                "type": "dataSet",
                "id": "5bfde8c5905c5a000082857d"
            }
        ],
        "metrics": {
            "startTime": 1544571333876,
            "endTime": 1544571358291,
            "recordsRead": 4,
            "recordsWritten": 4
        },
        "errors": [],
        "created": 1544571077325,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1544571368776,
        "version": "1.0.3"
    }
}
```

引數和篩選器的完整清單可在以下網址找到： [目錄API參考](https://www.adobe.io/experience-platform-apis/references/catalog/).

## 擷取屬於特定批次的所有檔案清單

現在您已擁有要存取之批次的ID，您可以使用 [!DNL Data Access] 用於取得屬於該批次檔案清單的API。

**API格式**

```http
GET /batches/{BATCH_ID}/files
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 您嘗試存取之批次的批次識別碼。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c6f332168966814cd81d3d3/files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{
    "data": [
        {
            "dataSetFileId": "8dcedb36-1cb2-4496-9a38-7b2041114b56-1",
            "dataSetViewId": "5cc6a9b60d4a5914b7940a7f",
            "version": "1.0.0",
            "created": "1558522305708",
            "updated": "1558522305708",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `data._links.self.href` | 存取此檔案的URL。 |

回應包含列出指定批次中所有檔案的資料陣列。 檔案是以其檔案ID參照，該檔案ID可在 `dataSetFileId` 欄位。

## 使用檔案ID存取檔案

擁有唯一的檔案ID後，您就可以使用 [!DNL Data Access] 存取檔案特定詳細資訊的API，包括其名稱、大小（位元組）和下載連結。

**API格式**

```http
GET /files/{FILE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID}` | 您要存取之檔案的識別碼。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

視檔案ID指向個別檔案或目錄而定，傳回的資料陣列可能包含單一專案或屬於該目錄的檔案清單。 每個檔案元素將包含檔案名稱、大小（位元組）和下載檔案的連結等詳細資訊。

**案例1：檔案ID指向單一檔案**

**响应**

```json
{
    "data": [
        {
            "name": "{FILE_NAME}.parquet",
            "length": "249058",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}?path={FILE_NAME_1}.parquet"
                }
            }
        }
    ],
    "_page": {
        "limit": 100,
        "count": 1
    }
}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_NAME}.parquet` | 檔案的名稱。 |
| `_links.self.href` | 下載檔案的URL。 |

**案例2：檔案ID指向目錄**

**响应**

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_2}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267347",
            "updated": "150151267347",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
                }
            }
        },
        {
            "dataSetFileId": "{FILE_ID_3}",
            "dataSetViewId": "460590b01ba38afd1",
            "version": "1.0.0",
            "created": "150151267685",
            "updated": "150151267685",
            "isValid": true,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_3}"
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

| 属性 | 描述 |
| -------- | ----------- | 
| `data._links.self.href` | 下載關聯檔案的URL。 |

此回應會傳回包含兩個個別檔案（具有ID）的目錄 `{FILE_ID_2}` 和 `{FILE_ID_3}`. 在此案例中，您需要遵循每個檔案的URL才能存取該檔案。

## 擷取檔案的中繼資料

您可以發出HEAD要求來擷取檔案的中繼資料。 這會傳回檔案的中繼資料標題，包括其大小（位元組和檔案格式）。

**API格式**

```http
HEAD /files/{FILE_ID}?path={FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID}` | 檔案的識別碼。 |
| `{FILE_NAME}` | 檔案名稱（例如profiles.parquet） |

**请求**

```shell
curl -I 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

回應標頭包含查詢檔案的中繼資料，包括：
- `Content-Length`：指出裝載的大小（以位元組為單位）
- `Content-Type`：指出檔案型別。

## 存取檔案內容

您也可以使用 [!DNL Data Access] API。

**API格式**

```shell
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID}` | 檔案的識別碼。 |
| `{FILE_NAME}` | 檔案名稱（例如profiles.parquet）。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回檔案內容。

## 下載檔案的部分內容

此 [!DNL Data Access] API允許以區塊下載檔案。 範圍標頭可在 `GET /files/{FILE_ID}` 從檔案下載特定位元組範圍的請求。 如果未指定範圍，API預設會下載整個檔案。

中的HEAD範例 [上一節](#retrieve-the-metadata-of-a-file) 會提供特定檔案的大小（位元組）。

**API格式**

```http
GET /files/{FILE_ID}?path={FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID} ` | 檔案的識別碼。 |
| `{FILE_NAME}` | 檔案名稱（例如profiles.parquet） |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/files/8dcedb36-1cb2-4496-9a38-7b2041114b56-1?path=profiles.parquet' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Range: bytes=0-99'
```

| 属性 | 描述 |
| -------- | ----------- | 
| `Range: bytes=0-99` | 指定要下載的位元組範圍。 如果未指定，API會下載整個檔案。 在此範例中，將下載前100個位元組。 |

**响应**

回應內文包含檔案的前100個位元組（如請求中的「Range」標頭所指定）以及HTTP狀態206 （部分內容）。 回應也包含下列標頭：

- Content-Length： 100 （傳回的位元組數）
- Content-type： application/parquet (已要求Parquet檔案，因此回應內容型別為 `parquet`)
- Content-Range：位元組0-99/249058 (要求的範圍(0-99)，位元組總數(249058))

## 設定API回應分頁

內的回應 [!DNL Data Access] API已分頁。 依預設，每頁的專案數上限為100。 分頁引數可用於修改預設行為。

- `limit`：您可以使用「limit」引數，根據需求指定每頁的專案數。
- `start`：位移可由「start」查詢引數設定。
- `&`：您可以使用&amp;符號，在單一呼叫中組合多個引數。

**API格式**

```http
GET /batches/{BATCH_ID}/files?start={OFFSET}
GET /batches/{BATCH_ID}/files?limit={LIMIT}
GET /batches/{BATCH_ID}/files?start={OFFSET}&limit={LIMIT}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 您嘗試存取之批次的批次識別碼。 |
| `{OFFSET}` | 啟動結果陣列的指定索引（例如，start=0） |
| `{LIMIT}` | 控制結果陣列中傳回的結果數量（例如limit=1） |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**:

回應包含 `"data"` 單一元素的陣列，如要求引數所指定 `limit=1`. 此元素是一個物件，包含第一個可用檔案的詳細資訊，如 `start=0` 請求中的引數（請記住，在以零開始的編號中，第一個元素為「0」）。

此 `_links.next.href` 值包含回應下一頁的連結，您可以在此看到 `start` 引數已進階至 `start=1`.

```json
{
    "data": [
        {
            "dataSetFileId": "{FILE_ID_1}",
            "dataSetViewId": "5a9f264c2aa0cf01da4d82fa",
            "version": "1.0.0",
            "created": "1521053793635",
            "updated": "1521053793635",
            "isValid": false,
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
                }
            }
        }
    ],
    "_page": {
        "limit": 1,
        "count": 6
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=1&limit=1"
        },
        "page": {
            "href": "https://platform.adobe.io/data/foundation/export/batches/5c102cac7c7ebc14cd6b098e/files?start=0&limit=1",
            "templated": true
        }
    }
}
```

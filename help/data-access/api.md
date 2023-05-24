---
keywords: Experience Platform；首頁；熱門主題；資料存取；python sdk；spark sdk；資料存取api；匯出；匯出
solution: Experience Platform
title: Data Access API指南
description: 資料存取API為開發人員提供RESTful介面，著重於Experience Platform內擷取資料集的可發現性和可存取性，藉此支援Adobe Experience Platform。
exl-id: 278ec322-dafa-4e3f-ae45-2d20459c5653
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 4%

---

# Data Access API指南

資料存取API透過為使用者提供RESTful介面來支援Adobe Experience Platform，該介面著重於內擷取資料集的可發現性和可存取性 [!DNL Experience Platform].

![Experience Platform上的資料存取](images/Data_Access_Experience_Platform.png)

## API規格參考

Swagger API參考檔案可找到 [此處](https://www.adobe.io/experience-platform-apis/references/data-access/).

## 术语

本檔案中一些常用辭彙的說明。

| 搜索词 | 描述 |
| ----- | ------------ |
| 数据集 | 包含結構和欄位的資料集合。 |
| 批次 | 一段時間內收集並作為單一單位一起處理的一組資料。 |

## 擷取批次中的檔案清單

透過使用批次識別碼(batchID)，資料存取API可以擷取屬於該特定批次的檔案清單。

**API格式**

```http
GET /batches/{BATCH_ID}/files
```

| 属性 | 描述 |
| -------- | ----------- |
| `{BATCH_ID}` | 指定批次的識別碼。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files \
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
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
        }
      }
    },
  ],
  "_page": {
    "limit": 100,
    "count": 1
  }
}
```

此 `"data"` 陣列包含指定批次中所有檔案的清單。 每個傳回的檔案都有自己的唯一ID (`{FILE_ID}`)內含於 `"dataSetFileId"` 欄位。 然後可使用此唯一ID來存取或下載檔案。

| 属性 | 描述 |
| -------- | ----------- |
| `data.dataSetFileId` | 指定批次中每個檔案的檔案識別碼。 |
| `data._links.self.href` | 存取檔案的URL。 |

## 存取和下載批次中的檔案

透過使用檔案識別碼(`{FILE_ID}`)，則資料存取API可用於存取檔案的特定詳細資料，包括其名稱、大小（位元組）和下載連結。

回應將包含資料陣列。 根據ID指向的檔案是個別檔案還是目錄，傳回的資料陣列可能包含單一專案或屬於該目錄的檔案清單。 每個檔案元素都會包含檔案的詳細資訊。

**API格式**

```http
GET /files/{FILE_ID}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID}` | 等於 `"dataSetFileId"`，要存取之檔案的ID。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**單一檔案回應**

```JSON
{
  "data": [
    {
      "name": "{FILE_NAME}",
      "length": "{LENGTH}",
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME}"
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
| `data.name` | 檔案名稱（例如profiles.csv）。 |
| `data.length` | 檔案的大小（以位元組為單位）。 |
| `data._links.self.href` | 下載檔案的URL。 |

**目錄回應**

```JSON
{
  "data": [
    {
      "dataSetFileId": "{FILE_ID_1}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_1}"
        }
      }
    },
    {
      "dataSetFileId": "{FILE_ID_2}",
      "dataSetViewId": "string",
      "version": "1.0.0",
      "created": "string",
      "updated": "string",
      "isValid": true,
      "_links": {
        "self": {
          "href": "https://platform.adobe.io/data/foundation/export/files/{FILE_ID_2}"
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

傳回目錄時，它包含目錄中所有檔案的陣列。

| 属性 | 描述 |
| -------- | ----------- |
| `data.name` | 檔案名稱（例如profiles.csv）。 |
| `data._links.self.href` | 下載檔案的URL。 |

## 存取檔案內容

此 [!DNL Data Access] API也可用來存取檔案的內容。 然後，您便可以使用此項將內容下載至外部來源。

**API格式**

```http
GET /files/{dataSetFileId}?path={FILE_NAME}
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_NAME}` | 您嘗試存取的檔案名稱。 |

**请求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/export/files/{FILE_ID}?path={FILE_NAME} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| 属性 | 描述 |
| -------- | ----------- |
| `{FILE_ID}` | 資料集中檔案的ID。 |
| `{FILE_NAME}` | 檔案的全名（例如profiles.csv）。 |

**响应**

`Contents of the file`

## 其他程式碼範例

如需其他範例，請參閱 [資料存取教學課程](tutorials/dataset-data.md).

## 訂閱資料擷取事件

[!DNL Platform] 讓特定的高價值事件可透過 [Adobe Developer主控台](https://www.adobe.com/go/devs_console_ui). 例如，您可以訂閱資料擷取事件，以接收潛在延遲和失敗的通知。 請參閱教學課程，位置如下： [訂閱資料擷取通知](../ingestion/quality/subscribe-events.md) 以取得詳細資訊。

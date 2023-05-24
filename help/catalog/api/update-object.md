---
keywords: Experience Platform；首頁；熱門主題；目錄；api；更新物件
solution: Experience Platform
title: 更新目錄物件
description: 您可以在PATCH請求的路徑中包含目錄物件的ID來更新其一部分。 本文介紹如何使用欄位和使用JSON修補程式標籤法，對目錄物件執行PATCH作業。
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 3%

---

# 更新目錄物件

您可以更新部分 [!DNL Catalog] 物件，方法是在PATCH請求的路徑中包含其ID。 本文介紹在目錄物件上執行PATCH作業的兩種方法：

* 使用欄位
* 使用JSON修補程式標籤法

>[!NOTE]
>
>物件上的PATCH作業無法修改其可展開的欄位，這些欄位代表相互關聯的物件。 必須直接修改相互關聯的物件。

## 使用欄位更新

以下呼叫範例示範如何使用欄位和值更新物件。

**API格式**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 型別 [!DNL Catalog] 要更新的物件。 有效物件包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 您要更新之特定物件的識別碼。 |

**请求**

以下請求會更新 `name` 和 `description` 資料集的欄位轉換為有效負載中提供的值。 您可從承載中排除不更新的物件欄位。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**响应**

成功的回應會傳回包含已更新資料集ID的陣列。 此ID應與PATCH請求中傳送的ID相符。 針對此資料集執行GET要求時，現在只會顯示 `name` 和 `description` 已更新，而所有其他值維持不變。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## 使用JSON修補程式標籤法更新

以下範例呼叫示範如何使用JSON修補程式更新物件，如中所述 [RFC-6902](https://tools.ietf.org/html/rfc6902).

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**API格式**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 型別 [!DNL Catalog] 要更新的物件。 有效物件包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 您要更新之特定物件的識別碼。 |

**请求**

以下請求會更新 `name` 和 `description` 資料集的欄位對應到每個JSON修補程式物件中提供的值。 使用JSON修補程式時，您也必須將Content-Type標頭設為 `application/json-patch+json`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**响应**

成功的回應會傳回包含更新物件ID的陣列。 此ID應與PATCH請求中傳送的ID相符。 執行此物件的GET要求現在只會顯示 `name` 和 `description` 已更新，而所有其他值維持不變。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

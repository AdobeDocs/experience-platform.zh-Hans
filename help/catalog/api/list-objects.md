---
keywords: Experience Platform；首頁；熱門主題；篩選；篩選；篩選資料；篩選資料
solution: Experience Platform
title: 列出目錄物件
description: 您可以透過單一API呼叫擷取特定型別的所有可用物件清單，最佳實務是加入限制回應大小的篩選器。
exl-id: 2c65e2bc-4ddd-445a-a52d-6ceb1153ccea
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 1%

---

# 列出目錄物件

您可以透過單一API呼叫擷取特定型別的所有可用物件清單，最佳實務是加入限制回應大小的篩選器。

**API格式**

```http
GET /{OBJECT_TYPE}
GET /{OBJECT_TYPE}?{FILTER}={VALUE}&{FILTER_2}={VALUE}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 型別 [!DNL Catalog] 要列出的物件。 有效物件包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{FILTER}` | 用來篩選回應中傳回結果的查詢引數。 多個引數以&amp;符號(`&`)。 請參閱指南： [篩選目錄資料](filter-data.md) 以取得詳細資訊。 |

**请求**

以下範例請求會擷取資料集清單，並附上 `limit` 篩選條件將回應減少為五個結果，以及 `properties` 限制每個資料集所顯示屬性的篩選器。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=5&properties=name,description,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回以下清單： [!DNL Catalog] 索引鍵值配對形式的物件，依請求中提供的查詢引數篩選。 對於每個機碼 — 值組，機碼代表 [!DNL Catalog] 有問題的物件，然後可用於對的其他呼叫 [檢視該特定物件](look-up-object.md) 以取得更多詳細資料。

>[!NOTE]
>
>如果傳回的物件不包含 `properties` 查詢時，回應只會傳回所請求的屬性，如所示 ***`Sample Dataset 3`*** 和 ***`Sample Dataset 4`*** 下方的。

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    },
    "5bda3a4228babc0000126377": {
        "name": "Sample Dataset 4",
        "files": "@/dataSets/5bda3a4228babc0000126377/views/5bda3a4228babc0000126378/files"
    },
    "5bde21511dd27b0000d24e95": {
        "name": "Sample Dataset 5",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bde21511dd27b0000d24e95/views/5bde21511dd27b0000d24e96/files"
    }
}
```

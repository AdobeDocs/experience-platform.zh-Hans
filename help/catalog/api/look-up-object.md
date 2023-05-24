---
keywords: Experience Platform；首頁；熱門主題；目錄；物件查詢；api
solution: Experience Platform
title: 查詢目錄物件
description: 如果您知道特定目錄物件的唯一識別碼，則可以執行GET要求來檢視該物件的詳細資訊。
exl-id: fd6fbe72-0108-4be3-a065-c753e7a19d24
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---

# 查詢目錄物件

如果您知道特定專案的唯一識別碼 [!DNL Catalog] 物件時，您可以執行GET要求來檢視該物件的詳細資訊。

>[!NOTE]
>
>檢視特定物件時，最佳作法仍是 [依屬性篩選](filter-data.md) 並只傳回您感興趣的屬性。

**API格式**

```http
GET /{OBJECT_TYPE}/{OBJECT_ID}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 型別 [!DNL Catalog] 要擷取的物件。 有效物件包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 您要擷取之特定物件的識別碼。 |

**请求**

以下請求會依其ID擷取資料集，並傳回其 `name`， `description`， `state`， `tags`、和 `files` 屬性。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a?properties=name,description,state,tags,files' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回指定的資料集，但只包含要求的資料集 `properties` 內文中的。

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset",
        "description": "Sample dataset containing important data.",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }
}
```

>[!NOTE]
>
>其值前置詞為的屬性 `@` 代表相互關聯的物件。 請參閱附錄中關於 [檢視相互關聯的物件](appendix.md#view-interrelated-objects) 瞭解如何檢視這些物件詳細資訊的步驟。

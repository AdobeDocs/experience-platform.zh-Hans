---
keywords: Experience Platform；首頁；熱門主題；目錄；api；取代物件
solution: Experience Platform
title: 取代目錄物件
description: 您可以使用PUT要求來覆寫目錄物件的內容，其中要求裝載會取代整個資源。
exl-id: cd98d13c-5261-4bff-b5db-af5f06d093c9
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---

# 取代目錄物件

您可以覆寫的 [!DNL Catalog] 使用PUT請求的物件，其中整個資源被替換為請求裝載。

>[!NOTE]
>
>如果您只需要更新中的幾個特定欄位 [!DNL Catalog] 物件，使用PATCH請求可能更有效率。

**API格式**

```http
PUT /{OBJECT_TYPE}/{OBJECT_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 型別 [!DNL Catalog] 要取代的物件。 有效物件包括： <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 您要更新之特定物件的識別碼。 |

**请求**

以下請求會使用承載中提供的值覆寫資料集。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "New Dataset Name",
        "description": "New description for dataset",
        "state": "DRAFT",
        "tags": {
            "adobe/pqs/table": [
                "sample_dataset"
            ]
        },
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    }'
```

**响应**

成功的回應會傳回包含被覆寫物件ID的陣列。 此ID應與PUT請求中傳送的ID相符。 執行此物件的GET要求時，現在會顯示其詳細資訊已被取代為先前PUT要求之裝載中提供的詳細資訊。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

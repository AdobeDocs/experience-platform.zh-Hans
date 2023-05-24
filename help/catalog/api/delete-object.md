---
keywords: Experience Platform；首頁；熱門主題；刪除物件；目錄服務；api
solution: Experience Platform
title: 刪除API中的物件
description: 您可以在DELETE請求的路徑中提供目錄物件的ID，以刪除目錄物件。
exl-id: 2ac9c378-2340-43e1-8279-7c365df652e4
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 1%

---

# 刪除API中的物件

您可以刪除 [!DNL Catalog] 物件，方法是在DELETE請求的路徑中提供其ID。

>[!WARNING]
>
>刪除物件時請格外留意，因為此動作無法復原，且可能在的其他位置產生重大變更。 [!DNL Experience Platform].

**API格式**

```http
DELETE /{OBJECT_TYPE}/{OBJECT_ID}
```

>[!IMPORTANT]
>
>此 `DELETE /batches/{ID}` 端點已過時。 若要刪除批次，您應使用 [批次擷取API](../../ingestion/batch-ingestion/api-overview.md#delete-a-batch).

| 参数 | 描述 |
| --- | --- |
| `{OBJECT_TYPE}` | 型別 [!DNL Catalog] 要刪除的物件。 有效物件包括： <ul><li>`accounts`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | 您要更新之特定物件的識別碼。 |

**请求**

以下請求會刪除在請求路徑中指定ID的資料集。

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態200 （確定）以及包含已刪除資料集ID的陣列。 此ID應與DELETE請求中傳送的ID相符。 對已刪除的物件執行GET要求會傳回HTTP狀態404 （找不到），確認資料集已成功刪除。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

>[!NOTE]
>
>若否 [!DNL Catalog] 物件符合請求中提供的ID，您仍可能會收到HTTP狀態碼200，但回應陣列將是空的。

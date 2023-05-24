---
keywords: Experience Platform；首頁；熱門主題；資料集；資料集；建立資料集；建立資料集；啟用資料集
solution: Experience Platform
title: 在API中建立資料集
description: 本文介紹如何在目錄服務API中建立資料集物件。
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# 在API中建立資料集

為了使用建立資料集 [!DNL Catalog] API，您必須瞭解 `$id` 的值 [!DNL Experience Data Model] 資料集將依據的(XDM)結構描述。 擁有結構描述ID後，您可以透過向以下專案發出POST請求來建立資料集： `/datasets` 中的端點 [!DNL Catalog] API。

>[!NOTE]
>
>本檔案僅說明如何在中建立資料集物件 [!DNL Catalog]. 如需建立、填入及監控資料集的完整步驟，請參閱以下內容 [教學課程](../datasets/create.md).

**API格式**

```HTTP
POST /dataSets
```

**请求**

以下請求會建立參考先前定義之結構描述的資料集。

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 要建立的資料集名稱。 |
| `schemaRef.id` | URI `$id` 資料集將依據的XDM結構描述值。 |
| `schemaRef.contentType` | 表示結構描述的格式和版本。 請參閱以下小節： [結構描述版本設定](../../xdm/api/getting-started.md#versioning) XDM API指南中取得更多資訊。 |

>[!NOTE]
>
>此範例使用 [Apache Parquet](https://parquet.apache.org/docs/) 檔案格式 `containerFormat` 屬性。 以下是使用JSON檔案格式的範例： [批次擷取開發人員指南](../../ingestion/batch-ingestion/api-overview.md).

**响应**

成功的回應會傳回HTTP Status 201 （已建立）和一個回應物件，該回應物件包含一個陣列，其中包含以格式建立的新資料集的ID `"@/datasets/{DATASET_ID}"`. 資料集ID是系統產生的唯讀字串，用來參考API呼叫中的資料集。

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

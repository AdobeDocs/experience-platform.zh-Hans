---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；啟用資料集
title: 使用API啟用設定檔更新的資料集
type: Tutorial
description: 本教學課程說明如何使用Adobe Experience Platform API來啟用具有「更新插入」功能的資料集，以更新即時客戶設定檔資料。
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 1%

---

# 使用API啟用設定檔更新的資料集

本教學課程涵蓋以「更新插入」功能啟用資料集的程式，以更新即時客戶設定檔資料。 這包括建立新資料集和設定現有資料集的步驟。

>[!NOTE]
>
>更新插入工作流程僅適用於批次擷取。 串流擷取是 **not** 支援。

## 快速入门

此教學課程需要您實際瞭解管理已啟用設定檔的資料集所涉及的幾項Adobe Experience Platform服務。 開始進行本教學課程之前，請先檢閱相關檔案 [!DNL Platform] 服務：

- [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
- [[!DNL Catalog Service]](../../catalog/home.md)：RESTful API可讓您建立資料集並設定資料集，用於 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Platform] 組織客戶體驗資料。
- [批次擷取](../../ingestion/batch-ingestion/overview.md)：批次擷取API可讓您將資料以批次檔案的形式擷取到Experience Platform中。

以下章節提供您成功呼叫Platform API所需的其他資訊。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的 `Content-Type` 標頭。 必要時，此標頭的正確值會顯示在範例要求中。

中的所有資源 [!DNL Experience Platform] 隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要 `x-sandbox-name` 標頭，指定將在其中執行作業的沙箱名稱。 如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

## 建立已啟用設定檔更新的資料集

建立新資料集時，您可以為設定檔啟用該資料集，並在建立時啟用更新功能。

>[!NOTE]
>
>若要建立已啟用設定檔的新資料集，您必須知道已為設定檔啟用的現有XDM結構描述的ID。 如需如何查詢或建立已啟用設定檔的結構描述的相關資訊，請參閱以下教學課程： [使用結構描述登入API建立結構描述](../../xdm/tutorials/create-schema-api.md).

若要建立已啟用設定檔和更新的資料集，請使用POST請求 `/dataSets` 端點。

**API格式**

```http
POST /dataSets
```

**请求**

藉由包含兩者 `unifiedIdentity` 和 `unifiedProfile` 在 `tags` 在請求內文中，資料集將啟用 [!DNL Profile] 建立時。 在內 `unifiedProfile` 陣列，新增 `isUpsert:true` 將新增資料集支援更新的功能。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Sample dataset",
        "description: "A sample dataset with a sample description.",
        "fields": [],
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "unifiedIdentity": [
                "enabled: true"
            ],
            "unifiedProfile": [
                "enabled: true",
                "isUpsert: true"
            ]
        }
      }'
```

| 属性 | 描述 |
| -------- | ----------- |
| `schemaRef.id` | 的ID [!DNL Profile] — 啟用的結構描述，資料集將以此為基礎。 |
| `{TENANT_ID}` | 內的名稱空間 [!DNL Schema Registry] ，其中包含屬於您組織的資源。 請參閱 [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) 部分 [!DNL Schema Registry] 開發人員指南，以取得詳細資訊。 |

**响应**

成功的回應會顯示陣列，其中包含新建立資料集的ID，其形式為 `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 設定現有的資料集 {#configure-an-existing-dataset}

下列步驟說明如何設定已啟用設定檔的現有資料集，以更新（更新插入）功能。

>[!NOTE]
>
>若要設定現有已啟用設定檔的資料集以供更新插入，您必須先停用設定檔的資料集，然後隨著 `isUpsert` 標籤之間。 如果設定檔未啟用現有資料集，您可以直接進行以下步驟： [為設定檔和更新插入啟用資料集](#enable-the-dataset). 如果您不確定，以下步驟會說明如何檢查資料集是否已啟用。

### 檢查資料集是否已針對設定檔啟用

使用 [!DNL Catalog] API時，您可以檢查現有資料集以判斷是否已啟用它以用於中 [!DNL Real-Time Customer Profile]. 以下呼叫會依ID擷取資料集的詳細資料。

**API格式**

```http
GET /dataSets/{DATASET_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | 您要檢查的資料集ID。 |

**请求**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "{DATASET_NAME}",
        "imsOrg": "{ORG_ID}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ],
            "unifiedProfile": [
                "enabled:true"
            ]
        },
        "lastBatchId": "{BATCH_ID}",
        "lastBatchStatus": "success",
        "dule": {},
        "statsCache": {
            "startDate": null,
            "endDate": null
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "{VIEW_ID}",
        "status": "enabled",
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "{SCHEMA}",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

在 `tags` 屬性，您會看到 `unifiedProfile` 與值同時存在 `enabled:true`. 因此， [!DNL Real-Time Customer Profile] 已針對此資料集啟用。

### 停用設定檔的資料集

若要設定已啟用設定檔的資料集以進行更新，您必須先停用 `unifiedProfile` 和 `unifiedIdentity` 標籤，然後在標籤旁重新啟用 `isUpsert` 標籤之間。 這是使用兩個PATCH請求來完成，一次為停用，另一次為重新啟用。

>[!WARNING]
>
>在停用時擷取到資料集中的資料將不會擷取到設定檔存放區。 在為設定檔重新啟用資料集之前，您應該避免將資料擷取到資料集中。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | 您要更新的資料集ID。 |

**请求**

第一個PATCH請求內文包含 `path` 至 `unifiedProfile` 和 `path` 至 `unifiedIdentity`，設定 `value` 至 `enabled:false` 以停用標籤。

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "replace", 
            "path": "/tags/unifiedProfile", 
            "value": ["enabled:false"] 
        },
        {
            "op": "replace",
            "path": "/tags/unifiedIdentity",
            "value": ["enabled:false"]
        }
      ]'
```

**响应**

成功的PATCH要求會傳回HTTP狀態200 （確定）以及包含已更新資料集ID的陣列。 此ID應與PATCH請求中傳送的ID相符。 此 `unifiedProfile` 和 `unifiedIdentity` 標籤現已停用。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### 為設定檔和更新插入啟用資料集 {#enable-the-dataset}

您可使用單一PATCH請求，為現有的資料集啟用設定檔和屬性更新。

>[!IMPORTANT]
>
>為設定檔啟用資料集時，請確保與資料集相關聯的結構描述為 **另外** 已啟用設定檔。 如果結構描述未啟用設定檔，資料集將 **not** 在Platform UI中顯示為已啟用設定檔。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{DATASET_ID}` | 您要更新的資料集ID。 |

**请求**

請求內文包含 `path` 至 `unifiedProfile` 設定 `value` 以包含 `enabled` 和 `isUpsert` 標籤，均設為 `true`，和 `path` 至 `unifiedIdentity` 設定 `value` 以包含 `enabled` 標籤已設定為 `true`.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "add", 
            "path": "/tags/unifiedProfile", 
            "value": [
                "enabled:true",
                "isUpsert:true"
            ] 
        },
        {
            "op": "add",
            "path": "/tags/unifiedIdentity",
            "value": [
                "enabled:true"
            ]
        }
      ]'
```

**响应**

成功的PATCH要求會傳回HTTP狀態200 （確定）以及包含已更新資料集ID的陣列。 此ID應與PATCH請求中傳送的ID相符。 此 `unifiedProfile` 標籤和 `unifiedIdentity` 標籤現在已啟用並設定屬性更新。

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 后续步骤

批次擷取工作流程現在可以使用您的設定檔和已啟用更新插入的資料集，來更新設定檔資料。 若要進一步瞭解如何將資料擷取至Adobe Experience Platform，請先閱讀 [資料擷取概觀](../../ingestion/home.md).

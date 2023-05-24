---
keywords: Experience Platform；首頁；熱門主題；資料集api；管理資料使用；資料使用api
solution: Experience Platform
title: 使用API管理資料集的資料使用標籤
description: 資料集服務API可讓您套用和編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集中繼資料的目錄服務API不同。
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 1%

---

# 使用API管理資料集的資料使用標籤

此 [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) 可讓您套用及編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與 [!DNL Catalog Service] 管理資料集中繼資料的API。

>[!IMPORTANT]
>
>僅資料控管使用案例支援在資料集層級套用標籤。 如果您嘗試建立資料的存取原則，您必須 [將標籤套用至結構描述](../../xdm/tutorials/labels.md) 資料集所根據的。 請參閱以下文章的概觀： [基於屬性的存取控制](../../access-control/abac/overview.md) 以取得詳細資訊。

本檔案說明如何使用管理資料集和欄位的標籤 [!DNL Dataset Service API]. 如需如何使用API呼叫管理資料使用標籤本身的步驟，請參閱 [標籤端點指南](../api/labels.md) 的 [!DNL Policy Service API].

## 快速入门

在閱讀本指南之前，請遵循以下說明的步驟： [快速入門區段](../../catalog/api/getting-started.md) 目錄開發人員指南中的，以收集必要的認證來呼叫 [!DNL Platform] API。

若要呼叫本檔案中概述的端點，您必須擁有唯一的 `id` 特定資料集的值。 如果您沒有此值，請參閱指南，位置為 [列出目錄物件](../../catalog/api/list-objects.md) 以尋找現有資料集的ID。

## 查詢資料集的標籤 {#look-up}

您可以透過向「 」發出GET請求，查詢已套用至現有資料集的資料使用標籤。 [!DNL Dataset Service] API。

**API格式**

```http
GET /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 唯一 `id` 您要查詢其標籤的資料集值。 |

**请求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回已套用至資料集的資料使用標籤。

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{ORG_ID}",
    "labels": [ "C1", "C2", "C3", "I1", "I2" ],
    "optionalLabels": [
      {
        "option": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
          "contentType": "application/vnd.adobe.xed-full+json;version=1",
          "schemaPath": "/properties/repositoryCreatedBy"
        },
        "labels": [ "S1", "S2" ]
      }
    ]
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `labels` | 已套用至資料集的資料使用標籤清單。 |
| `optionalLabels` | 資料集中已套用資料使用標籤的個別欄位清單。 |

## 將標籤套用至資料集 {#apply}

您可以透過在POST或PUT請求的裝載中提供資料集，為資料集建立一組標籤。 [!DNL Dataset Service] API。 使用其中一個方法會覆寫任何現有標籤，並以承載中提供的標籤取代。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 唯一 `id` 您正在建立標籤的資料集值。 |

**请求**

以下範例PUT請求會更新資料集的現有標籤，以及該資料集內的特定欄位。 承載中提供的欄位與POST請求所需的欄位相同。

進行API呼叫以更新資料集(PUT)的現有標籤時， `If-Match` 必須包含標頭，指出資料集服務中資料集 — 標籤實體的目前版本。 為避免資料衝突，服務將只更新資料集實體（如果包含） `If-Match` 字串符合系統為該資料集產生的最新版本標籤。

>[!NOTE]
>
>如果相關資料集目前沒有標籤，則只能透過POST請求新增新標籤，不需要新增標籤。 `If-Match` 標頭。 標籤新增至資料集後， `etag` 會指派值，以便稍後用來更新或移除標籤。

若要擷取最新版本的資料集 — 標籤實體，請建立 [GET要求](#look-up) 至 `/datasets/{DATASET_ID}/labels` 端點。 目前的值會傳回至下方的回應中 `etag` 標頭。 更新現有資料集標籤時，最佳實務是先執行資料集的查詢請求，以擷取其最新資料 `etag` 值之前，在下列位置使用該值： `If-Match` 後續PUT請求的標頭。

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000' \
  -d '{
        "labels": [ "C1", "C2", "C3", "I1", "I2" ],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/repositoryCreatedBy"
            },
            "labels": [ "S1", "S2" ]
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `labels` | 您要新增至資料集的資料使用標籤清單。 |
| `optionalLabels` | 資料集中您要新增標籤的任何個別欄位清單。 此陣列中的每個專案都必須具備下列屬性： <br/><br/>`option`：一個物件，包含 [!DNL Experience Data Model] 欄位的(XDM)屬性。 需要下列三個屬性：<ul><li>id</code>： URI $id</code> 與欄位關聯的結構描述值。</li><li>內容型別</code>：結構描述的內容型別和版本號碼。 這應該採用其中一種有效形式 <a href="../../xdm/api/getting-started.md#accept">接受標頭</a> XDM查詢請求的。</li><li>結構描述路徑</code>：資料集結構描述中欄位的路徑。</li></ul>`labels`：您要新增至欄位的資料使用標籤清單。 |

**响应**

成功的回應會傳回資料集的更新標籤集。

```json
{
  "labels": [ "C1", "C2", "C3", "I1", "I2" ],
  "optionalLabels": [
    {
      "option": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
        "contentType": "application/vnd.adobe.xed-full+json;version=1",
        "schemaPath": "/properties/repositoryCreatedBy"
      },
      "labels": [ "S1", "S2" ]
    }
  ]
}
```

## 后续步骤

閱讀本檔案後，您已瞭解如何使用 [!DNL Dataset Service] API。 您現在可以定義 [資料使用原則](../policies/overview.md) 和 [存取控制原則](../../access-control/abac/ui/policies.md) 根據您已套用的標籤。

如需中管理資料集的詳細資訊 [!DNL Experience Platform]，請參閱 [資料集總覽](../../catalog/datasets/overview.md).

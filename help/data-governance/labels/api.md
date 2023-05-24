---
keywords: Experience Platform；首頁；熱門主題；資料控管；資料使用標籤api；原則服務api
solution: Experience Platform
title: 使用API管理資料使用標籤
description: 資料集服務API可讓您套用和編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集中繼資料的目錄服務API不同。
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 2%

---


# 使用API管理資料使用標籤

本檔案提供如何使用管理資料使用標籤的步驟。 [!DNL Policy Service] API和 [!DNL Dataset Service] API。

此 [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) 提供數個端點，可讓您建立和管理組織的資料使用標籤。

此 [!DNL Dataset Service] API可讓您套用和編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與 [!DNL Catalog Service] 管理資料集中繼資料的API。

## 快速入门

在閱讀本指南之前，請遵循以下說明的步驟： [快速入門區段](../../catalog/api/getting-started.md) 目錄開發人員指南中的，以收集必要的認證來呼叫 [!DNL Platform] API。

為了呼叫 [!DNL Dataset Service] 此檔案中概述的端點，您必須具有 `id` 特定資料集的值。 如果您沒有此值，請參閱指南，位置為 [列出目錄物件](../../catalog/api/list-objects.md) 以尋找現有資料集的ID。

## 列出所有標籤 {#list-labels}

使用 [!DNL Policy Service] API，您可以列出所有 `core` 或 `custom` 向發出GET請求以貼上標籤 `/labels/core` 或 `/labels/custom`（分別）。

**API格式**

```http
GET /labels/core
GET /labels/custom
```

**请求**

以下請求列出在您組織下建立的所有自訂標籤。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回從系統擷取的自訂標籤清單。 由於上述範例請求是向 `/labels/custom`，以下的回應只會顯示自訂標籤。

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## 查詢標籤 {#look-up-label}

您可以包含特定標籤的 `name` 的GET請求路徑中的屬性 [!DNL Policy Service] API。

**API格式**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{LABEL_NAME}` | 此 `name` 要查閱的自訂標籤的屬性。 |

**请求**

以下請求會擷取自訂標籤 `L2`，如路徑中所示。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功回應會傳回自訂標籤的詳細資料。

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{ORG_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## 建立或更新自訂標籤 {#create-update-label}

若要建立或更新自訂標籤，您必須向以下專案發出PUT請求： [!DNL Policy Service] API。

**API格式**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{LABEL_NAME}` | 此 `name` 自訂標籤的屬性。 如果此名稱的自訂標籤不存在，則會建立新標籤。 如果存在，則會更新該標籤。 |

**请求**

以下請求會建立新標籤， `L3`，旨在說明內含客戶選定付款計畫相關資訊的資料。

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 標籤的唯一字串識別碼。 此值用於查詢目的，並將標籤套用至資料集和欄位，因此建議它簡短明瞭。 |
| `category` | 標籤的類別。 雖然您可以建立自己的自訂標籤類別，但強烈建議您使用 `Custom` 是否希望標籤顯示在UI中。 |
| `friendlyName` | 標籤的易記名稱，用於顯示用途。 |
| `description` | （選用）提供進一步內容的標籤說明。 |

**响应**

成功的回應會傳回自訂標籤的詳細資料，如果更新了現有標籤，則傳回HTTP代碼為200 （確定），如果建立了新標籤，則傳回201 （建立）。

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{ORG_ID}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## 查詢資料集的標籤 {#look-up-dataset-labels}

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
| `optionalLabels` | 資料集中已套用資料使用標籤的個別欄位清單。 需要下列子屬性：<br/><br/>`option`：一個物件，包含 [!DNL Experience Data Model] 欄位的(XDM)屬性。 需要下列三個屬性：<ul><li>`id`：URI `$id` 與欄位關聯的結構描述值。</li><li>`contentType`：指出結構描述的格式和版本。 請參閱以下小節： [結構描述版本設定](../../xdm/api/getting-started.md#versioning) XDM API指南中取得更多資訊。</li><li>`schemaPath`：相關結構描述屬性的路徑，寫入於 [JSON指標](../../landing/api-fundamentals.md#json-pointer) 語法。</li></ul>`labels`：您要新增至欄位的資料使用標籤清單。 |

- id：資料集所根據之XDM結構描述的URI $id值。
- contentType：指出結構描述的格式和版本。 請參閱以下小節： [結構描述版本設定](../../xdm/api/getting-started.md#versioning) XDM API指南中取得更多資訊。
- schemaPath：有問題的結構描述屬性的路徑，寫入 [JSON指標](../../landing/api-fundamentals.md#json-pointer) 語法。

## 將標籤套用至資料集 {#apply-dataset-labels}

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

以下POST請求會將一系列標籤新增至資料集，以及該資料集內的特定欄位。 承載中提供的欄位與PUT請求所需的欄位相同。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
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
| `optionalLabels` | 資料集中您要新增標籤的任何個別欄位清單。 此陣列中的每個專案都必須具備下列屬性：<br/><br/>`option`：一個物件，包含 [!DNL Experience Data Model] 欄位的(XDM)屬性。 需要下列三個屬性：<ul><li>`id`：URI `$id` 與欄位關聯的結構描述值。</li><li>`contentType`：指出結構描述的格式和版本。 請參閱以下小節： [結構描述版本設定](../../xdm/api/getting-started.md#versioning) XDM API指南中取得更多資訊。</li><li>`schemaPath`：相關結構描述屬性的路徑，寫入於 [JSON指標](../../landing/api-fundamentals.md#json-pointer) 語法。</li></ul>`labels`：您要新增至欄位的資料使用標籤清單。 |

**响应**

成功的回應會傳回已新增至資料集的標籤。

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

## 從資料集中移除標籤 {#remove-dataset-labels}

您可以透過向以下專案發出DELETE請求，移除套用至資料集的標籤： [!DNL Dataset Service] API。

**API格式**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 参数 | 描述 |
| --- | --- |
| `{DATASET_ID}` | 唯一 `id` 您要移除其標籤之資料集的值。 |

**请求**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應HTTP狀態200 （確定），表示標籤已移除。 您可以 [查詢現有標籤](#look-up-dataset-labels) 在另一個呼叫中用於資料集以確認此情況。

## 后续步骤

閱讀本檔案後，您已瞭解如何使用API管理資料使用標籤。

在資料集和欄位層級新增資料使用標籤後，您就可以開始將資料擷取到 [!DNL Experience Platform]. 若要深入瞭解，請先閱讀 [資料擷取檔案](../../ingestion/home.md).

您現在也可以根據已套用的標籤來定義資料使用原則。 如需詳細資訊，請參閱 [資料使用原則概觀](../policies/overview.md).

如需中管理資料集的詳細資訊 [!DNL Experience Platform]，請參閱 [資料集總覽](../../catalog/datasets/overview.md).
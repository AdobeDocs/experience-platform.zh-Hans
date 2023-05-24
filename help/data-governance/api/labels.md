---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 標籤API端點
description: 瞭解如何使用原則服務API管理Experience Platform中的資料使用標籤。
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 3%

---

# 標籤端點

資料使用標籤可讓您根據可能適用於該資料的使用原則來分類資料。 此 `/labels` 中的端點 [!DNL Policy Service API] 可讓您以程式設計方式管理體驗應用程式內的資料使用標籤。

>[!NOTE]
>
>此 `/labels` 端點僅用於擷取、建立和更新資料使用標籤。 如需如何使用API呼叫將標籤新增至資料集和欄位的步驟，請參閱以下指南中的 [管理資料集標籤](../labels/dataset-api.md).

## 快速入门

本指南中使用的API端點是 [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/). 在繼續之前，請檢閱 [快速入門手冊](getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功對任一檔案發出呼叫所需必要標題的重要資訊 [!DNL Experience Platform] API。

## 擷取標籤清單 {#list}

您可以列出所有 `core` 或 `custom` 向發出GET請求以貼上標籤 `/labels/core` 或 `/labels/custom`（分別）。

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

## 查詢標籤 {#look-up}

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

## 建立或更新自訂標籤 {#create-update}

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

## 后续步骤

本指南涵蓋 `/labels` 原則服務API中的端點。 如需如何將標籤套用至資料集和欄位的步驟，請參閱 [資料集標籤API指南](../labels/dataset-api.md).

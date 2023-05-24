---
keywords: Experience Platform；首頁；熱門主題；原則執行；行銷動作api；API型執行；資料控管
solution: Experience Platform
title: 行銷動作API端點
description: 在Adobe Experience Platform資料控管的內容中，行銷動作是Experience Platform資料消費者採取的動作，需要檢查其是否違反資料使用原則。
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 2%

---

# 行銷動作端點

在Adobe Experience Platform資料控管的內容中，行銷動作是指 [!DNL Experience Platform] 資料取用者需要檢查資料使用原則是否違規。

您可以使用管理組織的行銷動作 `/marketingActions` 原則服務API中的端點。

## 快速入门

本指南中使用的API端點屬於 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功對任一檔案發出呼叫所需必要標題的重要資訊 [!DNL Experience Platform] API。

## 擷取行銷動作清單 {#list}

您可以透過向以下發出GET請求，擷取核心或自訂行銷動作清單： `/marketingActions/core` 或 `/marketingActions/custom`（分別）。

**API格式**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**请求**

以下請求會擷取貴組織維護的自訂行銷動作清單。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回每個已擷取行銷動作的詳細資訊，包括其 `name` 和 `href`. 此 `href` 值用於識別行銷動作，當 [建立資料使用原則](policies.md#create-policy).

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{ORG_ID}",
            "created": 1550714012088,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714012088,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{ORG_ID}",
            "created": 1550793833224,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550793833224,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| 属性 | 描述 |
| --- | --- |
| `_page.count` | 傳回的行銷動作總數。 |
| `children` | 一個物件陣列，其中包含已擷取行銷動作的詳細資訊。 |
| `name` | 行銷動作的名稱，在下列情況下當作其唯一識別碼： [查詢特定行銷動作](#lookup). |
| `_links.self.href` | 行銷動作的URI參考，可用來完成 `marketingActionsRefs` 陣列時間 [建立資料使用原則](policies.md#create-policy). |

## 查詢特定的行銷動作 {#lookup}

您可以包含行銷動作的，以查詢特定行銷動作的詳細資訊 `name` GET要求路徑中的屬性。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 此 `name` 您要查閱之行銷動作的屬性。 |

**请求**

以下請求會擷取名為的自訂行銷動作 `combineData`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

回應物件包含行銷動作的詳細資訊，包括路徑(`_links.self.href`)時參考行銷動作所需 [定義資料使用原則](policies.md#create-policy) (`marketingActionsRefs`)。

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{ORG_ID}",
    "created": 1550793805590,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550793805590,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
        }
    }
}
```

## 建立或更新自訂行銷動作 {#create-update}

您可以建立新的自訂行銷動作，或更新現有的行銷動作，方法是在PUT請求的路徑中包含行銷動作的現有名稱或預期名稱。

**API格式**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要建立或更新之行銷動作的名稱。 如果系統中已存在具有所提供名稱的行銷動作，則會更新該行銷動作。 如果不存在，則會針對提供的名稱建立新的行銷動作。 |

**请求**

以下請求會建立名為的新行銷動作 `crossSiteTargeting`，前提是系統中不存在相同名稱的行銷動作。 若為 `crossSiteTargeting` 行銷動作確實存在，此呼叫會根據裝載中提供的屬性更新行銷動作。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| 属性 | 描述 |
| --- | --- |
| `name` | 要建立或更新之行銷動作的名稱。 <br><br>**重要**：此屬性必須與 `{MARKETING_ACTION_NAME}` 路徑中，否則會發生HTTP 400 （錯誤請求）錯誤。 換言之，建立行銷動作後， `name` 屬性無法變更。 |
| `description` | 選用的說明，可提供行銷動作的進一步內容。 |

**响应**

成功的回應會傳回行銷動作的詳細資訊。 如果更新了現有的行銷動作，回應會傳回HTTP狀態200 （確定）。 如果已建立新的行銷動作，回應會傳回HTTP狀態201 （已建立）。

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{ORG_ID}",
    "created": 1550713341915,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550713856390,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
        }
    }
}
```

## 刪除自訂行銷動作 {#delete}

您可以在DELETE請求的路徑中包含自訂行銷動作的名稱，以刪除自訂行銷動作。

>[!NOTE]
>
>無法刪除現有原則所參考的行銷動作。 嘗試刪除其中一個行銷動作將導致HTTP 400 （錯誤請求）錯誤以及包含引用行銷動作之所有原則ID的訊息。

**API格式**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 参数 | 描述 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 您要刪除的行銷動作名稱。 |

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態200 （確定），並帶有空白回應內文。

您可以嘗試確認刪除 [查詢行銷動作](#look-up). 如果行銷動作已從系統中移除，您應該會收到HTTP 404 （找不到）錯誤。

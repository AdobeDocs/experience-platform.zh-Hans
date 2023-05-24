---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述登入；結構描述登入；
solution: Experience Platform
title: 開始使用結構描述登入API
description: 本檔案會介紹您在嘗試呼叫Schema Registry API之前需要瞭解的核心概念。
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 0%

---

# 開始使用 [!DNL Schema Registry] API

此 [!DNL Schema Registry] API可讓您建立和管理各種Experience Data Model (XDM)資源。 本檔案會介紹您在嘗試呼叫「 」之前需要瞭解的核心概念。 [!DNL Schema Registry] API。

## 先决条件

使用開發人員指南需要深入瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM) System]](../home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../schema/composition.md)：瞭解XDM結構描述的基本建置組塊。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

XDM使用JSON結構描述格式來說明和驗證所擷取客戶體驗資料的結構。 因此，強烈建議您檢閱 [官方JSON結構描述檔案](https://json-schema.org/) 以進一步瞭解這項基礎技術。

## 讀取範例API呼叫

此 [!DNL Schema Registry] API檔案提供範例API呼叫，示範如何格式化請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑難排解指南中。

## 收集必要標題的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括屬於 [!DNL Schema Registry]，會隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱檔案](../../sandboxes/home.md).

對的所有查詢(GET)請求 [!DNL Schema Registry] 需要額外的 `Accept` 標頭，其值會決定API傳回的資訊格式。 請參閱 [接受標頭](#accept) 區段以取得更多詳細資訊。

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的標頭：

* `Content-Type: application/json`

## 知道您的TENANT_ID {#know-your-tenant_id}

在API指南中，您會看到 `TENANT_ID`. 此ID可用來確保您建立的資源能正確建立名稱空間，並包含在您的組織內。 如果您不知道您的ID，可以透過執行以下GET請求來存取它：

**API格式**

```http
GET /stats
```

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回有關貴組織使用的資訊 [!DNL Schema Registry]. 這包括 `tenantId` 屬性，其值是您的 `TENANT_ID`.

```JSON
{
  "imsOrg":"{ORG_ID}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "mixins": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "mixins",
      "meta:created": "Sat Feb 02 2019 00:24:30 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/5bdb5582be0c0f3ebfc1c603b705764f",
      "title": "Tenant Class",
      "description": "Tenant Defined Class",
      "meta:resourceType": "classes",
      "meta:created": "Fri Feb 01 2019 22:46:21 GMT+0000 (UTC)",
      "version": "1.0"
    } 
  ],
  "recentlyUpdatedResources": [
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "mixins",
      "meta:updated": "Sat Feb 02 2019 00:34:06 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "title": "Data Schema",
      "description": "Schema for Data Information",
      "meta:resourceType": "schemas",
      "meta:updated": "Fri Feb 01 2019 23:47:43 GMT+0000 (UTC)",
      "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab",
      "meta:classTitle": "Sample Class",
      "version": "1.1"
    }
 ],
 "classUsage": {
    "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "title": "Tenant Data Schema",
        "description": "Schema for tenant-specific data."
      }
    ],
    "https://ns.adobe.com/xdm/context/profile": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/3ac6499f0a43618bba6b138226ae3542",
        "title": "Simple Profile",
        "description": "A simple profile schema."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "title": "Program Schema",
        "description": "Schema for program-related data."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/4025a705890c6d4a4a06b16f8cf6f4ca",
        "title": "Sample Schema",
        "description": "A sample schema."
      }
    ]
  }
 }
```

## 瞭解 `CONTAINER_ID` {#container}

呼叫 [!DNL Schema Registry] API需要使用 `CONTAINER_ID`. 可以針對兩個容器進行API呼叫： `global` 容器和 `tenant` 容器。

### 全域容器

此 `global` 容器包含所有標準Adobe和 [!DNL Experience Platform] 合作夥伴提供的類別、結構描述欄位群組、資料型別和結構描述。 您只能對以下專案執行清單和查詢(GET)請求： `global` 容器。

使用 `global` 容器看起來像這樣：

```http
GET /global/classes
```

### 租使用者容器

不要與您的獨特之處混淆 `TENANT_ID`，則 `tenant` container包含組織定義的所有類別、欄位群組、資料型別、結構描述和描述項。 這些內容對每個組織都是獨一無二的，這表示其他組織無法看到或管理這些內容。 您可以針對在中建立的資源執行所有CRUD作業(GET、POST、PUT、PATCH、DELETE)。 `tenant` 容器。

使用 `tenant` 容器看起來像這樣：

```http
POST /tenant/fieldgroups
```

當您在中建立類別、欄位群組、結構或資料型別時 `tenant` 容器，則會儲存至 [!DNL Schema Registry] 並指派 `$id` 包含您的 `TENANT_ID`. 此 `$id` 在整個API中使用來參考特定資源。 範例： `$id` 值會在下一節中提供。

## 資源識別 {#resource-identification}

XDM資源以 `$id` URI形式的屬性，例如以下範例：

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

為了讓URI更適合REST，結構描述在名為的屬性中也有對URI進行點標籤法編碼 `meta:altId`：

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

呼叫 [!DNL Schema Registry] API將支援URL編碼的 `$id` URI或 `meta:altId` （點標籤法格式）。 最佳實務為使用URL編碼 `$id` 對API進行REST呼叫時的URI，如下所示：

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## 接受標頭 {#accept}

在中執行清單和查詢(GET)作業時 [!DNL Schema Registry] API、和 `Accept` 需要標題來決定API傳回的資料格式。 查詢特定資源時，版本號碼也必須包含在 `Accept` 標頭。

下表列出相容專案 `Accept` 標頭值（包括含有版本號碼的值），以及使用API時傳回內容的說明。

| Accept | 描述 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | 僅傳回ID清單。 這最常用於列出資源。 |
| `application/vnd.adobe.xed+json` | 傳回具有原始的完整JSON結構描述清單 `$ref` 和 `allOf` 包含。 這可用來傳回完整資源的清單。 |
| `application/vnd.adobe.xed+json; version=1` | 原始XDM與 `$ref` 和 `allOf`. 有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 屬性和 `allOf` 已解決。 有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 原始XDM與 `$ref` 和 `allOf`. 無標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 屬性和 `allOf` 已解決。 無標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 屬性和 `allOf` 已解決。 包含描述項。 |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` 和 `allOf` 已解決，具有標題和說明。 已棄用的欄位會以 `meta:status` 屬性： `deprecated`. |

{style="table-layout:auto"}

>[!NOTE]
>
>Platform目前僅支援每個結構描述一個主要版本(`1`)。 因此，此專案的值 `version` 必須一律為 `1` 執行查詢請求以傳回結構描述的最新次要版本時。 如需架構版本設定的詳細資訊，請參閱以下小節。

### 結構描述版本設定 {#versioning}

結構描述版本參考自 `Accept` 結構描述登入API和中的標頭 `schemaRef.contentType` 下游Platform服務API裝載中的屬性。

目前，Platform僅支援單一主要版本(`1`)以取得相同的結果。 根據 [結構描述演化規則](../schema/composition.md#evolution)，結構描述的每次更新都必須是非破壞性的，這表示結構描述的新次要版本(`1.2`， `1.3`、等) 始終與先前的次要版本回溯相容。 因此，在指定 `version=1`，結構描述登入一律會傳回 **最新** 主要版本 `1` 結構描述中，這表示不會傳回先前的次要版本。

>[!NOTE]
>
>只有在資料集參考結構描述且下列其中一個情況為真時，才會強制執行結構描述演化的非破壞性要求：
>
>* 資料已內嵌至資料集。
>* 此資料集已啟用以用於即時客戶個人檔案（即使尚未擷取任何資料）。
>
>如果結構描述尚未與符合上述其中一項條件的資料集建立關聯，則可以對資料集進行任何變更。 但在所有情況下， `version` 元件仍維持在 `1`.

## XDM欄位限制和最佳實務

結構描述的欄位會列在其中 `properties` 物件。 每個欄位本身都是一個物件，包含可描述和限制欄位可包含之資料的屬性。 請參閱以下指南： [在API中定義自訂欄位](../tutorials/custom-fields-api.md) 適用於最常用資料型別的程式碼範例和選擇性限制。

以下範例欄位說明正確格式化的XDM欄位，以及下面提供的有關命名限制和最佳實務的更多詳細資訊。 定義包含類似屬性的其他資源時，也可以套用這些實務。

```JSON
"fieldName": {
    "title": "Field Name",
    "type": "string",
    "format": "date-time",
    "examples": [
        "2004-10-23T12:00:00-06:00"
    ],
    "description": "Full sentence describing the field, using proper grammar and punctuation.",
}
```

* 欄位物件的名稱可能包含英數、破折號或底線字元，但 **可能不會** 以底線開頭。
   * **正確：** `fieldName`， `field_name2`， `Field-Name`， `field-name_3`
   * **不正確：** `_fieldName`
* 欄位物件的名稱偏好使用camelCase。 示例：`fieldName`
* 欄位應包含 `title`，以Title Case撰寫。 示例：`Field Name`
* 欄位需要 `type`.
   * 定義某些型別可能需要選擇性 `format`.
   * 需要特定格式化的資料， `examples` 可作為陣列新增。
   * 欄位型別也可以使用登入中的任何資料型別來定義。 請參閱以下小節： [建立資料型別](./data-types.md#create) 如需詳細資訊，請參閱資料型別端點指南。
* 此 `description` 說明欄位及與欄位資料相關的資訊。 它應以完整的句子撰寫並加上清晰的語言，以便存取結構描述的任何人都能瞭解此欄位的意圖。

## 后续步骤

若要開始使用進行呼叫 [!DNL Schema Registry] API中，選取其中一個可用的端點參考線。

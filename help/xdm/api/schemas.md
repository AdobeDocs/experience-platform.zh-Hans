---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述登入；結構描述登入；結構描述；結構描述；結構描述；建立
solution: Experience Platform
title: 結構描述API端點
description: Schema Registry API中的/schemas端點可讓您以程式設計方式管理體驗應用程式中的XDM結構描述。
exl-id: d0bda683-9cd3-412b-a8d1-4af700297abf
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 2%

---

# 結構描述端點

結構描述可視為您要擷取至Adobe Experience Platform的資料的藍圖。 每個結構描述都由一個類別和零個或多個結構描述欄位群組組成。 此 `/schemas` 中的端點 [!DNL Schema Registry] API可讓您以程式設計方式管理體驗應用程式中的結構描述。

## 快速入门

本指南中使用的API端點是 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

## 擷取結構描述清單 {#list}

您可以在「 」下方列出所有結構描述 `global` 或 `tenant` 向發出GET請求來建立容器 `/global/schemas` 或 `/tenant/schemas`（分別）。

>[!NOTE]
>
>列出資源時，結構描述登入將結果集限製為300個專案。 若要傳回超出此限制的資源，您必須使用分頁引數。 也建議您使用其他查詢引數來篩選結果並減少傳回的資源數量。 請參閱以下小節： [查詢引數](./appendix.md#query) 詳細資訊。

**API格式**

```http
GET /{CONTAINER_ID}/schemas?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 容納您要擷取之結構描述的容器： `global` 適用於Adobe建立的方案或 `tenant` 適用於貴組織擁有的結構描述。 |
| `{QUERY_PARAMS}` | 篩選結果的選用查詢引數。 請參閱 [附錄檔案](./appendix.md#query) 以取得可用引數的清單。 |

{style="table-layout:auto"}

**请求**

以下請求會從擷取結構描述清單 `tenant` 容器，使用 `orderby` 查詢引數，依結果排序 `title` 屬性。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於 `Accept` 標頭已在請求中傳送。 下列專案 `Accept` 標頭可用於列出結構描述：

| `Accept` 頁首 | 描述 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 傳回每個資源的簡短摘要。 這是列出資源的建議標頭。 （上限： 300） |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON結構描述，包含原始檔案 `$ref` 和 `allOf` 包含。 （上限： 300） |

{style="table-layout:auto"}

**响应**

上述請求使用的是 `application/vnd.adobe.xed-id+json` `Accept` 標題，因此回應僅包含 `title`， `$id`， `meta:altId`、和 `version` 每個結構描述的屬性。 使用另一個 `Accept` 頁首(`application/vnd.adobe.xed+json`)會傳回每個結構描述的所有屬性。 選取適當的 `Accept` 標題依您在回應中所需的資訊而定。

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0238be93d3e7a06aec5e0655955901ec",
      "meta:altId": "_{TENANT_ID}.schemas.0238be93d3e7a06aec5e0655955901ec",
      "version": "1.4",
      "title": "Hotels"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/0ef4ce0d390f0809fad490802f53d30b",
      "meta:altId": "_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b",
      "version": "1.0",
      "title": "Loyalty Members"
    }
  ],
  "_page": {
        "orderby": "title",
        "next": null,
        "count": 2
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

## 查詢結構描述 {#lookup}

您可以透過在路徑中包含結構描述ID的GET請求來查詢特定結構描述。

**API格式**

```http
GET /{CONTAINER_ID}/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 容納您要擷取之結構描述的容器： `global` 適用於Adobe建立的結構描述或 `tenant` 適用於貴組織擁有的結構描述。 |
| `{SCHEMA_ID}` | 此 `meta:altId` 或URL編碼 `$id` 要查閱的結構描述中。 |

{style="table-layout:auto"}

**请求**

以下請求會擷取其指定的結構描述 `meta:altId` 路徑中的值。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
  -H 'Accept: application/vnd.adobe.xed+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於 `Accept` 標頭已在請求中傳送。 所有查詢請求都需要 `version` 包含在 `Accept` 標頭。 下列專案 `Accept` 標頭可供使用：

| `Accept` 頁首 | 描述 |
| ------- | ------------ |
| `application/vnd.adobe.xed+json; version=1` | 原始 `$ref` 和 `allOf`，有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 和 `allOf` 已解決，具有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version=1` | 原始 `$ref` 和 `allOf`，無標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` 和 `allOf` 已解決，無標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` 和 `allOf` 已解決，包含描述項。 |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` 和 `allOf` 已解決，具有標題和說明。 已棄用的欄位會以 `meta:status` 屬性： `deprecated`. |

{style="table-layout:auto"}

**响应**

成功的回應會傳回結構描述的詳細資訊。 傳回的欄位取決於 `Accept` 標頭已在請求中傳送。 使用不同的實驗 `Accept` 標頭，用來比較回應及判斷哪個標頭最適合您的使用案例。

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:altId": "_{TENANT_ID}.schemas.20af3f1d4b175f27ba59529d1b51a0c79fc25df454117c80",
  "meta:resourceType": "schemas",
  "version": "1.1",
  "title": "Example schema",
  "type": "object",
  "description": "An example schema created within the tenant container.",
  "allOf": [
      {
          "$ref": "https://ns.adobe.com/xdm/context/profile",
          "type": "object",
          "meta:xdmType": "object"
      },
      {
          "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
          "type": "object",
          "meta:xdmType": "object"
      }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
      "https://ns.adobe.com/{TENANT_ID}/mixins/443fe51457047d958f4a97853e64e0eca93ef34d7990583b",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
      "repo:createdDate": 1602872911226,
      "repo:lastModifiedDate": 1603381419889,
      "xdm:createdClientId": "{CLIENT_ID}",
      "xdm:lastModifiedClientId": "{CLIENT_ID}",
      "xdm:createdUserId": "{USER_ID}",
      "xdm:lastModifiedUserId": "{USER_ID}",
      "eTag": "84b4da79b7445a4bf1c59269e718065effddb983c492f48e223d49c049c6d589",
      "meta:globalLibVersion": "1.15.4"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## 创建架构 {#create}

結構描述構成程式從指派類別開始。 類別會定義資料的主要行為方面（記錄或時間序列），以及描述將擷取之資料所需的最少欄位。

>[!NOTE]
>
>以下範例呼叫只是如何在API中建立結構描述的基本範例，具有類別和無欄位群組的最低構成要求。 如需如何在API中建立結構的完整步驟，包括如何使用欄位群組和資料型別指派欄位，請參閱 [結構描述建立教學課程](../tutorials/create-schema-api.md).

**API格式**

```http
POST /tenant/schemas
```

**请求**

請求必須包含 `allOf` 參照 `$id` 類別的。 此屬性會定義結構描述將實作的「基底類別」。 在此範例中，基底類別是先前建立的「屬性資訊」類別。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property Information",
        "description": "Property-related information.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590" 
          } 
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `allOf` | 一個物件陣列，每個物件都參照結構描述實作其欄位的類別或欄位群組。 每個物件都包含單一屬性(`$ref`)，其值代表 `$id` 新結構描述將實作的類別或欄位群組的名稱。 必須提供一個類別，並附帶零個或多個額外的欄位群組。 在上述範例中， `allOf` array是結構描述的類別。 |

{style="table-layout:auto"}

**响应**

成功的回應會傳回HTTP狀態201 （已建立）以及包含新建立之結構描述詳細資訊的裝載，包括 `$id`， `meta:altId`、和 `version`. 這些值是唯讀的，並由 [!DNL Schema Registry].

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088461236,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

執行GET要求至 [列出所有結構描述](#list) 在租使用者容器中，現在會包含新結構描述。 您可以執行 [查詢(GET)請求](#lookup) 使用URL編碼 `$id` URI直接檢視新結構描述。

若要將其他欄位新增到結構描述，您可以執行 [PATCH作業](#patch) 將欄位群組新增至結構描述的 `allOf` 和 `meta:extends` 陣列。

## 更新結構描述 {#put}

您可以透過PUT操作取代整個結構描述，基本上是重寫資源。 透過PUT請求更新結構描述時，本文必須包含以下情況所需的所有欄位： [建立新結構描述](#create) 在POST請求中。

>[!NOTE]
>
>如果您只想更新部分結構描述，而不是完全取代，請參閱 [更新結構描述的一部分](#patch).

**API格式**

```http
PUT /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | 此 `meta:altId` 或URL編碼 `$id` 重新寫入的結構描述中。 |

{style="table-layout:auto"}

**请求**

以下請求會取代現有結構描述，並變更其 `title`， `description`、和 `allOf` 屬性。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Commercial Property Information",
        "description": "Information related to commercial properties.",
        "type": "object",
        "allOf": [ 
          { 
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7" 
          } 
        ]
      }'
```

**响应**

成功的回應會傳回更新後之結構的詳細資訊。

```JSON
{
    "title":"Commercial Property Information",
    "description": "Information related to commercial properties.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
        "https://ns.adobe.com/xdm/data/record"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.0",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088470592,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## 更新結構描述的一部分 {#patch}

您可以使用PATCH請求來更新結構描述的一部分。 此 [!DNL Schema Registry] 支援所有標準JSON修補程式操作，包括 `add`， `remove`、和 `replace`. 如需JSON修補程式的詳細資訊，請參閱 [API基礎指南](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>如果您想使用新值取代整個資源，而不是更新個別欄位，請參閱 [使用PUT操作取代結構描述](#put).

最常見的PATCH作業之一是將先前定義的欄位群組新增到結構描述，如以下範例所示。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼 `$id` URI或 `meta:altId` 要更新的結構描述。 |

{style="table-layout:auto"}

**请求**

以下範例請求會新增欄位群組，藉此將新的欄位群組新增至結構描述。 `$id` 值會同時變成 `meta:extends` 和 `allOf` 陣列。

請求內文採用陣列形式，每個列出的物件都代表個別欄位的特定變更。 每個物件都包含要執行的操作(`op`)，操作應執行於哪個欄位(`path`)，以及該作業應包含哪些資訊(`value`)。

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/meta:extends/-",
          "value":  "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        },
        {
          "op": "add",
          "path": "/allOf/-",
          "value":  {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
          }
        }
      ]'
```

**响应**

回應顯示兩個操作都已成功執行。 欄位群組 `$id` 已新增至 `meta:extends` 陣列和參考(`$ref`)至欄位群組 `$id` 現在會顯示在 `allOf` 陣列。

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## 啟用結構描述以用於Real-Time Customer Profile {#union}

為了讓結構描述參與 [即時客戶個人檔案](../../profile/home.md)，您必須新增 `union` 標籤到結構描述的 `meta:immutableTags` 陣列。 您可以對相關結構描述發出PATCH要求來達到此目的。

>[!IMPORTANT]
>
>不可變標籤是旨在設定但從未移除的標籤。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼 `$id` URI或 `meta:altId` 要啟用的結構描述。 |

{style="table-layout:auto"}

**请求**

以下範例請求新增 `meta:immutableTags` 陣列轉換為現有結構描述，為陣列提供單一字串值 `union` 以啟用它以用於設定檔。

```SHELL
curl -X PATCH\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        {
          "op": "add",
          "path": "/meta:immutableTags",
          "value": ["union"]
        }
      ]'
```

**响应**

成功回應會傳回更新後結構的詳細資料，指出 `meta:immutableTags` 已新增陣列。

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.1",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552088649634,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    },
    "meta:immutableTags": [
      "union"
    ]
}
```

您現在可以檢視此結構描述類別的聯合，以確認結構描述的欄位已呈現。 請參閱 [聯合端點指南](./unions.md) 以取得詳細資訊。

## 刪除結構描述 {#delete}

有時可能需要從結構描述登入中移除結構描述。 這是透過使用路徑中提供的結構描述ID執行DELETE請求來完成。

**API格式**

```http
DELETE /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼 `$id` URI或 `meta:altId` 要刪除的結構描述中。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。

您可以嘗試對結構描述進行查詢(GET)請求以確認刪除。 您需要包含 `Accept` 標頭中，但應該會收到HTTP狀態404 （找不到），因為結構描述已從結構描述登入中移除。

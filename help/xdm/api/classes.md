---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；體驗資料模型；資料模型；資料模型；類別登入；架構登入；類別；類別；類別；類別；建立
solution: Experience Platform
title: 類別API端點
description: Schema Registry API中的/classes端點可讓您以程式設計方式管理體驗應用程式中的XDM類別。
exl-id: 7beddb37-0bf2-4893-baaf-5b292830f368
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 1%

---

# 類別端點

所有Experience Data Model (XDM)結構描述都必須根據類別。 類別決定了該類別的所有結構描述都必須包含的通用屬性的基本結構，以及哪些結構描述欄位群組適合用於這些結構描述。 此外，結構描述的類別會決定結構描述將包含之資料的行為方面，其中有兩種型別：

* **[!UICONTROL 記錄]**：提供主旨屬性的相關資訊。 主體可以是組織或個人。
* **[!UICONTROL 時間序列]**：提供記錄主體直接或間接執行動作時的系統快照。

>[!NOTE]
>
>如需資料行為類別如何影響結構描述構成的詳細資訊，請參閱 [結構描述組合基本概念](../schema/composition.md).

此 `/classes` 中的端點 [!DNL Schema Registry] API可讓您以程式設計方式管理體驗應用程式中的類別。

## 快速入门

本指南中使用的端點是 [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

## 擷取類別清單 {#list}

您可以列出所有類別在 `global` 或 `tenant` 向發出GET請求來建立容器 `/global/classes` 或 `/tenant/classes`（分別）。

>[!NOTE]
>
>列出資源時，結構描述登入將結果集限製為300個專案。 若要傳回超出此限制的資源，您必須使用分頁引數。 也建議您使用其他查詢引數來篩選結果並減少傳回的資源數量。 請參閱以下小節： [查詢引數](./appendix.md#query) 詳細資訊。

**API格式**

```http
GET /{CONTAINER_ID}/classes?{QUERY_PARAMS}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 您要擷取類別的容器： `global` Adobe建立的類別或 `tenant` 適用於貴組織擁有的類別。 |
| `{QUERY_PARAMS}` | 篩選結果的選用查詢引數。 請參閱 [附錄檔案](./appendix.md#query) 以取得可用引數的清單。 |

{style="table-layout:auto"}

**请求**

下列要求會從 `tenant` 容器，使用 `orderby` 查詢引數，依類別排序 `title` 屬性。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes?orderby=title \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於 `Accept` 標頭已在請求中傳送。 下列專案 `Accept` 標頭可用於列出類別：

| `Accept` 頁首 | 描述 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 傳回每個資源的簡短摘要。 這是列出資源的建議標頭。 （上限： 300） |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON類別（含原始專案） `$ref` 和 `allOf` 包含。 （上限： 300） |

{style="table-layout:auto"}

**响应**

上述請求使用的是 `application/vnd.adobe.xed-id+json` `Accept` 標題，因此回應僅包含 `title`， `$id`， `meta:altId`、和 `version` 每個類別的屬性。 使用另一個 `Accept` 頁首(`application/vnd.adobe.xed+json`)會傳回每個類別的所有屬性。 選取適當的 `Accept` 標題依您在回應中所需的資訊而定。

```json
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/01b7b1745e8ac4ed1e8784ec91b6afa7",
      "meta:altId": "_{TENANT_ID}.classes.01b7b1745e8ac4ed1e8784ec91b6afa7",
      "version": "1.0",
      "title": "Hotel"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/d43b86253676af50da3f671ecdd26ff9",
      "meta:altId": "_{TENANT_ID}.classes.d43b86253676af50da3f671ecdd26ff9",
      "version": "1.1",
      "title": "Property"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/366f015dbfea802455fbc46c3b27f771",
      "meta:altId": "_{TENANT_ID}.classes.366f015dbfea802455fbc46c3b27f771",
      "version": "1.0",
      "title": "Subscription"
    }
  ],
  "_page": {
    "orderby": "title",
    "next": null,
    "count": 3
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/classes"
    }
  }
}
```

## 查詢類別 {#lookup}

您可以在GET要求的路徑中包含類別ID來查詢特定類別。

**API格式**

```http
GET /{CONTAINER_ID}/classes/{CLASS_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CONTAINER_ID}` | 容納您要擷取之類別的容器： `global` Adobe建立的類別或 `tenant` 適用於貴組織擁有的類別。 |
| `{CLASS_ID}` | 此 `meta:altId` 或URL編碼 `$id` 要查閱的類別中。 |

{style="table-layout:auto"}

**请求**

下列要求會依照類別類別的 `meta:altId` 路徑中提供的值。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.f579a0b5f992c69458ea408ec36571f7da9de15901bab116 \
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

{style="table-layout:auto"}

**响应**

成功的回應會傳回類別的詳細資料。 傳回的欄位取決於 `Accept` 標頭已在請求中傳送。 使用不同的實驗 `Accept` 標頭，用來比較回應及判斷哪個標頭最適合您的使用案例。

```json
{
  "$id":"https://ns.adobe.com/{TENANT_ID}/classes/f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:altId":"_{TENANT_ID}.classes.f8bbdc3c49d49eae62d1c17e867230ac3de6b5b63b0615ce",
  "meta:resourceType":"classes",
  "version":"1.1",
  "title":"Hotel",
  "type":"object",
  "description":"Base class for the Hotels schema",
  "definitions":{
    "customFields":{
      "type":"object",
      "properties":{
        "_{TENANT_ID}":{
          "type":"object",
          "properties":{
            "Address":{
              "title":"Address",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/common/address",
              "type":"object",
              "meta:xdmType":"object"
            },
            "phoneNumber":{
              "title":"Phone Number",
              "description":"",
              "isRequired":false,
              "$ref":"https://ns.adobe.com/xdm/context/phonenumber",
              "type":"object",
              "meta:xdmType":"object"
            },
            "brand":{
              "title":"Brand",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            },
            "hotelId":{
              "title":"Hotel ID",
              "description":"",
              "type":"string",
              "isRequired":false,
              "meta:xdmType":"string"
            }
          },
          "meta:xdmType":"object"
        }
      },
      "meta:xdmType":"object"
    }
  },
  "allOf":[
    {
      "$ref":"https://ns.adobe.com/xdm/data/record",
      "type":"object",
      "meta:xdmType":"object"
    },
    {
      "$ref":"#/definitions/customFields",
      "type":"object",
      "meta:xdmType":"object"
    }
  ],
  "imsOrg":"{ORG_ID}",
  "meta:extensible":true,
  "meta:abstract":true,
  "meta:extends":[
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:xdmType":"object",
  "meta:registryMetadata":{
    "repo:createdDate":1593643258779,
    "repo:lastModifiedDate":1597246362579,
    "xdm:createdClientId":"{CLIENT_ID}",
    "xdm:lastModifiedClientId":"{CLIENT_ID}",
    "xdm:createdUserId":"{USER_ID}",
    "xdm:lastModifiedUserId":"{USER_ID}",
    "eTag":"502f89ee16b8ab2e6b4ea09ecf0ab1e5614907db755051c1f3c65a273001d725",
    "meta:globalLibVersion":"1.15.4"
  },
  "meta:containerId":"tenant",
  "meta:tenantNamespace":"_{TENANT_ID}"
}
```

## 建立類別 {#create}

您可以在下定義自訂類別 `tenant` 容器建立POST要求。

>[!IMPORTANT]
>
>根據您定義的自訂類別構成結構描述時，您將無法使用標準欄位群組。 每個欄位群組都會定義與其相容的類別 `meta:intendedToExtend` 屬性。 開始定義與新類別相容的欄位群組後(透過使用 `$id` 的新類別 `meta:intendedToExtend` 欄位群組的欄位群組)，則每次定義實作您所定義之類別的結構描述時，都可以重複使用這些欄位群組。 請參閱以下小節： [建立欄位群組](./field-groups.md#create) 和 [建立方案](./schemas.md#create) 在其各自的端點指南中瞭解更多資訊。
>
>如果您打算根據即時客戶設定檔中的自訂類別使用結構描述，請記住，聯合結構描述僅根據共用相同類別的結構描述來建構。 如果您想將自訂類別結構描述包含在另一個類別(例如 [!UICONTROL XDM個別設定檔] 或 [!UICONTROL XDM ExperienceEvent]，您必須與使用該類別的其他結構描述建立關係。 請參閱教學課程，位置如下： [在API中的兩個結構描述之間建立關係](../tutorials/relationship-api.md) 以取得詳細資訊。

**API格式**

```http
POST /tenant/classes
```

**请求**

建立(POST)類別的要求必須包括 `allOf` 包含 `$ref` 變更為下列兩個值之一： `https://ns.adobe.com/xdm/data/record` 或 `https://ns.adobe.com/xdm/data/time-series`. 這些值代表類別所依據的行為（分別是記錄或時間序列）。 如需記錄資料與時間序列資料之間差異的詳細資訊，請參閱 [結構描述組合基本概念](../schema/composition.md).

定義類別時，您也可以在類別定義中包含欄位群組或自訂欄位。 這會導致新增的欄位群組和欄位包含在實作類別的所有結構描述中。 以下範例請求會定義一個名為「Property」的類別，用於擷取有關公司擁有和經營的不同屬性的資訊。 它包含 `propertyId` 每次使用類別時要包含的欄位。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"Property",
        "description":"Properties owned and operated by the company.",
        "type":"object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property Identification Number",
                        "type": "string",
                        "description": "Unique Property identification number"
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `_{TENANT_ID}` | 此 `TENANT_ID` 適用於您組織的名稱空間。 貴組織建立的所有資源都必須包含此屬性，以避免與中的其他資源衝突。 [!DNL Schema Registry]. |
| `allOf` | 新類別要繼承其屬性的資源清單。 其中一項 `$ref` 陣列中的物件會定義類別的行為。 在此範例中，類別會繼承「記錄」行為。 |

{style="table-layout:auto"}

**响应**

成功的回應會傳回HTTP狀態201 （已建立）以及包含新建立類別詳細資訊的裝載，包括 `$id`， `meta:altId`、和 `version`. 這三個值均為唯讀，並由 [!DNL Schema Registry].

```JSON
{
  "title": "Property",
  "description": "Properties owned and operated by the company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property Identification Number",
                  "type": "string",
                  "description": "Unique Property identification number",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

執行GET要求至 [列出所有類別](#list) 在 `tenant` 容器現在會包含Property類別。 您也可以 [執行查詢(GET)請求](#lookup) 使用URL編碼 `$id` 以直接檢視新類別。

## 更新類別 {#put}

您可以透過PUT操作取代整個類別，基本上是重寫資源。 透過PUT要求更新類別時，本文必須包含以下情況所需的所有欄位： [建立新類別](#create) 在POST請求中。

>[!NOTE]
>
>如果您只想更新類別的一部分而不是完全取代它，請參閱以下小節： [更新類別的一部分](#patch).

**API格式**

```http
PUT /tenant/classes/{CLASS_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CLASS_ID}` | 此 `meta:altId` 或URL編碼 `$id` 要重新寫入的類別。 |

{style="table-layout:auto"}

**请求**

下列要求會重新寫入現有類別，變更其 `description` 和 `title` 其中一個欄位的。

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Property",
        "description": "Base class for properties operated by a company.",
        "type": "object",
        "definitions": {
          "property": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "property": {
                    "title": "Property Information",
                    "type": "object",
                    "description": "Information about different owned and operated properties.",
                    "properties": {
                      "propertyId": {
                        "title": "Property ID",
                        "type": "string",
                        "description": "Unique Property ID string."
                      }
                    }
                  }
                }
              }
            },
            "type": "object"
          }
        },
        "allOf": [
          {
            "$ref": "https://ns.adobe.com/xdm/data/record"
          },
          {
            "$ref": "#/definitions/property"
          }
        ]
      }'
```

**响应**

成功的回應會傳回更新類別的詳細資料。

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## 更新類別的一部分 {#patch}

您可以使用PATCH請求來更新類別的一部分。 此 [!DNL Schema Registry] 支援所有標準JSON修補程式操作，包括 `add`， `remove`、和 `replace`. 如需JSON修補程式的詳細資訊，請參閱 [API基礎指南](../../landing/api-fundamentals.md#json-patch).

>[!NOTE]
>
>如果您想使用新值取代整個資源，而不是更新個別欄位，請參閱 [使用PUT作業取代類別](#put).

**API格式**

```http
PATCH /tenant/class/{CLASS_ID} 
```

| 参数 | 描述 |
| --- | --- |
| `{CLASS_ID}` | URL編碼 `$id` URI或 `meta:altId` 要更新的類別。 |

{style="table-layout:auto"}

**请求**

以下範例請求會更新 `description` 現有類別的，以及 `title` 其中一個欄位的。

請求內文採用陣列形式，每個列出的物件都代表個別欄位的特定變更。 每個物件都包含要執行的操作(`op`)，操作應執行於哪個欄位(`path`)，以及該作業應包含哪些資訊(`value`)。

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { "op": "replace", "path": "/description", "value":  "Base class for properties operated by a company."},
        { "op": "replace", "path": "/definitions/property/properties/_{TENANT_ID}/properties/property/properties/propertyId/title", "value": "Unique Property ID string" }
      ]'
```

**响应**

回應顯示兩個操作都已成功執行。 此 `description` 已更新，以及 `title` 的 `propertyId` 欄位。

```JSON
{
  "title": "Property",
  "description": "Base class for properties operated by a company.",
  "type": "object",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "property": {
              "title": "Property Information",
              "type": "object",
              "description": "Information about different owned and operated properties.",
              "properties": {
                "propertyId": {
                  "title": "Property ID",
                  "type": "string",
                  "description": "Unique Property ID string",
                  "meta:xdmType": "string"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      },
      "type": "object",
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/data/record"
    },
    {
      "$ref": "#/definitions/property"
    }
  ],
  "meta:abstract": true,
  "meta:extensible": true,
  "meta:extends": [
    "https://ns.adobe.com/xdm/data/record"
  ],
  "meta:containerId": "tenant",
  "imsOrg": "{ORG_ID}",
  "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590",
  "meta:xdmType": "object",
  "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
  "version": "1.0",
  "meta:resourceType": "classes",
  "meta:registryMetadata": {
    "repo:createDate": 1552086405448,
    "repo:lastModifiedDate": 1552086405448,
    "xdm:createdClientId": "{CREATED_CLIENT}",
    "xdm:repositoryCreatedBy": "{CREATED_BY}"
  }
}
```

## 刪除類別 {#delete}

有時可能需要從結構描述登入中移除類別。 這是透過使用路徑中提供的類別ID執行DELETE要求來完成。

**API格式**

```http
DELETE /tenant/classes/{CLASS_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{CLASS_ID}` | URL編碼 `$id` URI或 `meta:altId` 要刪除的類別。 |

{style="table-layout:auto"}

**请求**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes/_{TENANT_ID}.classes.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。

您可以嘗試 [查詢(GET)請求](#lookup) 類別的。 您需要包含 `Accept` 標頭中，但是應該會收到HTTP狀態404 （找不到），因為類別已從Schema Registry中移除。

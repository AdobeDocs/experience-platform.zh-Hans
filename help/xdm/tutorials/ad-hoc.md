---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；體驗資料模型；資料模型；結構描述登入；結構描述登入；ad-hoc；ad-hoc；ad-hoc；Ad-hoc；教學課程；教學課程；建立；結構描述；結構描述
solution: Experience Platform
title: 建立臨時結構描述
description: 在特定情況下，可能有必要建立體驗資料模型(XDM)結構描述，其中包含僅供單一資料集使用的名稱空間欄位。 這稱為「臨機」結構描述。 臨機結構用於各種資料擷取工作流程中以進行Experience Platform，包括擷取CSV檔案和建立特定型別的來源連線。
type: Tutorial
exl-id: bef01000-909a-4594-8cf4-b9dbe0b358d5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 2%

---

# 建立臨時結構描述

在特定情況下，您可能需要建立 [!DNL Experience Data Model] (XDM)結構描述，其欄位已命名為僅供單一資料集使用。 這稱為「臨機」結構描述。 臨時結構用於各種資料擷取工作流程 [!DNL Experience Platform]，包括擷取CSV檔案和建立特定型別的來源連線。

本檔案提供使用來建立臨時結構描述的一般步驟。 [結構描述登入API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). 此函式旨在搭配其他 [!DNL Experience Platform] 需要建立隨選結構描述作為其工作流程一部分的教學課程。 其中每份檔案都提供有關如何為其特定使用案例正確設定臨時結構的詳細資訊。

## 快速入门

本教學課程需要您實際瞭解 [!DNL Experience Data Model] (XDM)系統。 開始進行本教學課程之前，請先檢閱下列XDM檔案：

- [XDM系統總覽](../home.md)：XDM及其在下列專案實作的高層級概觀： [!DNL Experience Platform].
- [結構描述組合基本概念](../schema/composition.md)：XDM結構描述的基本元件概觀。

在開始本教學課程之前，請檢閱 [開發人員指南](../api/getting-started.md) 如需您成功對 [!DNL Schema Registry] API。 這包括您的 `{TENANT_ID}`、「容器」的概念，以及發出請求所需的標頭（特別注意「接受」標頭及其可能的值）。

## 建立臨時類別

XDM結構描述的資料行為由其基礎類別決定。 建立臨時結構描述的第一步，是根據 `adhoc` 行為。 這是透過向發出POST請求來完成 `/tenant/classes` 端點。

**API格式**

```http
POST /tenant/classes
```

**请求**

以下請求會建立新的XDM類別，由承載中提供的屬性設定。 藉由提供 `$ref` 屬性設定為 `https://ns.adobe.com/xdm/data/adhoc` 在 `allOf` 陣列，此類別會繼承 `adhoc` 行為。 此請求也會定義 `_adhoc` 物件，其中包含類別的自訂欄位。

>[!NOTE]
>
>下定義的自訂欄位 `_adhoc` 會因臨時結構描述的使用案例而異。 如需根據使用案例所需的自訂欄位，請參閱相應教學課程中的特定工作流程。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/classes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New ad-hoc class",
        "description": "New ad-hoc class description",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/xdm/data/adhoc"
          },
          {
            "properties": {
              "_adhoc": {
                "type":"object",
                "properties": {
                  "field1": {
                    "type":"string"
                  },
                  "field2": {
                    "type":"string"
                  }
                }
              }
            }
          }
        ]
      }'
```

| 属性 | 描述 |
| --- | --- |
| `$ref` | 新類別的資料行為。 若為臨機類別，此值必須設為 `https://ns.adobe.com/xdm/data/adhoc`. |
| `properties._adhoc` | 包含類別自訂欄位的物件，以欄位名稱和資料型別的索引鍵值配對表示。 |

{style="table-layout:auto"}

**响应**

成功的回應會傳回新類別的詳細資料，取代 `properties._adhoc` 具有GUID的物件名稱，該GUID是系統產生的類別的唯讀唯一識別碼。 此 `meta:datasetNamespace` 屬性也會自動產生，並包含在回應中。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:altId": "_{TENANT_ID}.classes.6395cbd58812a6d64c4e5344f7b9120f",
    "meta:resourceType": "classes",
    "version": "1.0",
    "title": "New Class",
    "description": "New class description",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/data/adhoc"
        },
        {
            "properties": {
                "_6395cbd58812a6d64c4e5344f7b9120f": {
                    "type": "object",
                    "properties": {
                        "field1": {
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "field2": {
                            "type": "string",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:extends": [
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557527784822,
        "repo:lastModifiedDate": 1557527784822,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

| 属性 | 描述 |
| --- | --- |
| `$id` | 作為唯讀的URI，系統為新的ad-hoc類別產生的唯一識別碼。 此值用於建立臨時結構描述的下一個步驟。 |

{style="table-layout:auto"}

## 建立臨時結構描述

建立臨時類別後，您可以透過向以下專案發出POST要求，建立實作該類別的新結構描述： `/tenant/schemas` 端點。

**API格式**

```http
POST /tenant/schemas
```

**请求**

以下請求會建立新結構描述，並提供參考(`$ref`)重新命名為 `$id` 其裝載中先前建立的臨機類別。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title":"New Schema",
        "description": "New schema description.",
        "type":"object",
        "allOf": [
          {
            "$ref":"https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
          }
        ]
      }'
```

**响应**

成功的回應會傳回新建立之綱要的詳細資訊，包括其系統產生的唯讀 `$id`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f"
        }
    ],
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "Jggrlh4PQdZUvDUhQHXKx38iTQo="
    }
}
```

## 檢視完整的臨時結構描述

>[!NOTE]
>
>此步骤是可选的。如果您不想要檢查臨機操作結構描述的欄位結構，您可以跳至 [後續步驟](#next-steps) 區段（在本教學課程結束時）。

建立臨時結構描述後，您可以提出查詢(GET)請求，以展開形式檢視結構描述。 若要這麼做，請在GET要求中使用適當的Accept標頭，如下所示。

**API格式**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼 `$id` URI或 `meta:altId` 您想要存取的臨時結構描述中。 |

{style="table-layout:auto"}

**请求**

以下請求使用Accept標頭 `application/vnd.adobe.xed-full+json; version=1`，會傳回結構描述的展開形式。 請注意，從擷取特定資源時 [!DNL Schema Registry]，請求的Accept標頭必須包含相關資源的主要版本。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**响应**

成功的回應會傳回結構描述的詳細資訊，包括巢狀至下的所有欄位 `properties`.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d",
    "meta:altId": "_{TENANT_ID}.schemas.26f6833e55db1dd8308aa07a64f2042d",
    "meta:resourceType": "schemas",
    "version": "1.0",
    "title": "New Schema",
    "description": "New schema description.",
    "type": "object",
    "meta:datasetNamespace": "_6395cbd58812a6d64c4e5344f7b9120f",
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/6395cbd58812a6d64c4e5344f7b9120f",
        "https://ns.adobe.com/xdm/data/adhoc"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{ORG_ID}",
    "meta:xdmType": "object",
    "properties": {
        "_6395cbd58812a6d64c4e5344f7b9120f": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "field1": {
                    "type": "string",
                    "meta:xdmType": "string"
                },
                "field2": {
                    "type": "string",
                    "meta:xdmType": "string"
                }
            }
        }
    },
    "meta:registryMetadata": {
        "repo:createdDate": 1557528570542,
        "repo:lastModifiedDate": 1557528570542,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:lastModifiedClientId": "{MODIFIED_CLIENT}",
        "eTag": "bTogM1ON2LO/F7rlcc1iOWmNVy0="
    }
}
```

## 后续步骤 {#next-steps}

依照本教學課程，您已成功建立新的臨時結構描述。 如果您是其他教學課程的一部分，現在可以使用 `$id` 以依照指示完成工作流程。

有關使用的詳細資訊 [!DNL Schema Registry] API，請參閱 [開發人員指南](../api/getting-started.md).

---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述登入；結構描述；結構描述；結構描述；關係；關係描述項；參考身分；參考身分；
title: 使用結構描述登入API定義兩個結構描述之間的關係
description: 本檔案提供教學課程，說明如何定義貴組織使用Schema Registry API定義之兩個結構描述之間的一對一關係。
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '1383'
ht-degree: 1%

---

# 使用定義兩個結構描述之間的關係 [!DNL Schema Registry] API

瞭解客戶之間的關係以及客戶在不同管道中與您品牌的互動是Adobe Experience Platform的重要部分。 在的結構中定義這些關係 [!DNL Experience Data Model] (XDM)結構描述可讓您對客戶資料獲得複雜的深入分析。

雖然結構描述關係可透過使用聯合結構描述和來推斷 [!DNL Real-Time Customer Profile]，這僅適用於共用相同類別的結構描述。 若要在屬於不同類別的兩個結構描述之間建立關係，必須將專用關係欄位新增至 **來源結構描述**，表示個別專案的身分 **參考結構描述**.

>[!NOTE]
>
>結構描述登入API將參考結構描述稱為「目的地結構描述」。 這些不應與中的目的地結構描述混淆 [資料準備對應集](../../data-prep/mapping-set.md) 或結構描述 [目的地連線](../../destinations/home.md).

本檔案提供教學課程，說明如何定義貴組織透過以下工具定義之兩個結構描述之間的一對一關係： [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## 快速入门

本教學課程需要您實際瞭解 [!DNL Experience Data Model] (XDM)和 [!DNL XDM System]. 在開始本教學課程之前，請檢閱下列檔案：

* [Experience Platform中的XDM系統](../home.md)：XDM及其在中的實作概觀 [!DNL Experience Platform].
   * [結構描述組合基本概念](../schema/composition.md)：XDM結構描述建置區塊簡介。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

在開始本教學課程之前，請檢閱 [開發人員指南](../api/getting-started.md) 如需您成功對 [!DNL Schema Registry] API。 這包括您的 `{TENANT_ID}`、「容器」的概念，以及提出請求所需的標頭(請特別注意 [!DNL Accept] 標頭及其可能的值)。

## 定義來源和參考結構描述 {#define-schemas}

您應已建立將在關係中定義的兩個結構描述。 本教學課程在組織目前的熟客方案成員之間建立關係(定義於「[!DNL Loyalty Members]「結構描述)及其最喜愛的飯店(定義於「[!DNL Hotels]&quot;結構描述)。

結構描述關係由 **來源結構描述** 有一個欄位參照內的另一個欄位 **參考結構描述**. 在接下來的步驟中， 」[!DNL Loyalty Members]&quot;將是來源結構描述，而&quot;[!DNL Hotels]」將做為參考結構描述。

>[!IMPORTANT]
>
>為了建立關係，兩個結構描述都必須定義主要身分並啟用 [!DNL Real-Time Customer Profile]. 請參閱以下小節： [啟用結構描述以在設定檔中使用](./create-schema-api.md#profile) 架構建立教學課程中，如果您需要有關如何據以設定架構的指引。

若要定義兩個結構描述之間的關係，您必須先取得 `$id` 兩個結構描述的值。 如果您知道顯示名稱(`title`)中，您可以找到 `$id` 向以下傳送GET要求而獲得值： `/tenant/schemas` 中的端點 [!DNL Schema Registry] API。

**API格式**

```http
GET /tenant/schemas
```

**请求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>此 [!DNL Accept] 頁首 `application/vnd.adobe.xed-id+json` 僅傳回所產生結構描述的標題、ID和版本。

**响应**

成功回應會傳回您的組織所定義的結構描述清單，包括其 `name`， `$id`， `meta:altId`、和 `version`.

```json
{
    "results": [
        {
            "title": "Newsletter Subscriptions",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/192a66930afad02408429174c311ae73",
            "meta:altId": "_{TENANT_ID}.schemas.192a66930afad02408429174c311ae73",
            "version": "1.2"
        },
        {
            "title": "Loyalty Members",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
            "version": "1.5"
        },
        {
            "title": "Hotels",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
            "meta:altId": "_{TENANT_ID}.schemas.d4ad4b8463a67f6755f2aabbeb9e02c7",
            "version": "1.0"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform-stage.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

記錄 `$id` 您要定義兩者之間關係的兩個結構描述的值。 這些值將在後續步驟中使用。

## 定義來源結構描述的參考欄位

在內 [!DNL Schema Registry]，關係描述元的運作方式類似於關聯式資料庫表格中的外來索引鍵：來源綱要中的欄位會作為參照綱要之主要身分欄位的參照。 如果您的來源結構描述沒有用於此目的的欄位，您可能需要使用新欄位建立結構描述欄位群組，並將其新增到結構描述。 此新欄位必須具有 `type` 值 `string`.

>[!IMPORTANT]
>
>來源結構描述不能使用其主要身分作為參考欄位。

在本教學課程中，參考結構描述»[!DNL Hotels]&quot;包含 `hotelId` 做為結構描述主要身分的欄位。 然而，來源結構描述&quot;[!DNL Loyalty Members]&quot;沒有專用欄位可做為參照 `hotelId`，因此需要建立自訂欄位群組，才能將新欄位新增到結構描述中： `favoriteHotel`.

>[!NOTE]
>
>如果您的來源結構描述已有您打算用作參考欄位的專用欄位，您可以跳至上的步驟 [建立參考描述項](#reference-identity).

### 建立新的欄位群組

為了將新欄位新增到結構描述，必須首先在欄位群組中定義它。 您可以向以下專案發出POST請求，以建立新的欄位群組： `/tenant/fieldgroups` 端點。

**API格式**

```http
POST /tenant/fieldgroups
```

**请求**

以下請求會建立新欄位群組，新增 `favoriteHotel` 欄位位於 `_{TENANT_ID}` 要新增到的任何結構描述的名稱空間。

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel field group for the Loyalty Members schema.",
        "definitions": {
            "favoriteHotel": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "favoriteHotel": {
                      "title": "Favorite Hotel",
                      "type": "string",
                      "description": "Favorite hotel for a Loyalty Member."
                    }
                  }
                }
              }
            }
        },
        "allOf": [
            {
              "$ref": "#/definitions/favoriteHotel"
            }
        ]
      }'
```

**响应**

成功的回應會傳回新建立的欄位群組的詳細資訊。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220",
    "meta:altId": "_{TENANT_ID}.mixins.3387945212ad76ee59b6d2b964afb220",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "type": "object",
    "title": "Favorite Hotel",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Favorite hotel field group for the Loyalty Members schema.",
    "definitions": {
        "favoriteHotel": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "favoriteHotel": {
                            "title": "Favorite Hotel",
                            "type": "string",
                            "description": "Favorite hotel for a Loyalty Member.",
                            "meta:xdmType": "string"
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
            "$ref": "#/definitions/favoriteHotel"
        }
    ],
    "meta:xdmType": "object",
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:registryMetadata": {
        "eTag": "quM2aMPyb2NkkEiZHNCs/MG34E4=",
        "palm:sandboxName": "prod"
    }
}
```

| 属性 | 描述 |
| --- | --- |
| `$id` | 系統產生的新欄位群組唯讀唯一識別碼。 採用URI的形式。 |

{style="table-layout:auto"}

記錄 `$id` 欄位群組的URI，用於下一步將欄位群組新增至來源結構描述中。

### 將欄位群組新增至來源結構描述

建立欄位群組後，您可以透過向以下專案發出PATCH請求，將其新增到來源結構描述： `/tenant/schemas/{SCHEMA_ID}` 端點。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼 `$id` URI或 `meta:altId` 來源結構描述的。 |

{style="table-layout:auto"}

**请求**

以下請求新增「[!DNL Favorite Hotel]「 」欄位群組到「[!DNL Loyalty Members]「結構描述。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    { 
      "op": "add", 
      "path": "/allOf/-", 
      "value":  {
        "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
      }
    }
  ]'
```

| 属性 | 描述 |
| --- | --- |
| `op` | 要執行的PATCH操作。 此請求會使用 `add` 作業。 |
| `path` | 將新增新資源的結構描述欄位的路徑。 將欄位群組新增至結構描述時，值必須是&quot;/allOf/-&quot;。 |
| `value.$ref` | 此 `$id` 欄位群組的欄位名稱。 |

{style="table-layout:auto"}

**响应**

成功回應會傳回更新結構的詳細資訊，現在包含 `$ref` 在其下新增的欄位群組的值 `allOf` 陣列。

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
    "meta:resourceType": "schemas",
    "version": "1.1",
    "type": "object",
    "title": "Loyalty Members",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
        }
    ],
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:tenantNamespace": "_{TENANT_ID}",
    "imsOrg": "{ORG_ID}",
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3",
        "https://ns.adobe.com/{TENANT_ID}/mixins/61969bc646b66a6230a7e8840f4a4d33"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557525483804,
        "repo:lastModifiedDate": 1566419670915,
        "xdm:createdClientId": "{API_KEY}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "eTag": "ITNzu8BVTO5pw9wfCtTTpk6U4WY="
    }
}
```

## 建立參考身分描述項 {#reference-identity}

如果結構描述欄位用作關係中另一個結構描述的參考，則必須對其套用參考身分描述項。 由於 `favoriteHotel` 「」中的欄位[!DNL Loyalty Members]」將指 `hotelId` 「」中的欄位[!DNL Hotels]&quot;， `favoriteHotel` 必須為參考身分描述項指定名稱。

透過向以下專案發出POST請求，為來源結構描述建立參考描述項： `/tenant/descriptors` 端點。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下請求會建立 `favoriteHotel` 來源結構描述中的欄位&quot;[!DNL Loyalty Members]「。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| 参数 | 描述 |
| --- | --- |
| `@type` | 正在定義的描述項型別。 參考描述項的值必須是 `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | 此 `$id` 來源結構的URL。 |
| `xdm:sourceVersion` | 來源結構描述的版本號碼。 |
| `sourceProperty` | 來源結構描述中用於引用參考結構描述主要身分的欄位路徑。 |
| `xdm:identityNamespace` | 參考欄位的身分名稱空間。 此名稱空間必須與參考結構描述的主要身分相同。 請參閱 [身分名稱空間總覽](../../identity-service/home.md) 以取得詳細資訊。 |

{style="table-layout:auto"}

**响应**

成功的回應會傳回來源欄位新建立的參考描述項的詳細資訊。

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## 建立關係描述項 {#create-descriptor}

關係描述元在來源結構描述和參考結構描述之間建立一對一的關係。 一旦您在來源結構描述中定義了適當欄位的參考身分描述項，您就可以透過向以下專案發出POST請求來建立新的關係描述項： `/tenant/descriptors` 端點。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下請求會建立具有「」的新關係描述項[!DNL Loyalty Members]&quot;作為來源結構描述和&quot;[!DNL Hotels]」作為參考結構描述。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId"
  }'
```

| 参数 | 描述 |
| --- | --- |
| `@type` | 要建立的描述項型別。 此 `@type` 關係描述項的值為 `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | 此 `$id` 來源結構的URL。 |
| `xdm:sourceVersion` | 來源結構描述的版本號碼。 |
| `xdm:sourceProperty` | 來源結構描述中參考欄位的路徑。 |
| `xdm:destinationSchema` | 此 `$id` 參考結構描述的URL。 |
| `xdm:destinationVersion` | 參考結構描述的版本號碼。 |
| `xdm:destinationProperty` | 參考結構描述中主要身分欄位的路徑。 |

{style="table-layout:auto"}

### 响应

成功的回應會傳回新建立的關係描述項的詳細資料。

```json
{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId",
    "meta:containerId": "tenant",
    "@id": "76f6cc7105f4eaab7eb4a5e1cb4804cadc741669"
}
```

## 后续步骤

依照本教學課程，您已成功建立兩個結構描述之間的一對一關係。 如需有關使用描述元的詳細資訊，請參閱 [!DNL Schema Registry] API，請參閱 [Schema Registry開發人員指南](../api/descriptors.md). 如需如何在UI中定義結構描述關係的步驟，請參閱以下教學課程： [使用結構描述編輯器定義結構描述關係](relationship-ui.md).

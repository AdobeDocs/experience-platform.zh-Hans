---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；結構描述登入；結構描述登入；描述項；描述項；描述項；描述項；身分；身分；易記名稱；易記名稱；alternatedisplayinfo；參考；參考；關係；關係
solution: Experience Platform
title: 描述項API端點
description: Schema Registry API中的/descriptors端點可讓您以程式設計方式管理體驗應用程式中的XDM描述項。
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1872'
ht-degree: 1%

---

# 描述項端點

結構描述會定義資料實體的靜態檢視，但不會提供基於這些結構描述（例如資料集）的資料如何彼此關聯的特定詳細資訊。 Adobe Experience Platform可讓您使用描述項描述這些關係以及有關結構描述的其他解釋性中繼資料。

結構描述項是租使用者層級的中繼資料，這表示它們對於您的組織是唯一的，並且所有描述項作業都在租使用者容器中進行。

每個結構描述可以套用一或多個結構描述項實體。 每個結構描述項實體都包含一個描述項 `@type` 和 `sourceSchema` 要套用到的屬性。 套用後，這些描述項將套用至使用該結構描述建立的所有資料集。

此 `/descriptors` 中的端點 [!DNL Schema Registry] API可讓您以程式設計方式管理體驗應用程式中的描述項。

## 快速入门

本指南中使用的端點是 [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). 在繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案範例API呼叫的閱讀指南，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

## 擷取描述項清單 {#list}

您可以透過向以下發出GET要求，列出貴組織已定義的所有描述項： `/tenant/descriptors`.

**API格式**

```http
GET /tenant/descriptors
```

**请求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

回應格式取決於 `Accept` 標頭已在請求中傳送。 請注意 `/descriptors` 端點使用 `Accept` 與中所有其他端點不同的標頭 [!DNL Schema Registry] API。

>[!IMPORTANT]
>
>描述項需要唯一 `Accept` 取代的標頭 `xed` 替換為 `xdm`，也提供 `link` 描述項獨有的選項。 適當的 `Accept` 標頭已包含在以下的範例呼叫中，但請格外小心，以確保在使用描述項時使用正確的標頭。

| `Accept` 頁首 | 描述 |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | 傳回描述項ID的陣列 |
| `application/vnd.adobe.xdm-link+json` | 傳回描述項API路徑的陣列 |
| `application/vnd.adobe.xdm+json` | 傳回擴充描述項物件的陣列 |
| `application/vnd.adobe.xdm-v2+json` | 此 `Accept` 必須使用頁首才能使用分頁功能。 |

{style="table-layout:auto"}

**响应**

此回應包含已定義描述項的每個描述項型別的陣列。 換言之，如果沒有特定的 `@type` 定義，登入將不會傳回該描述項型別的空白陣列。

使用時 `link` `Accept` 標題，每個描述項都會以格式顯示為陣列專案 `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

```JSON
{
  "xdm:alternateDisplayInfo": [
    "/tenant/descriptors/85dc1bc8b91516ac41163365318e38a9f1e4f351",
    "/tenant/descriptors/49bd5abb5a1310ee80ebc1848eb508d383a462cf",
    "/tenant/descriptors/b3b3e548f1c653326bcf5459ceac4140fc0b9e08"
  ],
  "xdm:descriptorIdentity": [
    "/tenant/descriptors/f7a4bc25429496c4740f8f9a7a49ba96862c5379"
  ],
  "xdm:descriptorOneToOne": [
    "/tenant/descriptors/cb509fd6f8ab6304e346905441a34b58a0cd481a"
  ]
}
```

## 查詢描述項 {#lookup}

如果您想要檢視特定描述項的詳細資訊，可以使用其來查詢(GET)個別描述項 `@id`.

**API格式**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 此 `@id` 要查閱的描述項的ID。 |

{style="table-layout:auto"}

**请求**

以下請求會依照其擷取描述項 `@id` 值。 描述項不會建立版本，因此不會 `Accept` 查詢請求中需要標頭。

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回描述項的詳細資訊，包括其 `@type` 和 `sourceSchema`以及視描述項型別而異的其他資訊。 傳回的 `@id` 應該符合描述項 `@id` 要求中提供。

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "createdUser": "{CREATED_USER}",
  "imsOrg": "{ORG_ID}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 建立描述項 {#create}

您可以向以下網址發出POST要求，以建立新的描述項： `/tenant/descriptors` 端點。

>[!IMPORTANT]
>
>此 [!DNL Schema Registry] 可讓您定義數種不同的描述項型別。 每個描述項型別都需要有專屬的特定欄位，才能在要求內文中傳送。 請參閱 [附錄](#defining-descriptors) 取得描述元的完整清單，以及定義描述元所需的欄位。

**API格式**

```http
POST /tenant/descriptors
```

**请求**

以下請求在範例結構描述中的「電子郵件地址」欄位上定義身分描述項。 這說明 [!DNL Experience Platform] 將電子郵件地址當作識別碼，以協助彙整個人的相關資訊。

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**响应**

成功的回應會傳回HTTP狀態201 （已建立）和新建立之描述項的詳細資訊，包括其 `@id`. 此 `@id` 是由指派的唯讀欄位 [!DNL Schema Registry] 和用於參考API中的描述項。

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 更新描述項 {#put}

您可以包含描述項來更新描述項 `@id` 在PUT請求的路徑中。

**API格式**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 此 `@id` 要更新的描述項。 |

{style="table-layout:auto"}

**请求**

此請求基本上會重新寫入描述項，因此請求內文必須包含定義該型別描述項所需的所有欄位。 換言之，更新(PUT)描述項的要求裝載與的裝載相同 [建立(POST)描述項](#create) 相同型別。

>[!IMPORTANT]
>
>如同使用POST要求建立描述項一樣，每個描述項型別都需要在PUT要求裝載中傳送其專屬的特定欄位。 請參閱 [附錄](#defining-descriptors) 取得描述元的完整清單，以及定義描述元所需的欄位。

以下範例會更新身分描述項以參考不同的身分 `xdm:sourceProperty` (`mobile phone`)並變更 `xdm:namespace` 至 `Phone`.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/mobilePhone/number",
        "xdm:namespace": "Phone",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**响应**

成功的回應會傳回HTTP狀態201 （已建立），並且 `@id` 更新描述項的(應比對 `@id` （以請求傳送）。

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

執行 [查詢(GET)請求](#lookup) 若要檢視描述項，將顯示欄位現在已更新，以反映PUT請求中傳送的變更。

## 刪除描述項 {#delete}

有時候，您可能需要從以下位置移除已定義的描述項： [!DNL Schema Registry]. 這可透過參考「 」的「 」DELETE請求來完成 `@id` 要移除的描述項。

**API格式**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| 参数 | 描述 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 此 `@id` 個要刪除的描述項。 |

{style="table-layout:auto"}

**请求**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**响应**

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。

若要確認描述項已刪除，您可以執行 [查詢請求](#lookup) 針對描述項 `@id`. 回應會傳回HTTP狀態404 （找不到），因為描述項已從 [!DNL Schema Registry].

## 附录

下節提供有關在中使用描述項的其他資訊 [!DNL Schema Registry] API。

### 定義描述項 {#defining-descriptors}

以下小節提供可用描述項型別的概覽，包括定義每種型別描述項所需的欄位。

#### 身分描述項

身分描述項會指出「[!UICONTROL sourceProperty]的「」[!UICONTROL sourceSchema]「是 [!DNL Identity] 欄位，如所述 [Adobe Experience Platform Identity Service](../../identity-service/home.md).

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false
}
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 正在定義的描述項型別。 對於身分描述項，此值必須設定為 `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | 此 `$id` 正在定義描述項的結構描述的URI。 |
| `xdm:sourceVersion` | 來源結構描述的主要版本。 |
| `xdm:sourceProperty` | 將成為身分的特定屬性的路徑。 路徑應該以「/」開頭，而不是以一個結尾。 不要在路徑中包含「properties」（例如，使用「/personalEmail/address」而不是「/properties/personalEmail/properties/address」） |
| `xdm:namespace` | 此 `id` 或 `code` 身分名稱空間的值。 名稱空間清單可透過以下網址找到： [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service). |
| `xdm:property` | 兩者之一 `xdm:id` 或 `xdm:code`，取決於 `xdm:namespace` 已使用。 |
| `xdm:isPrimary` | 選用的布林值。 為true時，會將該欄位表示為主要身分。 結構描述只能包含一個主要身分。 |

{style="table-layout:auto"}

#### 易記名稱描述項 {#friendly-name}

易記名稱描述項可讓使用者修改 `title`， `description`、和 `meta:enum` 核心程式庫結構描述欄位的值。 使用「eVars」和其他「一般」欄位時，如果想要標示為包含貴組織的特定資訊，這個功能會特別有用。 UI可以使用這些來顯示更好記的名稱，或只顯示具有更好記名稱的欄位。

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:title": {
    "en_us": "Event Type"
  },
  "xdm:description": {
    "en_us": "The type of experience event detected by the system."
  },
  "meta:enum": {
    "click": "Mouse Click",
    "addCart": "Add to Cart",
    "checkout": "Cart Checkout"
  },
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out",
    "media.ping": "Media ping"
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 正在定義的描述項型別。 對於易記名稱描述項，此值必須設定為 `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | 此 `$id` 正在定義描述項的結構描述的URI。 |
| `xdm:sourceVersion` | 來源結構描述的主要版本。 |
| `xdm:sourceProperty` | 您要修改其詳細資訊之特定屬性的路徑。路徑應該以斜線(`/`)且結尾不是1。 不包括 `properties` 在路徑中(例如，使用 `/personalEmail/address` 而非 `/properties/personalEmail/properties/address`)。 |
| `xdm:title` | 您要為此欄位顯示的新標題，以「字首大寫」撰寫。 |
| `xdm:description` | 可選擇在標題中新增說明。 |
| `meta:enum` | 如果欄位指示為 `xdm:sourceProperty` 是字串欄位， `meta:enum` 可用來在分段UI中新增欄位的建議值。 請務必注意 `meta:enum` 不會為XDM欄位宣告分項清單或提供任何資料驗證。<br><br>這僅能用於Adobe定義的核心XDM欄位。 如果來源屬性是您的組織定義的自訂欄位，您應改為編輯欄位的 `meta:enum` 屬性直接透過PATCH要求傳遞至欄位的父資源。 |
| `meta:excludeMetaEnum` | 如果欄位指示為 `xdm:sourceProperty` 是字串欄位，其下提供了現有的建議值。 `meta:enum` 欄位，您可以在易記名稱描述項中包含此物件，從區段中排除部分或全部這些值。 每個專案的索引鍵和值都必須符合原始專案中所包含的索引鍵和值 `meta:enum` 欄位的URL來排除輸入。 |

{style="table-layout:auto"}

#### 關係描述項

關係描述項說明兩個不同結構描述之間的關係，其關鍵字為中所述的屬性 `sourceProperty` 和 `destinationProperty`. 請參閱教學課程，位置如下： [定義兩個結構描述之間的關係](../tutorials/relationship-api.md) 以取得詳細資訊。

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": 
    "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 正在定義的描述項型別。 對於關係描述項，此值必須設定為 `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | 此 `$id` 正在定義描述項的結構描述的URI。 |
| `xdm:sourceVersion` | 來源結構描述的主要版本。 |
| `xdm:sourceProperty` | 定義關係的來源結構描述中欄位的路徑。 應該以「/」開頭，而不是以開頭。 請勿在路徑中加入「properties」（例如，「/personalEmail/address」而非「/properties/personalEmail/properties/address」）。 |
| `xdm:destinationSchema` | 此 `$id` 此描述項正在定義關係的參考結構描述的URI。 |
| `xdm:destinationVersion` | 參考結構描述的主要版本。 |
| `xdm:destinationProperty` | 參考結構描述中目標欄位的可選路徑。 如果省略此屬性，則包含相符參考身分描述項的任何欄位都會推斷目標欄位（請參閱下文）。 |

{style="table-layout:auto"}

#### 參考身分描述項

參考身分描述項提供結構描述欄位主要身分的參考內容，以供其他結構描述中的欄位參考。 參考結構描述必須先定義主要身分欄位，其他結構描述才能透過此描述項參考參考它。

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:identityNamespace": "Email"
}
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 正在定義的描述項型別。 對於參考身分描述項，此值必須設定為 `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | 此 `$id` 正在定義描述項的結構描述的URI。 |
| `xdm:sourceVersion` | 來源結構描述的主要版本。 |
| `xdm:sourceProperty` | 來源結構描述中用於參考結構描述的欄位路徑。 應該以「/」開頭，而不是以開頭。 請勿在路徑中包含「properties」(例如， `/personalEmail/address` 而非 `/properties/personalEmail/properties/address`)。 |
| `xdm:identityNamespace` | 來源屬性的身分名稱空間代碼。 |

{style="table-layout:auto"}

#### 已棄用的欄位描述項

您可以 [棄用自訂XDM資源中的欄位](../tutorials/field-deprecation-api.md#custom) 藉由新增 `meta:status` 屬性設定為 `deprecated` 至有問題的欄位。 不過，如果您想要取代結構描述中標準XDM資源提供的欄位，您可以將取代的欄位描述項指派給有問題的結構描述，以達到相同的效果。 使用 [正確 `Accept` 頁首](../tutorials/field-deprecation-api.md#verify-deprecation)，則在API中查詢結構描述時，您可以檢視哪些標準欄位已過時。

```json
{
  "@type": "xdm:descriptorDeprecated",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/faxPhone"
}
```

| 属性 | 描述 |
| --- | --- |
| `@type` | 描述項的型別。 對於欄位淘汰描述項，此值必須設定為 `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | URI `$id` 要套用描述項的結構描述中。 |
| `xdm:sourceVersion` | 您要套用描述項的結構描述版本。 應設為 `1`. |
| `xdm:sourceProperty` | 要套用描述項的結構描述中的屬性路徑。 如果您想要將描述項套用至多個屬性，可以陣列形式提供路徑清單(例如， `["/firstName", "/lastName"]`)。 |

{style="table-layout:auto"}

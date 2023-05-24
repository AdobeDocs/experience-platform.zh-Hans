---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；xdm；體驗資料模型；名稱空間；名稱空間；相容性模式；xed；
solution: Experience Platform
title: Experience Data Model (XDM)中的名稱空間
description: 瞭解Experience Data Model (XDM)中的名稱空間如何讓您擴充結構描述，並在不同結構描述元件彙整時防止欄位衝突。
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: edd285c3d0638b606876c015dffb18309887dfb5
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# Experience Data Model (XDM)中的名稱空間

Experience Data Model (XDM)結構描述中的所有欄位都有關聯的名稱空間。 這些名稱空間可讓您擴充結構描述，並在不同結構描述元件彙整時防止欄位衝突。 本檔案概述XDM中的名稱空間，以及這些名稱空間在 [結構描述登入API](../api/overview.md).

名稱空間可讓您在一個名稱空間中定義欄位，以表示與不同名稱空間中相同欄位不同的內容。 實際上，欄位的名稱空間會指出建立欄位的人員(例如標準XDM (Adobe)、廠商或您的組織)。

例如，假設某個XDM結構描述使用 [[!UICONTROL 個人聯絡詳細資訊] 欄位群組](../field-groups/profile/demographic-details.md)，此版本含有標準 `mobilePhone` 存在於中的欄位 `xdm` 名稱空間。 在同一個結構描述中，您也可以自行建立個別的 `mobilePhone` 不同名稱空間下的欄位(您的 [租使用者ID](../api/getting-started.md#know-your-tenant_id))。 這兩個欄位可以共存，但具有不同的基本含義或限制。

## 名稱空間語法

以下章節示範如何以XDM語法指派名稱空間。

### 標準XDM {#standard}

標準XDM語法可讓您深入瞭解名稱空間在結構描述中的呈現方式(包括 [如何在Adobe Experience Platform中翻譯它們](#compatibility))。

標準XDM使用 [JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts) 指派名稱空間至欄位的語法。 此名稱空間採用URI的形式(例如 `https://ns.adobe.com/xdm` 的 `xdm` 名稱空間)，或是在下列位置設定的速記首碼： `@context` 結構描述的屬性。

以下是標準XDM語法中產品的結構描述範例。 以下專案除外： `@id` （由JSON-LD規格定義的唯一識別碼），下方的每個欄位 `properties` 以名稱空間開頭並以欄位名稱結尾。 如果使用下定義的速記首碼 `@context`，名稱空間和欄位名稱會以冒號(`:`)。 如果不使用首碼，則名稱空間和欄位名稱會以斜線(`/`)。

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "@context": {
    "xdm": "https://ns.adobe.com/xdm",
    "repo": "http://ns.adobe.com/adobecloud/core/1.0/",
    "schema": "http://schema.org",
    "tenantId": "https://ns.adobe.com/tenantId"
  },
  "properties": {
    "@id": {
      "type": "string"
    },
    "xdm:sku": {
      "type": "string"
    },
    "xdm:name": {
      "type": "string"
    },
    "repo:createdDate": {
      "type": "string",
      "format": "datetime"
    },
    "https://ns.adobe.com/xdm/channels/application": {
      "type": "string"
    },
    "schema:latitude": {
      "type": "number"
    },
    "https://ns.adobe.com/vendorA/product/stockNumber": {
      "type": "string"
    },
    "tenantId:internalSku": {
      "type": "number"
    }
  }
}
```

| 属性 | 描述 |
| --- | --- |
| `@context` | 一個物件，定義可以使用的速記首碼，而不是底下的完整名稱空間URI `properties`. |
| `@id` | 記錄的唯一識別碼，由 [JSON-LD規格](https://www.w3.org/TR/json-ld11/#node-identifiers). |
| `xdm:sku` | 使用速記首碼表示名稱空間的欄位範例。 在這種情況下， `xdm` 是名稱空間(`https://ns.adobe.com/xdm`)，以及 `sku` 是欄位名稱。 |
| `https://ns.adobe.com/xdm/channels/application` | 使用完整名稱空間URI的欄位範例。 在這種情況下， `https://ns.adobe.com/xdm/channels` 是名稱空間，且 `application` 是欄位名稱。 |
| `https://ns.adobe.com/vendorA/product/stockNumber` | 廠商資源提供的欄位會使用其專屬的名稱空間。 在此範例中， `https://ns.adobe.com/vendorA/product` 是廠商名稱空間，而且 `stockNumber` 是欄位名稱。 |
| `tenantId:internalSku` | 貴組織定義的欄位會使用您的唯一租使用者ID作為其名稱空間。 在此範例中， `tenantId` 是租使用者名稱空間(`https://ns.adobe.com/tenantId`)，以及 `internalSku` 是欄位名稱。 |

{style="table-layout:auto"}

### 相容性模式 {#compatibility}

在Adobe Experience Platform中，XDM結構描述會顯示在 [相容性模式](../api/appendix.md#compatibility) 語法，不會使用JSON-LD語法來表示名稱空間。 Platform會將名稱空間轉換為父欄位（以底線開頭），並將欄位巢狀在其下。

例如，標準XDM `repo:createdDate` 已轉換為 `_repo.createdDate` 和會顯示在「相容性模式」的下列結構下：

```json
"_repo": {
  "type": "object",
  "properties": {
    "createdDate": {
      "type": "string",
      "format": "datetime"
    }
  }
}
```

使用 `xdm` 名稱空間會顯示為下的根欄位 `properties` 並放置 `xdm:` 前置詞： [標準XDM語法](#standard). 例如， `xdm:sku` 只會列為 `sku` 而非。

以下JSON代表如何將以上所示的標準XDM語法範例轉譯為相容性模式。

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "properties": {
    "_id": {
      "type": "string"
    },
    "sku": {
      "type": "string"
    },
    "name": {
      "type": "string"
    },
    "_repo": {
      "type": "object",
      "properties": {
        "createdDate": {
          "type": "string",
          "format": "datetime"
        }
      }
    },
    "_channels": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_schema": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_vendorA": {
      "type": "object",
      "properties": {
        "product": {
          "type": "object",
          "properties": {
            "stockNumber": {
              "type": "string"
            }
          }
        }
      }
    },
    "_tenantId": {
      "type": "object",
      "properties": {
        "internalSku": {
          "type": "number"
        }
      }
    }
  }
}
```

## 后续步骤

本指南概述XDM名稱空間及其在JSON中的呈現方式。 如需有關如何使用API設定XDM結構的詳細資訊，請參閱 [Schema Registry API指南](../api/overview.md).

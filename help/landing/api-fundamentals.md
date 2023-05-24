---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: Experience PlatformAPI基礎知識
description: 本檔案簡要概述Experience Platform API相關的基礎技術和語法。
exl-id: cd69ba48-f78c-4da5-80d1-efab5f508756
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 1%

---

# Experience PlatformAPI基礎知識

Adobe Experience Platform API運用了幾項重要的基礎技術和語法，以便有效管理JSON型 [!DNL Platform] 資源。 本檔案提供這些技術的簡短概觀，以及外部檔案的連結以取得詳細資訊。

## JSON指標 {#json-pointer}

JSON指標是標準化的字串語法([RFC 6901](https://tools.ietf.org/html/rfc6901))以識別JSON檔案內的特定值。 JSON指標是權杖的字串，以 `/` 字元，指定物件索引鍵或陣列索引，而代號可以是字串或數字。 JSON指標字串用於許多PATCH操作 [!DNL Platform] API，如本檔案稍後所述。 如需JSON指標的詳細資訊，請參閱 [JSON指標概觀檔案](https://rapidjson.org/md_doc_pointer.html).

### 範例JSON結構描述物件

以下JSON代表簡化的XDM結構描述，其欄位可使用JSON指標字串參照。 請注意，已使用自訂結構描述欄位群組新增的所有欄位(例如 `loyaltyLevel`)的名稱空間 `_{TENANT_ID}` 物件，而使用核心欄位群組(例如 `fullName`)則否。

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:altId": "_{TENANT_ID}.schemas.85a4bdaa168b01bf44384e049fbd3d2e9b2ffaca440d35b9",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Example schema",
  "type": "object",
  "description": "This is an example schema.",
  "properties": {
    "_{TENANT_ID}": {
      "type": "object",
      "properties": {
        "loyaltyLevel": {
          "title": "Loyalty Level",
          "description": "",
          "type": "string",
          "isRequired": false,
          "enum": [
            "platinum",
            "gold",
            "silver",
            "bronze"
          ]
        }
      }
    },
    "person": {
      "title": "Person",
      "description": "An individual actor, contact, or owner.",
      "type": "object",
      "properties": {
        "name": {
          "title": "Full name",
          "description": "The person's full name.",
          "type": "object",
          "properties": {
            "fullName": {
              "title": "Full name",
              "type": "string",
              "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
            },
            "suffix": {
              "title": "Suffix",
              "type": "string",
              "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
          "meta:xdmField": "xdm:name"
        }
      }
    }
  }
}
```

### 根據結構描述物件的JSON指標範例

| JSON指標 | 解析為 |
| --- | --- |
| `"/title"` | `"Example schema"` |
| `"/properties/person/properties/name/properties/fullName"` | (傳回對的參照 `fullName` 欄位，由核心欄位群組提供。) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel"` | (傳回對的參照 `loyaltyLevel` 欄位，由自訂欄位群組提供。) |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum"` | `["platinum", "gold", "silver", "bronze"]` |
| `"/properties/_{TENANT_ID}/properties/loyaltyLevel/enum/0"` | `"platinum"` |

>[!NOTE]
>
>處理 `xdm:sourceProperty` 和 `xdm:destinationProperty` 屬性 [!DNL Experience Data Model] (XDM)描述項，任何 `properties` 金鑰必須是 **已排除** 從JSON指標字串。 請參閱 [!DNL Schema Registry] API開發人員指南子指南，於 [描述項](../xdm/api/descriptors.md) 以取得詳細資訊。

## JSON修補程式 {#json-patch}

有許多針對的PATCH操作 [!DNL Platform] 接受JSON修補程式物件請求裝載的API。 JSON修補程式為標準化格式([RFC 6902](https://tools.ietf.org/html/rfc6902))以說明JSON檔案的變更。 它可讓您定義JSON的部分更新，而無需在請求本文中傳送整個檔案。

### 範例JSON修補程式物件

```json
{
  "op": "remove",
  "path": "/foo"
}
```

* `op`：修補程式操作的型別。 雖然JSON修補程式支援數種不同的操作型別，但並非所有PATCH操作都適用於 [!DNL Platform] API與每個操作型別都相容。 可用的作業型別包括：
   * `add`
   * `remove`
   * `replace`
   * `copy`
   * `move`
   * `test`
* `path`：要更新的JSON結構部分，識別方式為 [JSON指標](#json-pointer) 表示法。

視中指定的作業型別而定 `op`，則JSON修補程式物件可能需要其他屬性。 如需不同JSON修補程式操作及其所需語法的詳細資訊，請參閱 [JSON修補程式檔案](https://datatracker.ietf.org/doc/html/rfc6902).

## JSON結構描述 {#json-schema}

JSON結構描述是用於說明和驗證JSON資料結構的格式。 [體驗資料模型(XDM)](../xdm/home.md) 運用JSON結構描述功能，對擷取的客戶體驗資料的結構和格式強制執行限制。 如需JSON結構描述的詳細資訊，請參閱 [正式檔案](https://json-schema.org/).

## 后续步骤

本檔案介紹了管理JSON型資源的相關技術和語法，針對 [!DNL Experience Platform]. 請參閱 [快速入門手冊](api-guide.md) 以取得有關使用Platform API的詳細資訊，包括最佳實務。 如需常見問題的解答，請參閱 [平台疑難排解指南](troubleshooting.md).

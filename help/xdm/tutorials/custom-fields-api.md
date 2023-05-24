---
title: 在結構描述登入API中定義XDM欄位
description: 瞭解如何在Schema Registry API中建立自訂Experience Data Model (XDM)資源時定義不同的欄位。
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# 在結構描述登入API中定義XDM欄位

所有體驗資料模型(XDM)欄位都是使用標準來定義 [JSON結構描述](https://json-schema.org/) 適用於其欄位型別的限制，以及Adobe Experience Platform強制執行的欄位名稱的其他限制。 Schema Registry API可讓您透過使用格式和選用限制來定義結構中的自訂欄位。 XDM欄位型別會由欄位層級屬性公開， `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` 是系統產生的值，因此使用API時不需要將此屬性新增到欄位的JSON （使用API時除外） [建立自訂地圖型別](#custom-maps))。 最佳實務是使用JSON結構描述型別(例如 `string` 和 `integer`)，並具備下表所定義的適當最小值/最大值限制。

本指南會概述定義不同欄位型別的適當格式，包括具選擇性屬性的欄位型別。 有關可選屬性和型別特定關鍵字的更多資訊，請參閱 [JSON結構描述檔案](https://json-schema.org/understanding-json-schema/reference/type.html).

若要開始，請尋找所需的欄位型別，並使用提供的範常式式碼來建置您的API請求 [建立欄位群組](../api/field-groups.md#create) 或 [建立資料型別](../api/data-types.md#create).

## [!UICONTROL 字符串] {#string}

[!UICONTROL 字符串] 欄位表示方式 `type: string`.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

您可選擇透過下列其他屬性，來限制可為字串輸入哪些型別的值：

* `pattern`：限制所依據的規則運算式模式。
* `minLength`：字串的最小長度。
* `maxLength`：字串的長度上限。

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field with added constraints.",
  "type": "string",
  "pattern": "^[A-Z]{2}$",
  "maxLength": 2
}
```

## [!UICONTROL URI] {#uri}

[!UICONTROL URI] 欄位表示方式 `type: string` 搭配 `format` 屬性設定為 `uri`. 不接受任何其他屬性。

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL 列舉] {#enum}

[!UICONTROL 列舉] 欄位必須使用 `type: string`，而列舉值本身則提供在 `enum` 陣列：

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ]
}
```

您可以選擇性地為下的每個值提供面對客戶的標籤 `meta:enum` 屬性，每個標籤都標示為底下的對應值 `enum`.

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum": {
      "value1": "Value 1",
      "value2": "Value 2",
      "value3": "Value 3"
  }
}
```

>[!NOTE]
>
>此 `meta:enum` 值會 **not** 自行宣告分項清單或驅動任何資料驗證。 在大多數情況下，字串提供於 `meta:enum` 也提供於 `enum` 以確保資料受到限制。 不過，有些使用案例會 `meta:enum` 提供，但不提供對應的 `enum` 陣列。 請參閱教學課程，位置如下： [定義建議值](../tutorials/suggested-values.md) 以取得詳細資訊。

您可以選擇提供 `default` 屬性以表示預設值 `enum` 如果未提供值，則欄位將使用的值。

```json
"sampleField": {
  "title": "Sample Enum Field",
  "description": "An example enum field with customer-facing labels and a default value.",
  "type": "string",
  "enum": [
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum": {
      "value1": "Value 1",
      "value2": "Value 2",
      "value3": "Value 3"
  },
  "default": "value1"
}
```

>[!IMPORTANT]
>
>若否 `default` 會提供值，且列舉欄位會設為 `required`，任何遺失此欄位可接受值的記錄將在擷取時驗證失敗。

## [!UICONTROL 数值] {#number}

數字欄位表示為 `type: number` 且沒有其他必要屬性。

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` 型別適用於任何數值型別，可以是整數或浮點數，而 [`integer` 型別](#integer) 專門用於整數值。 請參閱 [有關數值型別的JSON結構描述檔案](https://json-schema.org/understanding-json-schema/reference/numeric.html) 如需每種型別使用案例的詳細資訊。

## [!UICONTROL 整数] {#integer}

[!UICONTROL 整數] 欄位表示方式 `type: integer` 且沒有其他必要欄位。

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>當 `integer` 型別是指整數值， [`number` 型別](#number) 用於任何數值型別，可以是整數或浮點數。 請參閱 [有關數值型別的JSON結構描述檔案](https://json-schema.org/understanding-json-schema/reference/numeric.html) 如需每種型別使用案例的詳細資訊。

您可以選擇透過新增來限制整數的範圍 `minimum` 和 `maximum` 屬性至定義。 結構描述產生器UI支援的其他數位型別包括 `integer` 具有特定的 `minimum` 和 `maximum` 限制，例如 [[!UICONTROL 長]](#long)， [[!UICONTROL 短]](#short)、和 [[!UICONTROL 位元組]](#byte).

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field with added constraints.",
  "type": "integer",
  "minimum": 1,
  "maximum": 100
}
```

## [!UICONTROL 長] {#long}

相當於 [!UICONTROL 長] 透過結構描述產生器UI建立的欄位是 [`integer` 型別欄位](#integer) 具有特定 `minimum` 和 `maximum` 值(`-9007199254740992` 和 `9007199254740992`（分別）。

```json
"sampleField": {
  "title": "Sample Long Field",
  "description": "An example long field.",
  "type": "integer",
  "minimum": -9007199254740992,
  "maximum": 9007199254740992
}
```

## [!UICONTROL 短] {#short}

相當於 [!UICONTROL 短] 透過結構描述產生器UI建立的欄位是 [`integer` 型別欄位](#integer) 具有特定 `minimum` 和 `maximum` 值(`-32768` 和 `32768`（分別）。

```json
"sampleField": {
  "title": "Sample Short Field",
  "description": "An example short field.",
  "type": "integer",
  "minimum": -32768,
  "maximum": 32768
}
```

## [!UICONTROL 位元組] {#byte}

相當於 [!UICONTROL 位元組] 透過結構描述產生器UI建立的欄位是 [`integer` 型別欄位](#integer) 具有特定 `minimum` 和 `maximum` 值(`-128` 和 `128`（分別）。

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 128
}
```

## [!UICONTROL 布尔型] {#boolean}

[!UICONTROL 布林值] 欄位表示方式 `type: boolean`.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

您可以選擇提供 `default` 擷取期間未提供明確值時，欄位將使用的值。

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field with a default value.",
  "type": "boolean",
  "default": false
}
```

>[!IMPORTANT]
>
>若否 `default` 會提供值，而布林值欄位會設為 `required`，任何遺失此欄位可接受值的記錄將在擷取時驗證失敗。

## [!UICONTROL 日期] {#date}

[!UICONTROL 日期] 欄位表示方式 `type: string` 和 `format: date`. 您也可以選擇提供陣列 `examples` 若您想要為手動輸入資料的使用者顯示範例日期字串，請善用此選項。

```json
"sampleField": {
  "title": "Sample Date Field",
  "description": "An example date field with an example array item.",
  "type": "string",
  "format": "date",
  "examples": ["2004-10-23"]
}
```

## [!UICONTROL 日期時間] {#date-time}

[!UICONTROL 日期時間] 欄位表示方式 `type: string` 和 `format: date-time`. 您也可以選擇提供陣列 `examples` 若您想要為手動輸入資料的使用者顯示範例日期時間字串，請善用此選項。

```json
"sampleField": {
  "title": "Sample Datetime Field",
  "description": "An example datetime field with an example array item.",
  "type": "string",
  "format": "date-time",
  "examples": ["2004-10-23T12:00:00-06:00"]
}
```

## [!UICONTROL 陣列] {#array}

[!UICONTROL 陣列] 欄位表示方式 `type: array` 和 `items` 物件，定義陣列將接受之專案的結構描述。

您可以使用基本型別（例如字串陣列）來定義陣列專案：

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a primitive type.",
  "type": "array",
  "items": {
    "type": "string"
  }
}
```

您也可以參考 `$id` 透過 `$ref` 屬性。 以下是以下陣列 [!UICONTROL 付款專案] 物件：

```json
"sampleField": {
  "title": "Sample Array Field",
  "description": "An example array field using a data type reference.",
  "type": "array",
  "items": {
    "$ref": "https://ns.adobe.com/xdm/data/paymentitem"
  }
}
```

## [!UICONTROL 对象] {#object}

[!UICONTROL 物件] 欄位表示方式 `type: object` 和 `properties` 定義結構描述欄位之子屬性的物件。

下定義的每個子欄位 `properties` 可使用任何基本值來定義 `type` 或透過 `$ref` 屬性指向 `$id` 有問題的資料型別：

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field.",
  "type": "object",
  "properties": {
    "field1": {
      "type": "string"
    },
    "field2": {
      "$ref": "https://ns.adobe.com/xdm/common/measure"
    }
  }
}
```

您也可以透過參考資料型別來定義整個物件，前提是相關資料型別本身定義為 `type: object`：

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL 地图] {#map}

對應欄位本質上是 [`object`-type欄位](#object) 具有一組未限制的索引鍵。 如同物件，地圖具有 `type` 值 `object`，但其 `meta:xdmType` 明確設定為 `map`.

地圖 **不得** 定義任何屬性。 It **必須** 定義單一 `additionalProperties` 結構描述，說明對應中包含的值型別（每個對應只能包含單一資料型別）。 此 `type` 值必須是 `string` 或 `integer`.

例如，具有字串型別值的對應欄位的定義如下：

```json
"sampleField": {
  "title": "Sample Map Field",
  "description": "An example map field.",
  "type": "object",
  "meta:xdmType": "map",
  "additionalProperties": {
    "type": "string"
  }
}
```

如需建立自訂對應欄位的詳細資訊，請參閱以下章節。

### 建立自訂地圖型別 {#custom-maps}

為了在XDM中有效支援「類似地圖」的資料，物件可能會使用 `meta:xdmType` 設定為 `map` 以清楚說明物件的管理方式應如同金鑰集未受限制一樣。 擷取至對應欄位的資料必須使用字串索引鍵，且只能使用字串或整數值（由決定） `additionalProperties.type`)。

XDM會針對此儲存提示的使用設定下列限制：

* 對應型別必須是型別 `object`.
* 對應型別不能有已定義的屬性（換言之，它們定義「空白」物件）。
* 對應型別必須包括 `additionalProperties.type` 說明可放置在地圖中的值的欄位，可以 `string` 或 `integer`.

請確定您只在絕對必要時才使用對應型別欄位，因為這些欄位具有下列效能缺陷：

* 回應時間來自 [Adobe Experience Platform查詢服務](../../query-service/home.md) 1億筆記錄從3秒降至10秒。
* 地圖必須少於16個索引鍵，否則可能會進一步降低。

Platform使用者介面在擷取對應型別欄位索引鍵的方式上也有限制。 雖然物件型別欄位可以展開，但地圖會顯示為單一欄位。

## 后续步骤

本指南說明如何在API中定義不同的欄位型別。 如需如何格式化XDM欄位型別的詳細資訊，請參閱以下指南： [XDM欄位型別限制](../schema/field-constraints.md).

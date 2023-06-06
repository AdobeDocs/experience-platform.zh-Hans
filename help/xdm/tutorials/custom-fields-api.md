---
title: 在架构注册表API中定义XDM字段
description: 了解在架构注册表API中创建自定义Experience Data Model (XDM)资源时如何定义不同的字段。
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# 在架构注册表API中定义XDM字段

所有体验数据模型(XDM)字段均使用标准进行定义 [JSON架构](https://json-schema.org/) 应用于其字段类型的约束，以及由Adobe Experience Platform实施的字段名称的其他约束。 架构注册表API允许您通过使用格式和可选约束来定义架构中的自定义字段。 XDM字段类型由字段级别属性公开， `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` 是系统生成的值，因此使用API时，无需将此属性添加到字段的JSON中（使用API时除外） [创建自定义映射类型](#custom-maps))。 最佳实践为使用JSON架构类型(例如 `string` 和 `integer`)，具有下表定义的相应最小/最大约束。

本指南概述了定义不同字段类型（包括带有可选属性的字段类型）的相应格式。 有关可选属性和特定类型关键字的更多信息，请参阅 [JSON架构文档](https://json-schema.org/understanding-json-schema/reference/type.html).

要开始，请找到所需的字段类型并使用提供的示例代码为构建API请求 [创建字段组](../api/field-groups.md#create) 或 [创建数据类型](../api/data-types.md#create).

## [!UICONTROL 字符串] {#string}

[!UICONTROL 字符串] 字段由表示 `type: string`.

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

您可以选择通过以下附加属性来限制可以为字符串输入的值的类型：

* `pattern`：要作为约束依据的正则表达式模式。
* `minLength`：字符串的最小长度。
* `maxLength`：字符串的最大长度。

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

[!UICONTROL URI] 字段由表示 `type: string` 带有 `format` 属性设置为 `uri`. 不接受其他属性。

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL 枚举] {#enum}

[!UICONTROL 枚举] 字段必须使用 `type: string`，枚举值本身在 `enum` 数组：

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

您可以选择为下的每个值提供面向客户的标签 `meta:enum` 属性，每个标签均被键入以下项的相应值 `enum`.

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
>此 `meta:enum` 值do **非** 自行声明枚举或驱动任何数据验证。 在大多数情况下，字符串提供在 `meta:enum` 也提供于 `enum` 以确保数据受到约束。 但是，在以下用例中 `meta:enum` 提供时没有相应的 `enum` 数组。 请参阅上的教程 [定义建议值](../tutorials/suggested-values.md) 了解更多信息。

您可以选择提供 `default` 属性以指示默认值 `enum` 如果未提供值，则字段将使用的值。

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
>如果否 `default` 提供了值，并且枚举字段设置为 `required`，则任何缺少此字段的接受值的记录将在摄取时验证失败。

## [!UICONTROL 数值] {#number}

数字字段由表示 `type: number` 且没有其他必需的属性。

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number` 类型用于任何数字类型，可以是整数或浮点数，而 [`integer` 类型](#integer) 专门用于积分数。 请参阅 [有关数字类型的JSON架构文档](https://json-schema.org/understanding-json-schema/reference/numeric.html) 以了解有关每种类型的用例的更多信息。

## [!UICONTROL 整数] {#integer}

[!UICONTROL 整数] 字段由表示 `type: integer` 并且没有其他必填字段。

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>While `integer` 类型是指整数， [`number` 类型](#number) 用于任何数字类型，可以是整数或浮点数。 请参阅 [有关数字类型的JSON架构文档](https://json-schema.org/understanding-json-schema/reference/numeric.html) 以了解有关每种类型的用例的更多信息。

可以选择通过添加以下项来限制整数的范围 `minimum` 和 `maximum` 属性到定义。 架构生成器UI支持的其他几个数字类型只是 `integer` 具有特定的 `minimum` 和 `maximum` 约束，例如 [[!UICONTROL 长]](#long)， [[!UICONTROL 短]](#short)、和 [[!UICONTROL 字节]](#byte).

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field with added constraints.",
  "type": "integer",
  "minimum": 1,
  "maximum": 100
}
```

## [!UICONTROL 长] {#long}

等同于 [!UICONTROL 长] 通过架构生成器UI创建的字段是 [`integer` 类型字段](#integer) 具有特定 `minimum` 和 `maximum` 值(`-9007199254740992` 和 `9007199254740992`（分别是）。

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

等同于 [!UICONTROL 短] 通过架构生成器UI创建的字段是 [`integer` 类型字段](#integer) 具有特定 `minimum` 和 `maximum` 值(`-32768` 和 `32768`（分别是）。

```json
"sampleField": {
  "title": "Sample Short Field",
  "description": "An example short field.",
  "type": "integer",
  "minimum": -32768,
  "maximum": 32768
}
```

## [!UICONTROL 字节] {#byte}

等同于 [!UICONTROL 字节] 通过架构生成器UI创建的字段是 [`integer` 类型字段](#integer) 具有特定 `minimum` 和 `maximum` 值(`-128` 和 `128`（分别是）。

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

[!UICONTROL 布尔型] 字段由表示 `type: boolean`.

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

您可以选择提供 `default` 在摄取期间未提供显式值时字段将使用的值。

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
>如果否 `default` 值且布尔字段设置为 `required`，则任何缺少此字段的接受值的记录将在摄取时验证失败。

## [!UICONTROL 日期] {#date}

[!UICONTROL 日期] 字段由表示 `type: string` 和 `format: date`. 您还可以选择提供数组 `examples` 当您需要为用户手动输入数据显示示例日期字符串时，可利用此方法。

```json
"sampleField": {
  "title": "Sample Date Field",
  "description": "An example date field with an example array item.",
  "type": "string",
  "format": "date",
  "examples": ["2004-10-23"]
}
```

## [!UICONTROL 日期时间] {#date-time}

[!UICONTROL 日期时间] 字段由表示 `type: string` 和 `format: date-time`. 您还可以选择提供数组 `examples` ，以便您能够为手动输入数据的用户显示示例日期时间字符串。

```json
"sampleField": {
  "title": "Sample Datetime Field",
  "description": "An example datetime field with an example array item.",
  "type": "string",
  "format": "date-time",
  "examples": ["2004-10-23T12:00:00-06:00"]
}
```

## [!UICONTROL 数组] {#array}

[!UICONTROL 数组] 字段由表示 `type: array` 和 `items` 对象，定义数组将接受的项目的架构。

您可以使用基元类型（如字符串数组）定义数组项：

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

您还可以通过引用 `$id` 数据类型的ID为 `$ref` 属性。 以下是一个数组 [!UICONTROL 付款项目] 对象：

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

[!UICONTROL 对象] 字段由表示 `type: object` 和 `properties` 为架构字段定义子属性的对象。

下定义的每个子字段 `properties` 可以使用任何原始进行定义 `type` 或通过引用现有数据类型 `$ref` 属性指向 `$id` 相关数据类型的：

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

您也可以通过引用数据类型来定义整个对象，前提是相关数据类型本身定义为 `type: object`：

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL 地图] {#map}

映射字段本质上是 [`object`-type字段](#object) 一组不受约束的键。 与对象一样，映射也具有 `type` 值 `object`，但其 `meta:xdmType` 明确设置为 `map`.

地图 **不得** 定义任意属性。 It **必须** 定义单个 `additionalProperties` 描述映射中包含的值类型的架构（每个映射只能包含一种数据类型）。 此 `type` 值必须为 `string` 或 `integer`.

例如，具有字符串类型值的映射字段将按如下方式定义：

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

有关创建自定义映射字段的更多详细信息，请参阅以下部分。

### 创建自定义映射类型 {#custom-maps}

为了在XDM中有效地支持“类似映射”的数据，可以使用 `meta:xdmType` 设置为 `map` 以明确说明对象应像键集不受约束那样进行管理。 摄取到映射字段中的数据必须使用字符串键，并且只能使用字符串或整数值（由决定） `additionalProperties.type`)。

XDM对此存储提示的使用施加以下限制：

* 映射类型必须为类型 `object`.
* 映射类型不能定义属性（换句话说，它们定义“空”对象）。
* 映射类型必须包括 `additionalProperties.type` 描述可以放置在映射中的值的字段，也可 `string` 或 `integer`.

确保仅在绝对必要时使用映射类型字段，因为它们存在以下性能缺陷：

* 响应时间 [Adobe Experience Platform查询服务](../../query-service/home.md) 一亿条记录从3秒降到10秒。
* 地图必须少于16个键，否则可能会进一步降级。

Platform用户界面在如何提取映射类型字段的键方面也存在限制。 虽然对象类型字段可以展开，但映射显示为单个字段。

## 后续步骤

本指南介绍了如何在API中定义不同的字段类型。 有关XDM字段类型格式化的更多信息，请参阅以下指南： [XDM字段类型约束](../schema/field-constraints.md).

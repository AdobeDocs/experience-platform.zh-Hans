---
title: 在架构注册表API中定义XDM字段
description: 了解如何在架构注册表API中创建自定义体验数据模型(XDM)资源时定义不同的字段。
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 6c6104a6aa0a80c886f4f02486a7645eb95da781
workflow-type: tm+mt
source-wordcount: '1197'
ht-degree: 0%

---

# 在架构注册表API中定义XDM字段

所有Experience Data Model (XDM)字段均使用适用于其字段类型的标准[JSON架构](https://json-schema.org/)约束进行定义，并对Adobe Experience Platform强制实施的字段名称使用其他约束。 架构注册表API允许您通过使用格式和可选约束来定义架构中的自定义字段。 XDM字段类型由字段级别属性`meta:xdmType`公开。

>[!NOTE]
>
>`meta:xdmType`是系统生成的值，因此使用API时不需要将此属性添加到字段的JSON中（除非在[创建自定义映射类型](#custom-maps)时）。 最佳实践是将JSON架构类型（如`string`和`integer`）与下表定义的相应最小/最大约束一起使用。

本指南概述了用于定义不同字段类型的相应格式，包括那些具有可选属性的字段类型。 有关可选属性和特定类型关键字的详细信息，请参阅[JSON架构文档](https://json-schema.org/understanding-json-schema/reference/type.html)。

若要开始，请查找所需的字段类型并使用提供的示例代码为[创建字段组](../api/field-groups.md#create)或[创建数据类型](../api/data-types.md#create)生成API请求。

## [!UICONTROL 字符串] {#string}

[!UICONTROL String]字段由`type: string`指示。

```json
"sampleField": {
  "title": "Sample String Field",
  "description": "An example string field.",
  "type": "string"
}
```

您可以选择通过以下附加属性来限制可为字符串输入的值的类型：

* `pattern`：约束所依据的正则表达式模式。
* `minLength`：字符串的最小长度。 默认情况下，字符串接收的最小值为`1`。
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

[!UICONTROL URI]字段由`type: string`指示，其中`format`属性设置为`uri`。 不接受其他属性。

```json
"sampleField": {
  "title": "Sample URI Field",
  "description": "An example URI field.",
  "type": "string",
  "format": "uri"
}
```

## [!UICONTROL 枚举] {#enum}

[!UICONTROL 枚举]字段必须使用`type: string`，枚举值本身在`enum`数组下提供：

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

您可以选择为`meta:enum`属性下的每个值提供面向客户的标签，每个标签都与`enum`下的对应值键控。

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
>`meta:enum`值&#x200B;**不**&#x200B;自行声明枚举或驱动任何数据验证。 在大多数情况下，在`meta:enum`下提供的字符串也在`enum`下提供，以确保数据受约束。 但是，在某些情况下，提供`meta:enum`时没有相应的`enum`数组。 有关详细信息，请参阅有关[定义建议值](../tutorials/suggested-values.md)的教程。

您可以选择提供`default`属性，以指示如果未提供值，字段将使用的默认`enum`值。

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
>如果未提供`default`值，并且枚举字段设置为`required`，则任何缺少此字段的接受值的记录将在摄取时验证失败。

## [!UICONTROL 数字] {#number}

数字字段由`type: number`指示，没有其他必需属性。

```json
"sampleField": {
  "title": "Sample Number Field",
  "description": "An example number field.",
  "type": "number"
}
```

>[!NOTE]
>
>`number`类型用于任何数字类型，可以是整数或浮点数，而[`integer`类型](#integer)专门用于整数数字。 有关每种类型的用例的更多信息，请参阅有关数字类型](https://json-schema.org/understanding-json-schema/reference/numeric.html)的[JSON架构文档。

## [!UICONTROL 整数] {#integer}

[!UICONTROL 整数]字段由`type: integer`指示，没有其他必填字段。

```json
"sampleField": {
  "title": "Sample Integer Field",
  "description": "An example integer field.",
  "type": "integer"
}
```

>[!NOTE]
>
>虽然`integer`类型专门引用整数值，但[`number`类型](#number)用于任何数值类型，可以是整数或浮点数。 有关每种类型的用例的更多信息，请参阅有关数字类型](https://json-schema.org/understanding-json-schema/reference/numeric.html)的[JSON架构文档。

您可以选择通过将`minimum`和`maximum`属性添加到定义来约束整数的范围。 架构生成器UI支持的几个其他数字类型只是具有特定`minimum`和`maximum`约束的`integer`类型，如[[!UICONTROL Long]](#long)、[[!UICONTROL Short]](#short)和[[!UICONTROL Byte]](#byte)。

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

通过架构生成器UI创建的[!UICONTROL Long]字段的等效项是[`integer`类型字段](#integer)，具有特定`minimum`和`maximum`值（分别为`-9007199254740992`和`9007199254740992`）。

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

通过架构生成器UI创建的[!UICONTROL Short]字段的等效项是[`integer`类型字段](#integer)，具有特定`minimum`和`maximum`值（分别为`-32768`和`32767`）。

```json
"sampleField": {
  "title": "Sample Short Field",
  "description": "An example short field.",
  "type": "integer",
  "minimum": -32768,
  "maximum": 32767
}
```

## [!UICONTROL 字节] {#byte}

通过架构生成器UI创建的[!UICONTROL 字节]字段的等效项是[`integer`类型字段](#integer)，具有特定`minimum`和`maximum`值（分别为`-128`和`127`）。

```json
"sampleField": {
  "title": "Sample Byte Field",
  "description": "An example byte field.",
  "type": "integer",
  "minimum": -128,
  "maximum": 127
}
```

## [!UICONTROL 布尔值] {#boolean}

[!UICONTROL Boolean]字段由`type: boolean`指示。

```json
"sampleField": {
  "title": "Sample Boolean Field",
  "description": "An example boolean field.",
  "type": "boolean"
}
```

您可以选择提供一个`default`值，如果没有在摄取期间提供显式值，则字段将使用该值。

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
>如果未提供`default`值，并且布尔字段设置为`required`，则任何缺少此字段的接受值的记录将在摄取时验证失败。

## [!UICONTROL 日期] {#date}

[!UICONTROL 日期]字段由`type: string`和`format: date`指示。 此外，您还可以选择提供一个`examples`数组，以便在需要为用户手动输入数据显示样本日期字符串时使用该数组。

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

[!UICONTROL 日期时间]字段由`type: string`和`format: date-time`指示。 您还可以选择提供一个`examples`数组，以便在要显示手动输入数据的用户的日期时间字符串示例的情况下使用。

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

[!UICONTROL Array]字段由`type: array`和`items`对象表示，该对象定义了该数组将接受的项的架构。

您可以使用原始类型（如字符串数组）定义数组项：

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

您还可以通过`$ref`属性引用数据类型的`$id`，根据现有数据类型定义数组项。 以下是[!UICONTROL 付款项]对象的数组：

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

[!UICONTROL 对象]字段由`type: object`和定义架构字段的子属性的`properties`对象表示。

在`properties`下定义的每个子字段可以使用任何基元`type`定义，也可以通过指向相关数据类型的`$id`的`$ref`属性引用现有数据类型来定义：

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

您也可以通过引用数据类型来定义整个对象，前提是相关数据类型本身定义为`type: object`：

```json
"sampleField": {
  "title": "Sample Object Field",
  "description": "An example object field using a data type reference.",
  "$ref": "https://ns.adobe.com/xdm/common/phoneinteraction"
}
```

## [!UICONTROL 地图] {#map}

映射字段本质上是具有无约束键集的[`object`类型字段](#object)。 与对象类似，映射的`type`值为`object`，但其`meta:xdmType`显式设置为`map`。

映射&#x200B;**不得**&#x200B;定义任何属性。 它&#x200B;**必须**&#x200B;定义单个`additionalProperties`架构以描述映射中包含的值类型（每个映射只能包含单个数据类型）。 `type`值必须为`string`或`integer`。

例如，带有字符串类型值的映射字段的定义如下所示：

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

为了在XDM中有效地支持“类似映射”的数据，可以使用设置为`map`的`meta:xdmType`对对象进行注释，以明确表示应像键集不受约束那样管理对象。 摄取到映射字段的数据必须使用字符串键，并且只能使用字符串或整数值（由`additionalProperties.type`决定）。

XDM对使用此存储提示设置了以下限制：

* 映射类型必须是`object`类型。
* 映射类型不能定义属性（换句话说，它们定义“空”对象）。
* 映射类型必须包含描述可以放置在映射中的值的`additionalProperties.type`字段，即`string`或`integer`。

确保仅在绝对必要时使用映射类型字段，因为它们存在以下性能缺陷：

* 来自[Adobe Experience Platform查询服务](../../query-service/home.md)的响应时间从3秒降至10秒，涉及1亿条记录。
* 地图必须少于16个键，否则可能会进一步降级。

Experience Platform用户界面在如何提取映射类型字段的键方面也存在限制。 虽然对象类型字段可以展开，但映射显示为一个字段。

## 后续步骤

本指南介绍了如何在API中定义不同的字段类型。 有关XDM字段类型的格式化的详细信息，请参阅[XDM字段类型约束](../schema/field-constraints.md)指南。

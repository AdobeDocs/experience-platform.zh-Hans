---
keywords: Experience Platform；主页；热门主题；模式;模式；字段组；字段组；字段组；字段组；数据类型；数据类型；数据类型；模式设计；数据类型；数据类型；数据类型；数据类型；模式类型；模式;模式设计；映射；
solution: Experience Platform
title: XDM字段类型约束
topic-legacy: overview
description: 对体验数据模型(XDM)中字段类型约束的参考，包括可以映射到的其他序列化格式以及如何在API中定义您自己的字段类型。
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
translation-type: tm+mt
source-git-commit: 3985ba8f46a62e8d9ea8b1f084198b245318a24f
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 1%

---

# XDM字段类型约束

在体验数据模型(XDM)模式中，字段的类型将限制字段可以包含的数据类型。 本文档概述了每个核心字段类型，包括它们可以映射到的其他序列化格式，以及如何在API中定义您自己的字段类型以实施不同的约束。

## 入门指南

在使用本指南之前，请阅读模式合成的[基础知识](./composition.md)，了解XDM模式、类和模式字段组的简介。

如果您计划在API中定义自己的字段类型，强烈建议您开始[模式注册表开发人员指南](../api/getting-started.md)，以了解如何创建字段组和数据类型以将您的自定义字段包含在中。 如果您使用Experience Platform UI创建模式，请参阅[定义UI](../ui/fields/overview.md)中的字段的指南，了解如何对自定义字段组和数据类型中定义的字段实现约束。

## 基本结构和示例

XDM构建在JSON模式之上，因此XDM字段在定义其类型时继承类似的语法。 了解JSON模式中不同字段类型的表示方式有助于指明每种类型的基本约束。

>[!NOTE]
>
>有关JSON模式和平台API中的其他基础技术的详细信息，请参阅[API基础指南](../../landing/api-fundamentals.md#json-schema)。

下表概述了每个XDM类型在JSON模式中的表示方式，以及与类型相符的示例值：

<table style="table-layout:auto">
  <thead>
    <tr>
      <th>XDM类型</th>
      <th>JSON模式</th>
      <th>示例</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>[!UICONTROL字符串]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type":"string"}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL多次]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type":"number"}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  “类型”："integer",
  “maximum”：9007199254740991,
  “minimum”：-9007199254740991
}</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL整数]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  “类型”："integer",
  “maximum”：2147483648,
  “minimum”：-2147483648
}</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL短]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  “类型”："integer",
  “maximum”：32768,
  “minimum”：-32768
}</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL字节]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  “类型”："integer",
  “maximum”：128,
  “minimum”：-128
}</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL日期]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  “类型”："string",
  “格式”："日期"
}</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  “类型”："string",
  “格式”："date-time"
}</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL布尔值]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type":"string"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**所有日期格式化字符串必须符合ISO 8601标准（[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)节）。*

## 将XDM类型映射到其他格式

以下各节介绍了每种XDM类型如何映射到其他常用序列化格式：

* [Parke、Spark SQL和Java](#parquet)
* [Scala、.NET和CosmosDB](#scala)
* [MongoDB、Aeropspike和Protobuf 2](#mongo)

>[!IMPORTANT]
>
>在下表中列出的标准XDM类型中，[!UICONTROL Map]类型也包括在内。 当数据表示为映射到某些值的键时，或者在静态模式中不能合理包括键并且必须被视为数据值时，映射在标准模式中使用。
>
>地图类型字段保留用于行业和供应商模式的使用，因此不能用于您定义的自定义资源。 映射类型包含在以下表格中仅旨在帮助您确定如果当前以下列任何格式存储现有数据，如何将其映射到XDM。

### Parce、Spark SQL和Java {#parquet}

| XDM类型 | 镶木 | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL String] | 类型：`BYTE_ARRAY`<br>注释：`UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Double] | 类型：`DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Long] | 类型：`INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Integer] | 类型：`INT32`<br>注释：`INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Short] | 类型：`INT32`<br>注释：`INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | 类型：`INT32`<br>注释：`INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Date] | 类型：`INT32`<br>注释：`DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | 类型：`INT64`<br>注释：`TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Boolean] | 类型：`BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Map] | `MAP`-annotated group<br><br>(`<key-type>` 必须 `STRING`) | `MapType`<br><br>(`keyType` 必须 `StringType`) | `java.util.Map` |

### Scala、.NET和CosmosDB {#scala}

| XDM类型 | 斯卡拉 | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL String] | `String` | `System.String` | `String` |
| [!UICONTROL Double] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Long] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Integer] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Short] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Date] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Boolean] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Map] | `Map` | (不适用) | `object` |

{style=&quot;table-layout:auto&quot;}

### MongoDB、Aeropspike和Protobuf 2 {#mongo}

| XDM类型 | MongoDB | 气塞 | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL String] | `string` | `String` | `string` |
| [!UICONTROL Double] | `double` | `Double` | `double` |
| [!UICONTROL Long] | `long` | `Integer` | `int64` |
| [!UICONTROL Integer] | `int` | `Integer` | `int32` |
| [!UICONTROL Short] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Date] | `date` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL Boolean] | `bool` | `Integer`<br>（0/1二进制） | `bool` |
| [!UICONTROL Map] | `object` | `map` | `map<key_type, value_type>` |

{style=&quot;table-layout:auto&quot;}

## 在API {#define-fields}中定义XDM字段类型

所有XDM字段均使用标准[JSON模式](https://json-schema.org/)约束定义，这些约束适用于其字段类型，并且对由[!DNL Experience Platform]强制实施的字段名称有附加约束。 模式注册表API允许您通过使用格式和可选约束定义其他字段类型。 XDM字段类型由字段级属性`meta:xdmType`公开。

>[!NOTE]
>
>`meta:xdmType` 是系统生成的值，因此在使用API时，您不必将此属性添加到字段的JSON中。最佳实践是将JSON模式类型（如`string`和`integer`）与下表中定义的适当最小/最大约束一起使用。

下表概述了定义不同字段类型（包括具有可选属性的字段类型）的适当格式。 有关可选属性和类型特定关键字的详细信息，请通过[JSON模式文档](https://json-schema.org/understanding-json-schema/reference/type.html)获取。

要开始，请找到所需的字段类型，并使用提供的示例代码构建API请求，以便[创建字段组](../api/field-groups.md#create)或[创建数据类型](../api/data-types.md#create)。

<table style="table-layout:auto">
  <tr>
    <th>XDM类型</th>
    <th>可选属性</th>
    <th>示例</th>
  </tr>
  <tr>
    <td>[!UICONTROL字符串]</td>
    <td>
      <ul>
        <li><code>pattern</code></li>
        <li><code>minLength</code></li>
        <li><code>maxLength</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
    “类型”："string",
    “模式”："^[A-Z]{2}$",
    "maxLength":2
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL URI]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  “类型”："string",
  “格式”："uri"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL枚举]</td>
    <td>
      <ul>
        <li><code>default</code></li>
        <li><code>meta:enum</code></li>
      </ul>
    </td>
    <td>约束枚举值在<code>enum</code>数组下提供，而每个值的面向客户的可选标签可以在<code>meta:enum</code>下提供：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  “类型”："string",
  "enum":[
      "value1",
      "value2",
      "value3"
  ],
  "meta:enum":{
      "value1":"值1",
      “value2”："值2",
      "value3":"值3"
  },
  “默认”："value1"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL编号]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  “类型”："number"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Long]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  “类型”："integer",
  “minimum”：-9007199254740992,
  “maximum”：9007199254740992
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL整数]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  “类型”："integer",
  “minimum”：-2147483648,
  “maximum”：2147483648
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL短]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  “类型”："integer",
  “minimum”：-32768,
  “maximum”：32768
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL字节]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  “类型”："integer",
  “minimum”：-128,
  “maximum”：128
  }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL布尔值]</td>
    <td>
      <ul>
        <li><code>default</code></li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  “类型”："boolean",
  “默认”：假
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL日期]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  “类型”："string",
  “格式”：“日期”，
  “examples”：["2004-10-23"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  “类型”："string",
  “格式”："date-time",
  “examples”：["2004-10-23T12:00:00-06:00"]
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL数组]</td>
    <td></td>
    <td>基本标量类型（例如字符串）的数组：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  “类型”："array",
  “项目”：{
    “类型”："字符串"
  }
}</pre>
      由另一个模式定义的对象数组：<br/>
      <pre class="JSON language-JSON hljs">
"sampleField":{
  “类型”："array",
  “项目”：{
    “$ref”："https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL对象]</td>
    <td></td>
    <td><code>properties</code>下定义的每个子字段的<code>type</code>属性可以使用任何标量类型进行定义：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  “类型”："object",
  “属性”：{
    "field1":{
      “类型”："字符串"
    },
    "field2":{
      “类型”："number"
    }
  }
}</pre>
      可通过引用数据类型的<code>$id</code>来定义对象类型字段：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  “类型”："object",
  “$ref”："https://ns.adobe.com/xdm/common/phoneinteraction"
}</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL映射]</td>
    <td></td>
    <td>映射<strong>不能</strong>定义任何属性。 它<strong>必须</strong>定义单个<code>additionalProperties</code>模式来描述映射中包含的值类型（每个映射只能包含单个数据类型）。 值可以是任何有效的XDM <code>type</code>属性，也可以是使用<code>$ref</code>属性对其他模式的引用。<br/><br/>具有字符串类型值的映射字段：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  “类型”："object",
  "additionalProperties":{
    “类型”："字符串"
  }
}</pre>
    具有以下值字符串数组的映射字段：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  “类型”："object",
  "additionalProperties":{
    “类型”："array",
    “项目”：{
      “类型”："字符串"
    }
  }
}</pre>
    引用其他数据类型的映射字段：
      <pre class="JSON language-JSON hljs">
"sampleField":{
  “类型”："object",
  "additionalProperties":{
    “$ref”："https://ns.adobe.com/xdm/data/paymentitem"
  }
}</pre>
    </td>
  </tr>
</table>

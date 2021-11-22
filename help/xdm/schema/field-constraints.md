---
keywords: Experience Platform；主页；热门主题；架构；架构；字段组；字段组；字段组；数据类型；数据类型；数据类型；数据类型；架构设计；数据类型；数据类型；数据类型；数据类型；架构；架构；架构；架构设计；映射；
solution: Experience Platform
title: XDM字段类型约束
topic-legacy: overview
description: 体验数据模型(XDM)中字段类型约束的引用，包括可映射到的其他序列化格式以及如何在API中定义您自己的字段类型。
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 684237122e7384f6c611e1c602c30af2518aba58
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 3%

---

# XDM字段类型约束

在体验数据模型(XDM)架构中，字段的类型将限制字段可以包含的数据类型。 本文档概述了每个核心字段类型，包括可映射到的其他序列化格式，以及如何在API中定义您自己的字段类型以强制实施不同的限制。

## 快速入门

在使用本指南之前，请查看 [架构组合基础知识](./composition.md) 有关XDM模式、类和模式字段组的介绍。

如果您计划在API中定义自己的字段类型，强烈建议您先从 [架构注册开发人员指南](../api/getting-started.md) 了解如何创建字段组和数据类型，以在中包含您的自定义字段。 如果您使用Experience PlatformUI创建架构，请参阅 [在UI中定义字段](../ui/fields/overview.md) 了解如何对自定义字段组和数据类型中定义的字段实施约束。

## 基本结构和示例

XDM是基于JSON架构构建的，因此，XDM字段在定义其类型时会继承类似的语法。 了解不同字段类型在JSON模式中的表示方式有助于指示每种类型的基本约束。

>[!NOTE]
>
>请参阅 [API基础知识指南](../../landing/api-fundamentals.md#json-schema) 有关Platform API中JSON模式和其他基础技术的更多信息。

下表概述了每个XDM类型在JSON模式中的表示方式，以及符合该类型的示例值：

<table style="table-layout:auto">
  <thead>
    <tr>
      <th>XDM类型</th>
      <th>JSON架构</th>
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
      <td>[!UICONTROL Double]</td>
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
{ "type":"integer", "maximum":9007199254740991，“最小”：-9007199254740991 }</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL整数]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type":"integer", "maximum":2147483648，“最小”：-2147483648 }</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type":"integer", "maximum":32768，“最小”：-32768 }</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type":"integer", "maximum":128，“最低”：-128 }</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL日期]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type":"string", "format":"date" }</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type":"string", "format":"date-time" }</pre>
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

**所有日期格式的字符串必须符合ISO 8601标准([RFC 3339，第5.6节](https://tools.ietf.org/html/rfc3339#section-5.6))。*

## 将XDM类型映射到其他格式

以下各节介绍了每种XDM类型如何映射到其他常见的序列化格式：

* [Parquet、Spark SQL和Java](#parquet)
* [Scala、.NET和CosmosDB](#scala)
* [MongoDB、塞式和Protobuf 2](#mongo)

>[!IMPORTANT]
>
>在下表中列出的标准XDM类型中， [!UICONTROL 地图] 类型。 当数据表示为映射到某些值的键时，或者当静态架构中不能合理地包含键并且必须将其视为数据值时，标准架构中会使用映射。
>
>映射类型字段为行业和供应商架构使用而保留，因此不能在您定义的自定义资源中使用。 下表中包含的映射类型仅旨在帮助您确定如果现有数据当前以下面列出的任何格式存储，则如何将现有数据映射到XDM。

### Parquet、Spark SQL和Java {#parquet}

| XDM类型 | 镶木 | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL 字符串] | 类型： `BYTE_ARRAY`<br>注释： `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL 双精度] | 类型：`DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL 长] | 类型：`INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL 整数] | 类型： `INT32`<br>注释： `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL 短] | 类型： `INT32`<br>注释： `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL 字节] | 类型： `INT32`<br>注释： `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL 日期] | 类型： `INT32`<br>注释： `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | 类型： `INT64`<br>注释： `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL 布尔型] | 类型：`BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL 地图] | `MAP` — 注释组<br><br>(`<key-type>` 必须 `STRING`) | `MapType`<br><br>(`keyType` 必须 `StringType`) | `java.util.Map` |

{style=&quot;table-layout:auto&quot;}

### Scala、.NET和CosmosDB {#scala}

| XDM类型 | 斯卡拉 | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL 字符串] | `String` | `System.String` | `String` |
| [!UICONTROL 双精度] | `Double` | `System.Double` | `Number` |
| [!UICONTROL 长] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL 整数] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL 短] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL 字节] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL 日期] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL 布尔型] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL 地图] | `Map` | (不适用) | `object` |

{style=&quot;table-layout:auto&quot;}

### MongoDB、塞式和Protobuf 2 {#mongo}

| XDM类型 | MongoDB | 气塞 | 原虫2 |
| --- | --- | --- | --- |
| [!UICONTROL 字符串] | `string` | `String` | `string` |
| [!UICONTROL 双精度] | `double` | `Double` | `double` |
| [!UICONTROL 长] | `long` | `Integer` | `int64` |
| [!UICONTROL 整数] | `int` | `Integer` | `int32` |
| [!UICONTROL 短] | `int` | `Integer` | `int32` |
| [!UICONTROL 字节] | `int` | `Integer` | `int32` |
| [!UICONTROL 日期] | `date` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL 布尔型] | `bool` | `Integer`<br>（0/1二进制） | `bool` |
| [!UICONTROL 地图] | `object` | `map` | `map<key_type, value_type>` |

{style=&quot;table-layout:auto&quot;}

## 在API中定义XDM字段类型 {#define-fields}

所有XDM字段均使用标准 [JSON架构](https://json-schema.org/) 应用于其字段类型的约束，对字段名称的附加约束由 [!DNL Experience Platform]. 架构注册表API允许您通过使用格式和可选约束定义其他字段类型。 XDM字段类型由字段级别属性公开， `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` 是系统生成的值，因此在使用API时，您无需将此属性添加到字段的JSON中。 最佳实践是使用JSON架构类型(例如 `string` 和 `integer`)，并且具有下表中定义的相应最小/最大约束。

下表概述了用于定义不同字段类型（包括具有可选属性的字段类型）的相应格式。 有关可选属性和特定类型关键词的更多信息，请通过 [JSON模式文档](https://json-schema.org/understanding-json-schema/reference/type.html).

要开始，请找到所需的字段类型，然后使用提供的示例代码来构建 [创建字段组](../api/field-groups.md#create) 或 [创建数据类型](../api/data-types.md#create).

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
"sampleField":{ "type":"string", "pattern":"^[A-Z]{2}$", "maxLength":2 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL URI]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"string", "format":"uri" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Enum]</td>
    <td>
      <ul>
        <li><code>default</code></li>
        <li><code>meta:enum</code></li>
      </ul>
    </td>
    <td>约束枚举值在 <code>enum</code> 数组中，而每个值的可选面向客户的标签可以在 <code>meta:enum</code>:
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"string", "enum":[ "value1"、"value2"、"value3" ]、"meta:enum":{ "value1":"Value 1"、"value2":"Value 2"、"value3":"Value 3" }, "default":"value1" }</pre>
    <br>请注意， <code>meta:enum</code> 值 <strong>not</strong> 声明枚举或自行驱动任何数据验证。 在大多数情况下， <code>meta:enum</code> 此外， <code>enum</code> 以确保数据受到约束。 但是，在某些用例中， <code>meta:enum</code> 没有相应的 <code>enum</code> 数组。 请参阅 <a href="../tutorials/extend-soft-enum.md">扩展软边</a> 以了解更多信息。
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Number]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"number" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Long]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"integer", "minimum":-9007199254740992, "maximum":9007199254740992 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL整数]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"integer", "minimum":-2147483648, "maximum":2147483648 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Short]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"integer", "minimum":-32768, "maximum":32768 }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Byte]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"integer", "minimum":-128，“最大值”：128 }</pre>
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
"sampleField":{ "type":"boolean", "default":false }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL日期]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"string", "format":"date"、"examples":["2004-10-23"] }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL DateTime]</td>
    <td></td>
    <td>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"string", "format":"date-time"、"examples":["2004-10-23T12:00:00-06:00"] }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL Array]</td>
    <td></td>
    <td>基本标量类型（例如字符串）的数组：
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"array", "items":{ "type":"string" } }</pre>
      由其他模式定义的对象数组：<br/>
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"array", "items":{“$ref”："https://ns.adobe.com/xdm/data/paymentitem } }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL对象]</td>
    <td></td>
    <td>的 <code>type</code> 下定义的每个子字段的属性 <code>properties</code> 可以使用任何标量类型定义：
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"object"、"properties":{ "field1":{ "type":"string" }, "field2":{ "type":"number" } } }</pre>
      可通过引用 <code>$id</code> 数据类型：
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"object", "$ref":"https://ns.adobe.com/xdm/common/phoneinteraction" }</pre>
    </td>
  </tr>
  <tr>
    <td>[!UICONTROL映射]</td>
    <td></td>
    <td>地图 <strong>必须</strong> 定义任何属性。 它 <strong>必须</strong> 定义单个 <code>additionalProperties</code> 用于描述映射中包含的值类型的架构（每个映射只能包含单个数据类型）。 值可以是任何有效的XDM <code>type</code> 属性，或使用 <code>$ref</code> 属性。<br/><br/>具有字符串类型值的映射字段：
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"object", "additionalProperties":{ "type":"string" } }</pre>
    包含值字符串数组的映射字段：
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"object", "additionalProperties":{ "type":"array", "items":{ "type":"string" } } }</pre>
    引用其他数据类型的映射字段：
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"object", "additionalProperties":{ "$ref":"https://ns.adobe.com/xdm/data/paymentitem } }</pre>
    </td>
  </tr>
</table>

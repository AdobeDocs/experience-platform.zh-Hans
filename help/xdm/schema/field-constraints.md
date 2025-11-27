---
keywords: Experience Platform；主页；热门主题；架构；架构；字段组；字段组；字段组；数据类型；数据类型；数据类型；架构设计；数据类型；数据类型；数据类型；架构；架构；架构设计；映射；映射；
solution: Experience Platform
title: XDM字段类型约束
description: 参考体验数据模型(XDM)中的字段类型约束，包括它们可以映射到的其他序列化格式以及如何在API中定义您自己的字段类型。
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 8ddedb5ff8c12b05cdf39fa8dc2b59258389e522
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 1%

---

# XDM字段类型约束

在Experience Data Model (XDM)架构中，字段的类型会限制字段可以包含的数据类型。 本文档概述了每种核心字段类型，包括它们可以映射到的其他序列化格式，以及如何在API中定义自己的字段类型以强制实施不同的限制。

## 快速入门

在使用本指南之前，请查看架构组合的[基础知识](./composition.md)，以了解XDM架构、类和架构字段组的简介。

如果您计划在API中定义自己的字段类型，强烈建议您从[架构注册表开发人员指南](../api/getting-started.md)开始，了解如何创建字段组和数据类型以包含您的自定义字段。 如果您使用Experience Platform UI创建架构，请参阅[在UI中定义字段指南](../ui/fields/overview.md)，以了解如何对您在自定义字段组和数据类型中定义的字段实施约束。

## 基本结构和示例 {#basic-types}

XDM基于JSON架构构建，因此XDM字段在定义其类型时继承类似的语法。 了解不同字段类型在JSON架构中的表示方式有助于指示每种类型的基本约束。 自定义字段名称不区分大小写，并且在架构中的同一级别必须具有不同的名称。

>[!NOTE]
>
>有关Experience Platform API中JSON架构和其他基础技术的更多信息，请参阅[API基础指南](../../landing/api-fundamentals.md#json-schema)。

下表概述了每个XDM类型在JSON架构中的表示方式，以及符合该类型的示例值：

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
      <td>[!UICONTROL String]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type"： "string"}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Number]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type"： "number"}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type"： "integer"，
  "maximum"：9007199254740991，
  "minimum"： -9007199254740991
}</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Integer]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type"： "integer"，
  "maximum"：2147483648，
  "minimum"： -2147483648
}</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type"： "integer"，
  "maximum"：32767，
  "minimum"： -32768
}</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Byte]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type"： "integer"，
  “最大值”：128，
  “最小值”：-128
}</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Date]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type"： "string"，
  "format"： "date"
}</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL DateTime]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{
  "type"： "string"，
  "format"： "date-time"
}</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[!UICONTROL Boolean]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type"： "boolean"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**所有日期格式字符串必须符合ISO 8601标准（[RFC 3339，第5.6](https://tools.ietf.org/html/rfc3339#section-5.6)节）。*

## 将XDM类型映射到其他格式

以下各节将介绍每个XDM类型如何映射到其他常见的序列化格式：

* [Parquet、Spark SQL和Java](#parquet)
* [Scala、.NET和CosmosDB](#scala)
* [MongoDB、Arospike和Protobuf 2](#mongo)

>[!NOTE]
>
>在下表列出的标准XDM类型中，[!UICONTROL Map]类型也包括在内。 当数据表示为映射到特定值的键时，或者在静态架构中无法合理地包含键且必须视为数据值时，在标准架构中使用映射。
>
>许多标准XDM组件使用映射类型，如果需要，您还可以[定义自定义映射字段](../tutorials/custom-fields-api.md#custom-maps)。 下表包含映射类型，其目的是为了帮助您确定如何将现有数据映射到XDM（如果当前以下面列出的任何格式存储）。

### Parquet、Spark SQL和Java {#parquet}

| XDM类型 | Parquet | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL String] | 类型： `BYTE_ARRAY`<br>批注： `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL Number] | 类型：`DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL Long] | 类型：`INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL Integer] | 类型： `INT32`<br>批注： `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL Short] | 类型： `INT32`<br>批注： `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL Byte] | 类型： `INT32`<br>批注： `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL Date] | 类型： `INT32`<br>批注： `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL DateTime] | 类型： `INT64`<br>批注： `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL Boolean] | 类型：`BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL Map] | `MAP` — 注释的组<br><br>（`<key-type>`必须为`STRING`） | `MapType`<br><br>（`keyType`必须为`StringType`） | `java.util.Map` |

{style="table-layout:auto"}

### Scala、.NET和CosmosDB {#scala}

| XDM类型 | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL String] | `String` | `System.String` | `String` |
| [!UICONTROL Number] | `Double` | `System.Double` | `Number` |
| [!UICONTROL Long] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL Integer] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL Short] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL Byte] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL Date] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL DateTime] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL Boolean] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL Map] | `Map` | （不适用） | `object` |

{style="table-layout:auto"}

### MongoDB、Arospike和Protobuf 2 {#mongo}

| XDM类型 | MongoDB | 塞式火箭 | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL String] | `string` | `String` | `string` |
| [!UICONTROL Number] | `double` | `Double` | `double` |
| [!UICONTROL Long] | `long` | `Integer` | `int64` |
| [!UICONTROL Integer] | `int` | `Integer` | `int32` |
| [!UICONTROL Short] | `int` | `Integer` | `int32` |
| [!UICONTROL Byte] | `int` | `Integer` | `int32` |
| [!UICONTROL Date] | `date` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL DateTime] | `timestamp` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL Boolean] | `bool` | `Integer`<br>（0/1二进制文件） | `bool` |
| [!UICONTROL Map] | `object` | `map` | `map<key_type, value_type>` |

{style="table-layout:auto"}

## 在API中定义XDM字段类型 {#define-fields}

架构注册表API允许您通过使用格式和可选约束来定义自定义字段。 有关详细信息，请参阅[在架构注册表API](../tutorials/custom-fields-api.md)中定义自定义字段指南。

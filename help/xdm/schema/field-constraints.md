---
keywords: Experience Platform；主页；热门主题；架构；架构；字段组；字段组；字段组；数据类型；数据类型；数据类型；架构设计；数据类型；数据类型；数据类型；数据类型；架构；架构；架构设计；映射；映射；
solution: Experience Platform
title: XDM字段类型约束
description: 参考体验数据模型(XDM)中的字段类型约束，包括它们可以映射到的其他序列化格式以及如何在API中定义自己的字段类型。
exl-id: 63839a28-6d26-46f1-8bbf-b524e82ac4df
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 4%

---

# XDM字段类型约束

在Experience Data Model (XDM)架构中，字段的类型会限制字段可以包含的数据类型。 本文档概述了每个核心字段类型，包括它们可以映射到的其他序列化格式，以及如何在API中定义自己的字段类型以强制执行不同的限制。

## 快速入门

在使用本指南之前，请查阅 [模式组合基础](./composition.md) 有关XDM架构、类和架构字段组的介绍。

如果您计划在API中定义自己的字段类型，强烈建议您从 [Schema Registry开发人员指南](../api/getting-started.md) 了解如何创建字段组和数据类型以在中包含自定义字段。 如果您使用Experience PlatformUI创建架构，请参阅以下指南中的 [在UI中定义字段](../ui/fields/overview.md) 了解如何对您在自定义字段组和数据类型中定义的字段实施约束。

## 基本结构和示例 {#basic-types}

XDM基于JSON架构构建，因此XDM字段在定义其类型时继承类似的语法。 了解不同字段类型在JSON架构中的表示方式有助于指示每种类型的基本约束。

>[!NOTE]
>
>请参阅 [API基础知识指南](../../landing/api-fundamentals.md#json-schema) 有关JSON架构和平台API中其他底层技术的更多信息。

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
      <td>[！UICONTROL字符串]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type"： "string"}</pre>
      </td>
      <td><code>"Platinum"</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL双精度]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type"： "number"}</pre>
      </td>
      <td><code>12925.49</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL Long]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type"： "integer"， "maximum"： 9007199254740991， "minimum"： -9007199254740991 }</pre>
      </td>
      <td><code>1478108935</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL整数]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type"： "integer"， "maximum"： 2147483648， "minimum"： -2147483648 }</pre>
      </td>
      <td><code>24906290</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL Short]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type"： "integer"， "maximum"： 32768， "minimum"： -32768 }</pre>
      </td>
      <td><code>15781</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL字节]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type"： "integer"， "maximum"： 128， "minimum"： -128 }</pre>
      </td>
      <td><code>90</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL日期]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type"： "string"， "format"： "date" }</pre>
      </td>
      <td><code>"2019-05-15"</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL日期时间]*</td>
      <td>
        <pre class="JSON language-JSON hljs">
{ "type"： "string"， "format"： "date-time" }</pre>
      </td>
      <td><code>"2019-05-15T20:20:39+00:00"</code></td>
    </tr>
    <tr>
      <td>[！UICONTROL Boolean]</td>
      <td>
        <pre class="JSON language-JSON hljs">
{"type"： "string"}</pre>
      </td>
      <td><code>true</code></td>
    </tr>
  </tbody>
</table>

**所有日期格式字符串必须符合ISO 8601标准([RFC 3339,5.6节](https://tools.ietf.org/html/rfc3339#section-5.6))。*

## 将XDM类型映射到其他格式

以下各节将介绍每个XDM类型如何映射到其他常见的序列化格式：

* [Parquet、Spark SQL和Java](#parquet)
* [Scala、.NET和CosmosDB](#scala)
* [MongoDB、Arespoke和Protobuf 2](#mongo)

>[!NOTE]
>
>在下表中列出的标准XDM类型中， [!UICONTROL 映射] 类型也包括在内。 当数据表示为映射到某些值的键，或者键无法合理地包含在静态架构中并且必须被视为数据值时，在标准架构中使用映射。
>
>许多标准XDM组件使用映射类型，您还可以 [定义自定义映射字段](../tutorials/custom-fields-api.md#custom-maps) 如果需要。 下表中包含的映射类型旨在帮助您确定如何将现有数据映射到XDM（如果它当前以下面列出的任何格式存储）。

### Parquet、Spark SQL和Java {#parquet}

| XDM类型 | Parquet | Spark SQL | Java |
| --- | --- | --- | --- |
| [!UICONTROL 字符串] | 类型： `BYTE_ARRAY`<br>注释： `UTF8` | `StringType` | `java.lang.String` |
| [!UICONTROL 双精度] | 类型：`DOUBLE` | `LongType` | `java.lang.Double` |
| [!UICONTROL 长] | 类型：`INT64` | `LongType` | `java.lang.Long` |
| [!UICONTROL 整数] | 类型： `INT32`<br>注释： `INT_32` | `IntegerType` | `java.lang.Integer` |
| [!UICONTROL 短] | 类型： `INT32`<br>注释： `INT_16` | `ShortType` | `java.lang.Short` |
| [!UICONTROL 字节] | 类型： `INT32`<br>注释： `INT_8` | `ByteType` | `java.lang.Short` |
| [!UICONTROL 日期] | 类型： `INT32`<br>注释： `DATE` | `DateType` | `java.util.Date` |
| [!UICONTROL 日期时间] | 类型： `INT64`<br>注释： `TIMESTAMP_MILLIS` | `TimestampType` | `java.util.Date` |
| [!UICONTROL 布尔型] | 类型：`BOOLEAN` | `BooleanType` | `java.lang.Boolean` |
| [!UICONTROL 地图] | `MAP` — 注释组<br><br>(`<key-type>` 必须是 `STRING`) | `MapType`<br><br>(`keyType` 必须是 `StringType`) | `java.util.Map` |

{style="table-layout:auto"}

### Scala、.NET和CosmosDB {#scala}

| XDM类型 | Scala | .NET | CosmosDB |
| --- | --- | --- | --- |
| [!UICONTROL 字符串] | `String` | `System.String` | `String` |
| [!UICONTROL 双精度] | `Double` | `System.Double` | `Number` |
| [!UICONTROL 长] | `Long` | `System.Int64` | `Number` |
| [!UICONTROL 整数] | `Int` | `System.Int32` | `Number` |
| [!UICONTROL 短] | `Short` | `System.Int16` | `Number` |
| [!UICONTROL 字节] | `Byte` | `System.SByte` | `Number` |
| [!UICONTROL 日期] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL 日期时间] | `java.util.Date` | `System.DateTime` | `String` |
| [!UICONTROL 布尔型] | `Boolean` | `System.Boolean` | `Boolean` |
| [!UICONTROL 地图] | `Map` | (不适用) | `object` |

{style="table-layout:auto"}

### MongoDB、Arespoke和Protobuf 2 {#mongo}

| XDM类型 | MongoDB | 塞式火箭 | Protobuf 2 |
| --- | --- | --- | --- |
| [!UICONTROL 字符串] | `string` | `String` | `string` |
| [!UICONTROL 双精度] | `double` | `Double` | `double` |
| [!UICONTROL 长] | `long` | `Integer` | `int64` |
| [!UICONTROL 整数] | `int` | `Integer` | `int32` |
| [!UICONTROL 短] | `int` | `Integer` | `int32` |
| [!UICONTROL 字节] | `int` | `Integer` | `int32` |
| [!UICONTROL 日期] | `date` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL 日期时间] | `timestamp` | `Integer`<br>（Unix毫秒） | `int64`<br>（Unix毫秒） |
| [!UICONTROL 布尔型] | `bool` | `Integer`<br>（0/1二进制） | `bool` |
| [!UICONTROL 地图] | `object` | `map` | `map<key_type, value_type>` |

{style="table-layout:auto"}

## 在API中定义XDM字段类型 {#define-fields}

架构注册表API允许您通过使用格式和可选约束来定义自定义字段。 请参阅指南，网址为 [定义架构注册表API中的自定义字段](../tutorials/custom-fields-api.md) 了解更多信息。

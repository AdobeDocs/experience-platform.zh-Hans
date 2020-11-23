---
keywords: Experience Platform;home;popular topics;schema;Schema;mixin;Mixin;Mixins;mixins;data type;data types;Data types;Data type;schema design;datatype;Datatype;data type;Data type;schemas;Schemas;Schema design;map;Map;
solution: Experience Platform
title: XDM字段类型约束
topic: overview
description: 对XDM字段类型约束的引用，包括可以映射到的其他序列化格式以及如何在API中定义您自己的字段类型。
translation-type: tm+mt
source-git-commit: e92294b9dcea37ae2a4a398c9d3397dcf5aa9b9e
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 6%

---


# XDM字段类型约束

您为模式选择的XDM字段类型会限制这些字段可以包含的数据类型。 此文档概述了每个核心字段类型，包括可映射到的其他序列化格式，以及如何在API中定义您自己的字段类型以实施不同的约束。

## 入门指南

在使用本指南之前，请查阅 [模式合成的基础](./composition.md) ，了解XDM模式、类和混合的简介。

如果您计划定义自己的字段类型，强烈建议您开始《 [模式注册表开发人员指南](../api/getting-started.md) 》，了解如何创建混音和数据类型以将自定义字段包含在中。

## 将XDM类型映射到其他格式

下表描述了每种XDM类型()和其`meta:xdmType`他序列化格式之间的映射。

| XDM类型<br>(meta:xdmType) | JSON<br>(JSON模式) | Parke<br>（类型／注释） | [!DNL Spark] SQL | Java | 斯卡拉 | .NET | CosmosDB | MongoDB | 塞式飞行器 | Protobuf 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| 字符串 | 类型：字符串 | BYTE_ARRAY/UTF8 | 字符串类型 | java.lang.String | 字符串 | System.String | 字符串 | 字符串 | 字符串 | 字符串 |
| 数字 | 类型：数字 | 多次 | DoubleType | java.lang.Double | 双精度 | System.Double | 数值 | 多次 | 双精度 | 多次 |
| 长 | type:<br>integermaximum:2^53+1<br>minimum:-2^53+1 | INT64 | LongType | java.lang.Long | 长 | System.Int64 | 数值 | 长 | 整数 | int64 |
| int | type:<br>integermaximum:2^31<br>minimum:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | 数值 | int | 整数 | int32 |
| 短 | type:<br>integermaximum:2^15<br>minimum:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | 短 | System.Int16 | 数值 | int | 整数 | int32 |
| 字节 | type:<br>integermaximum:2^7<br>minimum:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | 字节 | System.SByte | 数值 | int | 整数 | int32 |
| 布尔 | 类型：布尔值 | 布尔值 | BooleanType | java.lang.Boolean | 布尔值 | System.Boolean | 布尔值 | bool | 整数 | 整数 | bool |
| 日期 | type:<br>stringformat:date<br>（RFC 3339，第5.6节） | INT32/日 | 日期类型 | java.util.Date | java.util.Date | System.DateTime | 字符串 | 日期 | 整数<br>(unix millis) | int64<br>(unix millis) |
| date-time | type:<br>stringformat:date-time<br>（RFC 3339，第5.6节） | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | 字符串 | timestamp | 整数<br>(unix millis) | int64<br>(unix millis) |
| 地图 | 对象 | MAP注释组<br><br>&lt;<span>key_type</span>>必须是映射值的STRING<br><br><span>&lt;</span>value_type>类型 | MapType<br><br>&quot;keyType&quot; MUST be StringType<br><br>&quot;valueType&quot;是映射值的类型。 | java.util.Map | 地图 | --- | 对象 | 对象 | 地图 | map&lt;<span>key_type, value_type</span>> |

## 在API中定义XDM字段类型 {#define-fields}

XDM模式是使用JSON [模式标准和基](https://json-schema.org/) 本字段类型定义 [!DNL Experience Platform]，并对字段名称进行附加约束，这些约束由强制实施。 模式 [注册表API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) 允许您通过使用格式和可选约束定义其他字段类型。 XDM字段类型由字段级属性公开 `meta:xdmType`。

>[!NOTE]
>
>`meta:xdmType` 是系统生成的值，因此您无需将此属性添加到字段的JSON中。 最佳实践是将JSON模式类型（如字符串和整数）与下表中定义的适当最小／最大约束一起使用。

下表概述了使用可选属性定义标量字段类型和更多特定字段类型的适当格式。 有关可选属性和类型特定关键字的更多信息，请通过JSON [模式文档获取](https://json-schema.org/understanding-json-schema/reference/type.html)。

首先，找到所需的字段类型，然后使用提供的示例代码构建API请求， [以创建混合](../api/mixins.md#create)[或创建数据类型](../api/data-types.md#create)。

<table>
  <tr>
    <th>所需类型<br/>(meta:xdmType)</th>
    <th>JSON<br/>(JSON模式)</th>
    <th>代码示例</th>
  </tr>
  <tr>
    <td>字符串</td>
    <td>类型：字<br/><br/><strong>符串可选属性：</strong><br/>
      <ul>
        <li>图案</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"string", "pattern":"^[A-Z]{2}$", "maxLength":2 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>类型：<br/>字符串格式：uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"string", "format":"uri" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>枚举<br/>(xdmType:字符串)</td>
    <td>类型：<br/><br/><strong>string可选属性：</strong><br/>
      <ul>
        <li>默认</li>
      </ul>
    </td>
    <td>使用“meta:enum”指定面向客户的选项标签：
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"string", "enum":[ "value1"、"value2"、"value3" ]、"meta:enum":{ "value1":“值1”、“值2”:“值2”、“值3”:"Value 3" }, "default":"value1" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>数字</td>
    <td>类型：最<br/>小数量：最大为±2.23×10^308<br/>:±1.80×10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"number" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>长</td>
    <td>类型：最<br/>大积分：2^53+1<br>最小积分：-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"integer", "minimum":-9007199254740992, "maximum":9007199254740992 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>类型：最<br/>大积分：2<br>^31最小积分：-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"integer", "minimum":-2147483648, "maximum":2147483648 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>短</td>
    <td>类型：最<br/>大积分：2<br>^15最小积分：-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"integer", "minimum":-32768, "maximum":32768 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>字节</td>
    <td>类型：最<br/>大积分：2^<br>7最小积分：-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"integer", "minimum":-128, "maximum":128 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>布尔</td>
    <td><br/>类型：boolean<br/>{true, false}可<br/><br/><strong>选属性：</strong><br/>
      <ul>
        <li>默认</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"boolean", "default":false }
      </pre>
    </td>
  </tr>
  <tr>
    <td>日期</td>
    <td>类型：<br/>字符串格式：日期</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"string", "format":“date”、“examples”:["2004-10-23"] }
      </pre>
      RFC 3339第5. <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">6节定义的日期</a>，其中“full-date” = date-fullyear "-" date-month "-" date-mday(YYYY-MM-DD)
    </td>
  </tr>
  <tr>
    <td>date-time</td>
    <td>类型：<br/>字符串格式：date-time</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"string", "format":“date-time”、“examples”:["2004-10-23T12:00:00-06:00"] }
      </pre>
      Date-Time，由 <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339第5.6节定义</a>，其中“date-time”=完整日期“T”全时：<br/>(YYYY-MM-DD'T'HH:MM:SS.SSSX)
    </td>
  </tr>
  <tr>
    <td>阵列</td>
    <td>类型：阵列</td>
    <td>items.type可使用任何标量类型定义：
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"array", "items":{ "type":"string" } }
      </pre>
      由另一个模式定义的对象数组：<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"array", "items":{ "$ref":"id" } }
      </pre>
      其中“id”是引用模式的{id}。
    </td>
  </tr>
  <tr>
    <td>对象</td>
    <td>类型：对象</td>
    <td>属性。{field}.type可以使用任何标量类型定义：
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"object", "properties":{ "field1":{ "type":"string" }, "field2":{ "type":"number" } } } }
      </pre>
      引用模式定义的“object”类型字段：
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":“对象”、“$ref”:"id" }
      </pre>
      其中“id”是引用模式的{id}。
    </td>
  </tr>
  <tr>
    <td>地图</td>
    <td>类型：对<br/><br/><strong>象注</strong><br/>意：“map”数据类型的使用是为行业和供应商模式的使用而保留的，不可用于租户定义的字段。 当数据表示为映射到某个值的键时，或者在静态模式中无法合理包含键并且必须作为数据值时，它将在标准模式中使用。</td>
    <td>“map”不能定义任何属性。 它必须定义单个“[!UICONTROL additionalProperties]”模式来描述“map”中包含的值类型。 XDM中的“map”只能包含单个数据类型。 值可以是任何有效的XDM模式定义，包括数组或对象，或作为对其他模式的引用（通过$ref）。<br/><br/>具有“string”类型值的映射字段：
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"object", "additionalProperties":{ "type":"string" } }
      </pre>
    值为字符串数组的映射字段：
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"object", "additionalProperties":{ "type":"array", "items":{ "type":"string" } } } }
      </pre>
    引用其他模式的映射字段：
      <pre class="JSON language-JSON hljs">
        "sampleField":{ "type":"object", "additionalProperties":{ "$ref":"id" } }
      </pre>
      其中“id”是引用模式的{id}。
    </td>
  </tr>
</table>

---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 模式注册开发人员附录
topic: developer guide
translation-type: tm+mt
source-git-commit: f7c87cc86bfc5017ec5c712d05e39be5c14a7147

---


# 附录

本文档提供与使用模式注册表API相关的补充信息。

## 兼容性模式

Experience Data Model(XDM)是一个公开记录的规范，由Adobe推动，旨在提高数字体验的互操作性、表现力和强大功能。 Adobe在GitHub上的开放源项目中维护 [源代码和正式XDM定义](https://github.com/adobe/xdm/)。 这些定义以XDM标准记号编写，使用JSON-LD（链接数据的JavaScript对象记号）和JSON模式作为定义XDM模式的语法。

在公共存储库中查看正式的XDM定义时，您会发现标准XDM与Adobe Experience Platform中看到的不同。 您在Experience Platform中看到的内容称为兼容性模式，它提供了标准XDM与平台内使用方式之间的简单映射。

### 兼容性模式的工作原理

兼容性模式允许XDM JSON-LD模型通过更改标准XDM中的值，同时保持语义相同，与现有数据基础结构一起使用。 它使用嵌套的JSON结构，以类树格式显示模式。

标准XDM和兼容性模式之间的主要区别是删除了字段名称的“xdm:”前缀。

下面是一个并排比较，其中显示了标准XDM和兼容性模式中与生日相关的字段（已删除“description”属性）。 请注意，兼容性模式字段包括对“meta:xdmField”和“meta:xdmType”属性中XDM字段及其数据类型的引用。

<table>
  <th>标准XDM</th>
  <th>兼容性模式</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        { "xdm:birthDate":{ "title":“出生日期”、“类型”:"string", "format":"date", }, "xdm:birthDayAndMonth":{ "title":“出生日期”、“类型”:"string", "pattern":"[0-1][0-9]-[0-9][0-9]", }, "xdm:birthYear":{ "title":“出生年”,“类型”:“integer”、“minimum”:1, "maximum":32767 }
      </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        { "birthDate":{ "title":“出生日期”、“类型”:"string", "format":"date", "meta:xdmField":"xdm:birthDate", "meta:xdmType":"date" }, "birthDayAndMonth":{ "title":“出生日期”、“类型”:"string", "pattern":“[0-1][0-9]-[0-9][0-9]”,“meta:xdmField”:"xdm:birthDayAndMonth", "meta:xdmType":"string" }, "birthYear":{ "title":“出生年”,“类型”:“integer”、“minimum”:1, "maximum":32767, "meta:xdmField":"xdm:birthYear", "meta:xdmType":"short" }
      </pre>
  </td>
  </tr>
</table>

### 为什么需要兼容模式？

Adobe Experience Platform设计为可与多种解决方案和服务结合使用，每种解决方案和服务都有各自的技术挑战和限制（例如，某些技术如何处理特殊特征）。 为了克服这些限制，开发了兼容性模式。

大多数Experience Platform服务(包括目录、数据湖和实时客户用户档案)都使用兼容性模式代替标准XDM。 模式注册表API还使用兼容性模式，此文档中的示例都使用兼容性模式显示。

值得知道的是，标准XDM与在Experience Platform中操作的方式之间有映射，但这不应影响您对平台服务的使用。

开放源项目可供您使用，但在通过模式注册表与资源交互时，本文档中的API示例提供您应了解和遵循的最佳实践。

## 在API中定义XDM字段类型 {#field-types}

XDM模式使用JSON模式标准和基本字段类型进行定义，并对Experience Platform强制实施的字段名称进行附加约束。 XDM允许您通过使用格式和可选约束定义其他字段类型。 XDM字段类型由字段级属性显示 `meta:xdmType`。

>[!NOTE] 是系 `meta:xdmType` 统生成的值，因此您无需将此属性添加到字段的JSON中。 最佳实践是使用JSON模式类型（如字符串和整数），并按照下表中的定义设置相应的最小／最大约束。

下表概述了使用可选属性定义标量字段类型和更具体的字段类型的相应格式。 有关可选属性和类型特定关键字的更多信息，请通过 [JSON模式文档获取](https://json-schema.org/understanding-json-schema/reference/type.html)。

要开始，请查找所需的字段类型，并使用提供的示例代码构建API请求。

<table>
  <tr>
    <th>所需类型<br/>(meta:xdmType)</th>
    <th>JSON<br/>(JSON模式)</th>
    <th>代码示例</th>
  </tr>
  <tr>
    <td>字符串</td>
    <td>type:<br/><br/><strong>string可选属性：</strong><br/>
      <ul>
        <li>图案</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":"string", "pattern":"^[A-Z]{2}$", "maxLength":2 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>type:<br/>stringformat:uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":"string", "format":"uri" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType:字符串)</td>
    <td>type:<br/><br/><strong>stringOptional属性：</strong><br/>
      <ul>
        <li>默认</li>
      </ul>
    </td>
    <td>使用“meta:enum”指定面向客户的选项标签：
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":"string", "enum":[ "value1", "value2", "value3" ], "meta:enum:{ "value1":“值1”、“值2”:“值2”、“值3”:"Value 3" }, "default":"value1" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>数字</td>
    <td>type:最低<br/>数量：最大为±2.23×10^308<br/>:±1.80×10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":"number" }
      </pre>
    </td>
  </tr>
  <tr>
    <td>长</td>
    <td>type:最<br/>大积分：2^53+1<br>最小值：-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":“integer”、“minimum”:-9007199254740992, "maximum":9007199254740992 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>type:最<br/>大积分：2^31<br>最小值：-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":“integer”、“minimum”:-2147483648, "maximum":2147483648 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>短</td>
    <td>type:最<br/>大积分：2^15<br>最小值：-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":“integer”、“minimum”:-32768, "maximum":32768 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>字节</td>
    <td>type:最<br/>大积分：2^7<br>最小值：-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":“integer”、“minimum”:-128, "maximum":128 }
      </pre>
    </td>
  </tr>
  <tr>
    <td>布尔</td>
    <td><br/>type:boolean<br/>{true, false}可<br/><br/><strong>选属性：</strong><br/>
      <ul>
        <li>默认</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":“boolean”、“default”:false }
      </pre>
    </td>
  </tr>
  <tr>
    <td>date</td>
    <td>type:<br/>stringformat:date</td>
    <td>
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":"string", "format":“date”、“examples”:["2004-10-23"] }
      </pre>
      由 <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339第5.6节定义的日期，其中</a>“full-date” = date-fullyear "-" date-month "-" date-mday(YYYY-MM-DD)
    </td>
  </tr>
  <tr>
    <td>date-time</td>
    <td>type:<br/>stringformat:date-time</td>
    <td>
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":"string", "format":“date-time”、“examples”:["2004-10-23T12:00:00-06:00"] }
      </pre>
      Date-Time(由 <a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339第5.6节定义)，其中</a>“date-time”=完整日期“T”全时：<br/>(YYYY-MM-DD'T'HH:MM:SS.SSX)
    </td>
  </tr>
  <tr>
    <td>阵列</td>
    <td>type:阵列</td>
    <td>items.type可以使用任何标量类型定义：
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":“array”、“items”:{ "type":"string" } }
      </pre>
      由另一个模式定义的对象数组：<br/>
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":“array”、“items”:{ "$ref":"id" } }
      </pre>
      其中，“id”是引用模式的{id}。
    </td>
  </tr>
  <tr>
    <td>对象</td>
    <td>type:对象</td>
    <td>属性。{field}.type可以使用任何标量类型定义：
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":“object”、“properties”:{ "field1":{ "type":"string" }, "field2":{ "type":"number" } } }
      </pre>
      引用模式定义的“object”类型字段：
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":“对象”、“$ref”:"id" }
      </pre>
      其中，“id”是引用模式的{id}。
    </td>
  </tr>
  <tr>
    <td>地图</td>
    <td>type:对<br/><br/><strong>象注</strong><br/>意：“map”数据类型的使用是为行业和供应商模式的使用而保留的，不可用于租户定义的字段。 当数据表示为映射到某些值的键时，或者当键不能合理地包含在静态模式中且必须被视为数据值时，它会在标准模式中使用。</td>
    <td>“映射”不能定义任何属性。 它必须定义一个“additionalProperties”模式来描述“map”中包含的值类型。 XDM中的“map”只能包含单个数据类型。 值可以是任何有效的XDM模式定义，包括数组或对象，或作为对其他模式的引用（通过$ref）。<br/><br/>具有“string”类型的值的映射字段：
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":"object", "additionalProperties":{ "type":"string" } }
      </pre>
    映射字段，其值为字符串数组：
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":"object", "additionalProperties":{ "type":“array”、“items”:{ "type":"string" } } }
      </pre>
    引用其他模式的映射字段：
      <pre class="JSON language-JSON hljs">
        “sampleField”:{ "type":"object", "additionalProperties":{ "$ref":"id" } }
      </pre>
      其中，“id”是引用模式的{id}。
    </td>
  </tr>
</table>


## 将XDM类型映射到其他格式

下表介绍了“meta:xdmType”与其他序列化格式之间的映射。

| XDM类型<br>(meta:xdmType) | JSON<br>(JSON模式) | Parce<br>（类型／注释） | Spark SQL | Java | 斯卡拉 | .NET | CosmosDB | MongoDB | 塞式飞行器 | Protobuf 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| 字符串 | type:string | BYTE_ARRAY/UTF8 | StringType | java.lang.String | 字符串 | System.String | 字符串 | 字符串 | 字符串 | 字符串 |
| 数字 | 类型：数字 | 多次 | DoubleType | java.lang.多次 | 双精度 | 系统。多次 | 数值 | 多次 | 双精度 | 多次 |
| 长 | type:<br>integermaximum:2^53+1<br>minimum:-2^53+1 | INT64 | LongType | java.lang.Long | 长 | System.Int64 | 数值 | 长 | 整数 | int64 |
| int | type:<br>integermaximum:2^31<br>minimum:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | 数值 | int | 整数 | int32 |
| 短 | type:<br>integermaximum:2^15<br>minimum:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | 短 | System.Int16 | 数值 | int | 整数 | int32 |
| 字节 | type:<br>integermaximum:2^7<br>minimum:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | 字节 | System.SByte | 数值 | int | 整数 | int32 |
| 布尔 | 类型：布尔值 | BOOLEAN | BooleanType | java.lang.Boolean | Boolean | System.Boolean | Boolean | bool | 整数 | 整数 | bool |
| date | type:<br>stringformat:date<br>（RFC 3339，第5.6节） | INT32/日 | 日期类型 | java.util.Date | java.util.Date | System.DateTime | 字符串 | date | Integer<br>(unix millis) | int64<br>(unix millis) |
| date-time | type:<br>stringformat:date-time<br>（RFC 3339，第5.6节） | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | 字符串 | timestamp | Integer<br>(unix millis) | int64<br>(unix millis) |
| 地图 | 对象 | MAP annotated group<br><br>&lt;<span>key_type</span>> MUST be STRING<br><br>&lt;<span>value_type</span>> type of map values | MapType<br><br>&quot;keyType&quot; MUST be StringType<br><br>&quot;valueType&quot;是映射值的类型。 | java.util.Map | 地图 | --- | 对象 | 对象 | 地图 | map&lt;<span>key_type, value_type</span>> |

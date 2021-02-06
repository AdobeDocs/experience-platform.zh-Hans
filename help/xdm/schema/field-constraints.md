---
keywords: Experience Platform；主页；热门主题；模式;模式；混合；混合；混合；混合；混合；数据类型；数据类型；数据类型；模式设计；数据类型；数据类型；数据类型；数据类型；数据类型；模式;模式;模式设计；映射；
solution: Experience Platform
title: XDM字段类型约束
topic: overview
description: 对XDM字段类型约束的引用，包括可以映射到的其他序列化格式以及如何在API中定义您自己的字段类型。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 5%

---


# XDM字段类型约束

您为模式选择的XDM字段类型会限制这些字段可以包含的数据类型。 此文档概述了每个核心字段类型，包括可映射到的其他序列化格式，以及如何在API中定义您自己的字段类型以实施不同的约束。

## 入门指南

在使用本指南之前，请阅读[模式合成基础知识](./composition.md)，了解XDM模式、类和混音的简介。

如果您计划定义自己的字段类型，强烈建议您开始[模式注册表开发人员指南](../api/getting-started.md)，了解如何创建混音和数据类型以将自定义字段包含在中。

## 将XDM类型映射到其他格式

下表描述了每个XDM类型(`meta:xdmType`)与其他序列化格式之间的映射。

| XDM类型<br>(meta:xdmType) | JSON<br>(JSON模式) | Parce<br>（类型／注释） | [!DNL Spark] SQL | Java | 斯卡拉 | .NET | CosmosDB | MongoDB | 塞式飞行器 | Protobuf 2 |
|---|---|---|---|---|---|---|---|---|---|---|
| 字符串 | 类型：字符串 | BYTE_ARRAY/UTF8 | 字符串类型 | java.lang.String | 字符串 | System.String | 字符串 | 字符串 | 字符串 | 字符串 |
| 数字 | 类型：数字 | 多次 | DoubleType | java.lang.Double | 双精度 | System.Double | 数值 | 多次 | 双精度 | 多次 |
| 长 | type:integer<br>maximum:2^53+1<br>minimum:-2^53+1 | INT64 | LongType | java.lang.Long | 长 | System.Int64 | 数值 | 长 | 整数 | int64 |
| int | type:integer<br>maximum:2^31<br>minimum:-2^31 | INT32/INT_32 | IntegerType | java.lang.Integer | Int | System.Int32 | 数值 | int | 整数 | int32 |
| 短 | type:integer<br>maximum:2^15<br>minimum:-2^15 | INT32/INT_16 | ShortType | java.lang.Short | 短 | System.Int16 | 数值 | int | 整数 | int32 |
| 字节 | type:integer<br>maximum:2^7<br>minimum:-2^7 | INT32/INT_8 | ByteType | java.lang.Short | 字节 | System.SByte | 数值 | int | 整数 | int32 |
| 布尔 | 类型：布尔值 | 布尔值 | BooleanType | java.lang.Boolean | 布尔值 | System.Boolean | 布尔值 | bool | 整数 | 整数 | bool |
| 日期 | type:string<br>format:date<br>（RFC 3339，第5.6节） | INT32/日 | 日期类型 | java.util.Date | java.util.Date | System.DateTime | 字符串 | 日期 | 整数<br>(unix millis) | int64<br>(unix millis) |
| date-time | type:string<br>format:date-time<br>（RFC 3339，第5.6节） | INT64/TIMESTAMP_MILLIS | TimestampType | java.util.Date | java.util.Date | System.DateTime | 字符串 | timestamp | 整数<br>(unix millis) | int64<br>(unix millis) |
| 地图 | 对象 | MAP加注释的组<br><br>&lt;<span>key_type</span>必须是映射值的STRING<br><br><span>value_type</span>类型 | MapType<br><br>&quot;keyType&quot; MUST be StringType<br><br>&quot;valueType&quot;是映射值的类型。 | java.util.Map | 地图 | — | 对象 | 对象 | 地图 | map&lt;<span>key type, value_type</span>> |

## 在API {#define-fields}中定义XDM字段类型

XDM模式是使用[JSON模式](https://json-schema.org/)标准和基本字段类型定义的，并且对字段名称有附加约束，这些约束由[!DNL Experience Platform]实施。 [模式注册表API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)允许您通过使用格式和可选约束定义其他字段类型。 XDM字段类型由字段级属性`meta:xdmType`公开。

>[!NOTE]
>
>`meta:xdmType` 是系统生成的值，因此您无需将此属性添加到字段的JSON中。最佳实践是将JSON模式类型（如字符串和整数）与下表中定义的适当最小／最大约束一起使用。

下表概述了使用可选属性定义标量字段类型和更多特定字段类型的适当格式。 有关可选属性和类型特定关键字的详细信息，请通过[JSON模式文档](https://json-schema.org/understanding-json-schema/reference/type.html)获取。

首先，找到所需的字段类型，然后使用提供的示例代码构建API请求，以创建[的混音](../api/mixins.md#create)或[创建数据类型](../api/data-types.md#create)。

<table>
  <tr>
    <th>所需类型<br/>(meta:xdmType)</th>
    <th>JSON<br/>(JSON模式)</th>
    <th>代码示例</th>
  </tr>
  <tr>
    <td>字符串</td>
    <td>类型：string<br/><br/><strong>可选属性：</strong><br/>
      <ul>
        <li>图案</li>
        <li>minLength</li>
        <li>maxLength</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
            “类型”:"string",
            “模式”:"^[A-Z]{2}$",
            “maxLength”:2
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>uri<br/>(xdmType:string)</td>
    <td>类型：string<br/>格式：uri</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          “类型”:"string",
          “格式”:"uri"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>enum<br/>(xdmType:字符串)</td>
    <td>类型：string<br/><br/><strong>可选属性：</strong><br/>
      <ul>
        <li>默认</li>
      </ul>
    </td>
    <td>使用“meta:enum”指定面向客户的选项标签：
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          “类型”:"string",
          “枚举”:[
              "value1",
              "value2",
              "value3"
          ],
          "meta:enum":{
              "value1":"值1",
              "value2":"值2",
              "value3":"值3"
          },
          “默认”:"value1"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>数字</td>
    <td>类型：number<br/>最小：±2.23×10^308<br/>最大值：±1.80×10^308</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          “类型”:"number"
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>长</td>
    <td>类型：integer<br/>maximum:2^53+1<br>minimum:-2^53+1</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          “类型”:"integer",
          “最小”:-9007199254740992,
          “maximum”:9007199254740992
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>int</td>
    <td>类型：integer<br/>maximum:2^31<br>minimum:-2^31</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          “类型”:"integer",
          “最小”:-2147483648,
          “maximum”:2147483648
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>短</td>
    <td>类型：integer<br/>maximum:2^15<br>minimum:-2^15</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          “类型”:"integer",
          “最小”:-32768,
          “maximum”:32768
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>字节</td>
    <td>类型：integer<br/>maximum:2^7<br>minimum:-2^7</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          “类型”:"integer",
          “最小”:-128,
          “maximum”:128
          }
      </pre>
    </td>
  </tr>
  <tr>
    <td>布尔</td>
    <td><br/>类型：boolean<br/>{true, false}<br/><br/><strong>可选属性：</strong><br/>
      <ul>
        <li>默认</li>
      </ul>
    </td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          “类型”:"boolean",
          “默认”:假
        }
      </pre>
    </td>
  </tr>
  <tr>
    <td>日期</td>
    <td>类型：string<br/>格式：日期</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          “类型”:"string",
          “格式”:“日期”,
          “示例”:["2004-10-23"]
        }
      </pre>
      由<a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339第5.6</a>节定义的日期，其中"full-date" = date-fullyear "-" date-month "-" date-mday(YYYY-MM-DD)
    </td>
  </tr>
  <tr>
    <td>date-time</td>
    <td>类型：string<br/>格式：date-time</td>
    <td>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          “类型”:"string",
          “格式”:"date time",
          “示例”:["2004-10-23T12:00:00-06:00"]
        }
      </pre>
      Date-Time，由<a href="https://tools.ietf.org/html/rfc3339#section-5.6" target="_blank">RFC 3339第5.6</a>节定义，其中"date-time" =完整日期"T"全时：<br/>(YYYY-MM-DD'T'HH:MM:SS.SSX)
    </td>
  </tr>
  <tr>
    <td>阵列</td>
    <td>类型：阵列</td>
    <td>items.type可使用任何标量类型定义：
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          “类型”:"array",
          “项目”:{
            “类型”:"字符串"
          }
        }
      </pre>
      由另一个模式定义的对象数组：<br/>
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          “类型”:"array",
          “项目”:{
            “$ref”:"id"
          }
        }
      </pre>
      其中“id”是引用模式的{id}。
    </td>
  </tr>
  <tr>
    <td>对象</td>
    <td>类型：对象</td>
    <td>属性。{field}.type可以使用任何标量类型定义：
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          “类型”:“对象”、
          “属性”:{
            "field1":{
              “类型”:"字符串"
            },
            "field2":{
              “类型”:"number"
            }
          }
        }
      </pre>
      引用模式定义的“object”类型字段：
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          “类型”:“对象”、
          “$ref”:"id"
        }
      </pre>
      其中“id”是引用模式的{id}。
    </td>
  </tr>
  <tr>
    <td>地图</td>
    <td>类型：object<br/><br/><strong>注意：</strong><br/>使用“map”数据类型是为行业和供应商模式使用而保留的，不能用于租户定义的字段。 当数据表示为映射到某个值的键时，或者在静态模式中无法合理包含键并且必须作为数据值时，它将在标准模式中使用。</td>
    <td>“map”不能定义任何属性。 它必须定义单个“[!UICONTROL additionalProperties]”模式来描述“map”中包含的值类型。 XDM中的“map”只能包含单个数据类型。 值可以是任何有效的XDM模式定义，包括数组或对象，或作为对其他模式的引用（通过$ref）。<br/><br/>具有“string”类型值的映射字段：
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          “类型”:“对象”、
          "additionalProperties":{
            “类型”:"字符串"
          }
        }
      </pre>
    值为字符串数组的映射字段：
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          “类型”:“对象”、
          "additionalProperties":{
            “类型”:"array",
            “项目”:{
              “类型”:"字符串"
            }
          }
        }
      </pre>
    引用其他模式的映射字段：
      <pre class="JSON language-JSON hljs">
        "sampleField":{
          “类型”:“对象”、
          "additionalProperties":{
            “$ref”:"id"
          }
        }
      </pre>
      其中“id”是引用模式的{id}。
    </td>
  </tr>
</table>

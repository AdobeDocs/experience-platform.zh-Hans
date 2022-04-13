---
title: 在架构注册API中定义XDM字段
description: 了解在架构注册API中创建自定义体验数据模型(XDM)资源时如何定义不同的字段。
exl-id: d79332e3-8448-42af-b250-882bcb0f1e7d
source-git-commit: 536657f11a50ea493736296780dd57f41dfefeae
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# 在架构注册API中定义XDM字段

所有体验数据模型(XDM)字段均使用标准 [JSON架构](https://json-schema.org/) 应用于其字段类型的约束，以及Adobe Experience Platform强制实施的对字段名称的其他约束。 架构注册表API允许您通过使用格式和可选约束来定义架构中的自定义字段。 XDM字段类型由字段级别属性公开， `meta:xdmType`.

>[!NOTE]
>
>`meta:xdmType` 是系统生成的值，因此在使用API时，您无需将此属性添加到字段的JSON中(除非 [创建自定义映射类型](#maps))。 最佳实践是使用JSON架构类型(例如 `string` 和 `integer`)，并且具有下表中定义的相应最小/最大约束。

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
    <td>映射类型字段本质上是具有不受约束键集的对象类型字段。 与对象一样，映射具有 <code>type</code> 值 <code>object</code>但是 <code>meta:xdmType</code> 显式设置为 <code>map</code>.<br><br>地图 <strong>必须</strong> 定义任何属性。 它 <strong>必须</strong> 定义单个 <code>additionalProperties</code> 用于描述映射中包含的值类型的架构（每个映射只能包含单个数据类型）。 的 <code>type</code> 值必须为 <code>string</code> 或 <code>integer</code>.<br/><br/>具有字符串类型值的映射字段：
      <pre class="JSON language-JSON hljs">
"sampleField":{ "type":"object", "meta:xdmType":"map", "additionalProperties":{ "type":"string" } }</pre>
    有关在XDM中创建自定义映射类型的更多信息，请参阅以下部分。
    </td>
  </tr>
</table>

## 创建自定义映射类型 {#maps}

为了在XDM中高效地支持“类似地图”数据，可以使用 `meta:xdmType` 设置为 `map` 要明确说明应当像对键集不受约束一样管理对象。 摄取到映射字段中的数据必须使用字符串键，并且只能使用字符串或整数值(由 `additionalProperties.type`)。

XDM对使用此存储提示施加了以下限制：

* 映射类型MUST为类型 `object`.
* 映射类型必须不定义属性（换句话说，它们定义“空”对象）。
* 映射类型必须包括 `additionalProperties.type` 字段，用于描述可能放置在映射中的值， `string` 或 `integer`.

请确保您只在绝对必要时才使用映射类型字段，因为这些字段存在以下性能缺陷：

* 对于1亿条记录，Adobe Experience Platform查询服务的响应时间会从3秒降为10秒。
* 地图必须少于16个键值，否则就有进一步退化的风险。

平台用户界面在如何提取映射类型字段的键值方面也存在限制。 对象类型字段可以展开，而映射显示为单个字段。

## 后续步骤

本指南介绍如何在API中定义不同的字段类型。 有关XDM字段类型的格式的详细信息，请参阅 [XDM字段类型约束](../schema/field-constraints.md).

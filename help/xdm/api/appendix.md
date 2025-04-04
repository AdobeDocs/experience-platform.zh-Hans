---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；体验数据模型；数据模型；数据模型；架构注册表；架构注册表；兼容性；兼容性；兼容模式；兼容模式；字段类型；字段类型；
solution: Experience Platform
title: 架构注册表API指南附录
description: 本文档提供有关使用架构注册表API的补充信息。
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 0%

---

# 架构注册表API指南附录

本文档提供有关使用[!DNL Schema Registry] API的补充信息。

## 使用查询参数 {#query}

[!DNL Schema Registry]支持在列出资源时使用查询参数来页面和筛选结果。

>[!NOTE]
>
>组合多个查询参数时，必须用&amp;符号(`&`)分隔。

### 分页 {#paging}

分页最常见的查询参数包括：

| 参数 | 描述 |
| --- | --- |
| `orderby` | 按特定属性对结果进行排序。 示例：`orderby=title`将按标题以升序(A-Z)对结果进行排序。 在参数值(`orderby=-title`)之前添加`-`将按标题降序(Z-A)对项排序。 |
| `limit` | 当与`orderby`参数一起使用时，`limit`限制给定请求应返回的最大项目数。 如果没有`orderby`参数，则无法使用此参数。<br><br>参数`limit`指定正整数（介于`0`和`500`之间）作为&#x200B;*提示*，表示应返回的最大项数。 例如，`limit=5`在列表中只返回五个资源。 但是，不会严格遵循此值。 实际响应大小可以小于或大于，因为需要提供`start`参数的可靠操作而受此限制（如果提供）。 |
| `start` | 当与`orderby`参数一起使用时，`start`指定子设置的项目列表的开始位置。 如果没有`orderby`参数，则无法使用此参数。 此值可从列表响应的`_page.next`属性中获取，并用于访问结果的下一页。 如果`_page.next`值为null，则表示没有其他页面可用。<br><br>通常省略此参数以获取结果的第一页。 之后，`start`应设置为在上一页收到的`orderby`字段的主排序属性的最大值。 然后，API响应返回以主排序属性从`orderby`开始并严格大于（对于升序）或严格小于（对于降序）指定值的条目。<br><br>例如，如果`orderby`参数设置为`orderby=name,firstname`，则`start`参数将包含`name`属性的值。 在这种情况下，如果您想在名称“Miller”之后立即显示资源的后20个条目，则可以使用： `?orderby=name,firstname&start=Miller&limit=20`。 |

{style="table-layout:auto"}

### 筛选 {#filtering}

您可以使用`property`参数筛选结果，该参数用于针对检索到的资源中的给定JSON属性应用特定运算符。 支持的运算符包括：

| 操作员 | 描述 | 示例 |
| --- | --- | --- |
| `==` | 按属性是否等于提供的值筛选。 | `property=title==test` |
| `!=` | 按属性是否不等于提供的值筛选。 | `property=title!=test` |
| `<` | 根据属性是否小于提供的值来进行筛选。 | `property=version<5` |
| `>` | 按属性是否大于提供的值筛选。 | `property=version>5` |
| `<=` | 根据属性是否小于或等于提供的值来进行筛选。 | `property=version<=5` |
| `>=` | 按属性是否大于或等于提供的值筛选。 | `property=version>=5` |
| （无） | 仅声明属性名称将只返回属性存在的条目。 | `property=title` |

{style="table-layout:auto"}

>[!TIP]
>
>您可以使用`property`参数按架构字段组的兼容类筛选架构字段组。 例如，`property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile`只返回与[!DNL XDM Individual Profile]类兼容的字段组。

## 兼容模式 {#compatibility}

[!DNL Experience Data Model] (XDM)是一个公开记录的规范，由Adobe驱动，用于提高数字体验的互操作性、表现性和强大功能。 Adobe在GitHub](https://github.com/adobe/xdm/)上的[开源项目中维护源代码和正式XDM定义。 这些定义使用XDM标准表示法编写，并使用JSON-LD(链接数据的JavaScript对象表示法)和JSON Schema作为定义XDM架构的语法。

在公共存储库中查看正式XDM定义时，您可以看到标准XDM与您在Adobe Experience Platform中看到的不同。 您在[!DNL Experience Platform]中看到的内容称为兼容性模式，它提供了标准XDM与[!DNL Experience Platform]中使用该模式的方式之间的简单映射。

### 兼容模式的工作原理

兼容模式允许XDM JSON-LD模型通过更改标准XDM中的值同时保持语义相同来与现有数据基础结构一起使用。 它使用嵌套的JSON结构，以树状格式显示架构。

您会注意到标准XDM和兼容模式之间的主要区别是删除了字段名称的“xdm：”前缀。

以下并排比较显示在标准XDM和兼容性模式中与生日相关的字段（删除了“description”属性）。 请注意，兼容性模式字段包括对XDM字段的引用，以及它在“meta：xdmField”和“meta：xdmType”属性中的数据类型。

<table style="table-layout:auto">
  <th>标准XDM</th>
  <th>兼容模式</th>
  <tr>
  <td>
  <pre class=" language-json">
{
  "xdm：birthDate"： {
    "title"： "Birth Date"，
    "type"： "string"，
    "format"： "date"
  }，
  "xdm：birthDayAndMonth"： {
    "title"： "Birth Date"，
    "type"： "string"，
    "pattern"： "[0-1][0-9]-[0-9][0-9]"
  }，
  "xdm：birthYear"： {
    "title"： "Birth year"，
    "type"： "integer"，
    “最小值”：1，
    "maximum"： 32767
  }
}
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{
  "birthDate"： {
    "title"： "Birth Date"，
    "type"： "string"，
    "format"： "date"，
    "meta：xdmField"： "xdm：birthDate"，
    "meta：xdmType"： "date"
  }，
  "birthDayAndMonth"： {
    "title"： "Birth Date"，
    "type"： "string"，
    "pattern"： "[0-1][0-9]-[0-9][0-9]"，
    "meta：xdmField"： "xdm：birthDayAndMonth"，
    "meta：xdmType"： "string"
  }，
  "birthYear"： {
    "title"： "Birth year"，
    "type"： "integer"，
    “最小值”：1，
    "maximum"：32767，
    "meta：xdmField"： "xdm：birthYear"，
    "meta：xdmType"： "short"
  }
}
      </pre>
  </td>
  </tr>
</table>

### 为什么需要兼容模式？

Adobe Experience Platform设计为可与多种解决方案和服务配合使用，每种解决方案和服务都有各自的技术挑战和限制（例如，某些技术如何处理特殊字符）。 为了克服这些限制，开发了兼容模式。

大多数[!DNL Experience Platform]服务（包括[!DNL Catalog]、[!DNL Data Lake]和[!DNL Real-Time Customer Profile]）都使用[!DNL Compatibility Mode]代替标准XDM。 [!DNL Schema Registry] API也使用[!DNL Compatibility Mode]，此文档中的示例全部使用[!DNL Compatibility Mode]显示。

需要了解的是，映射在标准XDM与在[!DNL Experience Platform]中操作的方式之间发生，但它不应影响您对[!DNL Experience Platform]服务的使用。

开放源代码项目可供您使用，但涉及通过[!DNL Schema Registry]与资源交互时，本文档中的API示例提供了您应了解和遵循的最佳实践。

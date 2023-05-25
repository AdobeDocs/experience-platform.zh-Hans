---
keywords: Experience Platform；主页；热门主题；API；API；XDM；XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；架构注册表；架构注册表；兼容性；兼容性；兼容模式；兼容模式；字段类型；字段类型；
solution: Experience Platform
title: 架构注册表API指南附录
description: 本文档提供有关使用架构注册表API的补充信息。
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 0%

---

# 架构注册表API指南附录

本文档提供了与使用 [!DNL Schema Registry] API。

## 使用查询参数 {#query}

此 [!DNL Schema Registry] 支持在列出资源时使用查询参数来分页和筛选结果。

>[!NOTE]
>
>组合多个查询参数时，必须使用&amp;符号(`&`)。

### 分页 {#paging}

分页最常见的查询参数包括：

| 参数 | 描述 |
| --- | --- |
| `orderby` | 按特定属性对结果进行排序。 示例： `orderby=title` 将按标题对结果进行升序(A-Z)排序。 添加 `-` 在参数值之前(`orderby=-title`)将按标题对项目进行降序排序(Z-A)。 |
| `limit` | 当与 `orderby` 参数， `limit` 限制给定请求应返回的最大项目数。 如果没有参数，不能使用此参数 `orderby` 参数存在。<br><br>此 `limit` 参数指定一个正整数(介于 `0` 和 `500`) as a *提示* 应返回的项目的最大数量。 例如， `limit=5` 仅返回列表中的五个资源。 但是，不会严格遵循此值。 实际响应大小可以小于或大于，因为需要提供可靠的运行 `start` 参数（如果有）。 |
| `start` | 当与 `orderby` 参数， `start` 指定子设置的项目列表的开始位置。 如果没有参数，不能使用此参数 `orderby` 参数存在。 此值可从以下位置获取： `_page.next` 列表响应的属性，用于访问结果的下一页。 如果 `_page.next` 值为null，则没有其他可用页面。<br><br>通常，为获取结果的第一页，将忽略此参数。 之后， `start` 应设置为的主排序属性的最大值 `orderby` 在上一页接收的字段。 然后，API响应返回以具有来自的主要排序属性的条目开头的条目 `orderby` 严格大于（对于升序）或严格小于（对于降序）指定的值。<br><br>例如，如果 `orderby` 参数设置为 `orderby=name,firstname`，则 `start` 参数将包含 `name` 属性。 在这种情况下，如果要紧跟名称“Miller”显示资源的接下来的20个条目，则可以使用： `?orderby=name,firstname&start=Miller&limit=20`. |

{style="table-layout:auto"}

### 正在筛选 {#filtering}

您可以使用以下方式筛选结果： `property` 参数，用于对检索到的资源中的给定JSON属性应用特定运算符。 支持的运算符包括：

| 操作员 | 描述 | 示例 |
| --- | --- | --- |
| `==` | 按属性是否等于提供的值筛选。 | `property=title==test` |
| `!=` | 按属性是否不等于提供的值筛选。 | `property=title!=test` |
| `<` | 按属性是否小于提供的值筛选。 | `property=version<5` |
| `>` | 按属性是否大于提供的值筛选。 | `property=version>5` |
| `<=` | 按属性是否小于或等于提供的值来筛选。 | `property=version<=5` |
| `>=` | 按属性是否大于或等于提供的值筛选。 | `property=version>=5` |
| `~` | 按属性是否与提供的正则表达式匹配进行筛选。 | `property=title~test$` |
| (None) | 仅声明属性名称将只返回属性存在的条目。 | `property=title` |

{style="table-layout:auto"}

>[!TIP]
>
>您可以使用 `property` 用于按架构字段组的兼容类筛选架构字段组的参数。 例如， `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` 仅返回与兼容的字段组 [!DNL XDM Individual Profile] 类。

## 兼容模式 {#compatibility}

[!DNL Experience Data Model] (XDM)是一个公开记录的规范，由Adobe驱动，用于提高数字体验的互操作性、表达性和强大功能。 Adobe在中维护源代码和正式XDM定义 [GitHub上的开源项目](https://github.com/adobe/xdm/). 这些定义以XDM标准表示法编写，使用JSON-LD（链接数据的JavaScript对象表示法）和JSON架构作为定义XDM架构的语法。

在公共存储库中查看正式XDM定义时，您可以看到标准XDM与您在Adobe Experience Platform中看到的不同。 您在中看到的内容 [!DNL Experience Platform] 称为兼容模式，它提供了标准XDM与其使用方式之间的简单映射 [!DNL Platform].

### 兼容模式的工作原理

兼容性模式允许XDM JSON-LD模型通过更改标准XDM中的值同时保持语义相同来与现有数据基础架构配合使用。 它使用嵌套JSON结构，以树状格式显示架构。

您会注意到标准XDM和兼容模式之间的主要区别是删除了字段名称的“xdm：”前缀。

以下并排比较显示在标准XDM和兼容性模式中与生日相关的字段（删除了“描述”属性）。 请注意，兼容模式字段包括对XDM字段的引用，以及其“meta：xdmField”和“meta：xdmType”属性中的数据类型。

<table style="table-layout:auto">
  <th>标准XDM</th>
  <th>兼容模式</th>
  <tr>
  <td>
  <pre class=" language-json">
{ "xdm：birthDate"： { "title"： "Birth Date"， "type"： "string"， "format"： "date" }， "xdm：birthDayAndMonth"： { "title"： "Birth Date"， "type"： "string"， "pattern"： "[0-1][0-9]-[0-9][0-9]" }， "xdm：birthYear"： { "title"： "Birth year"， "type"： "integer"： 1， "maximimimum"： 32767 } } }
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{ "birthDate"： { "title"： "Birth Date"， "type"： "string"， "format"： "date"， "meta：xdmField"： "xdm：birthDate"， "meta：xdmType"： "date" }， "birthDayAndMonth"： { "title"： "Birth Date"， "type"： "string"， "pattern"： "[0-1][0-9]-[0-9]"， "meta：xdmField"： "xdm：birthDayAnd"， meta：xdmType"： "string" }， "birthYear"： { "title"： "Birth year"， "type"： "integer"， "minimum"： 1， "maximum"： 32767， "meta：xdmField"： "xdm：birthYear"， "meta：xdmType"： "short" }
      </pre>
  </td>
  </tr>
</table>

### 为什么需要兼容模式？

Adobe Experience Platform设计为可与多种解决方案和服务配合使用，而每种解决方案和服务都有各自的技术挑战和限制（例如，某些技术如何处理特殊字符）。 为了克服这些限制，开发了兼容模式。

最多 [!DNL Experience Platform] 服务包括 [!DNL Catalog]， [!DNL Data Lake]、和 [!DNL Real-Time Customer Profile] 使用 [!DNL Compatibility Mode] 代替标准XDM。 此 [!DNL Schema Registry] API还使用 [!DNL Compatibility Mode]，本文档中的示例均使用 [!DNL Compatibility Mode].

值得一提的是，在标准XDM及其操作方式之间会进行映射 [!DNL Experience Platform]，但它应该不会影响您的使用 [!DNL Platform] 服务。

开放源码项目可供您使用，但是当涉及通过与资源交互时， [!DNL Schema Registry]，本文档中的API示例提供了您应了解和遵循的最佳实践。

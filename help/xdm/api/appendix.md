---
keywords: Experience Platform；主页；热门主题；API;XDM;XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；模式注册表；模式注册表；兼容性；兼容性；兼容性模式；兼容性模式；兼容性模式；字段类型；字段类型；
solution: Experience Platform
title: 架构注册API指南附录
description: 本文档提供了与使用架构注册表API相关的补充信息。
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 1%

---

# 架构注册API指南附录

本文档提供了与使用 [!DNL Schema Registry] API。

## 使用查询参数 {#query}

的 [!DNL Schema Registry] 支持在列出资源时使用查询参数来筛选页面和结果。

>[!NOTE]
>
>组合多个查询参数时，必须用与号(`&`)。

### 分页 {#paging}

用于分页的最常见查询参数包括：

| 参数 | 描述 |
| --- | --- |
| `orderby` | 按特定属性对结果排序。 示例： `orderby=title` 将按标题以升序(A-Z)对结果进行排序。 添加 `-` 在参数值(`orderby=-title`)将按标题以降序(Z-A)对项目进行排序。 |
| `limit` | 与 `orderby` 参数， `limit` 限制为给定请求应返回的最大项目数。 如果没有 `orderby` 参数存在。<br><br>的 `limit` 参数指定正整数(介于 `0` 和 `500`)as a *提示* 至应返回的最大项目数。 例如， `limit=5` 仅返回列表中的5个资源。 但是，此值并不严格遵循。 实际响应尺寸可以是小于或大于，因为需要提供可靠的操作 `start` 参数（如果提供）。 |
| `start` | 与 `orderby` 参数， `start` 指定项目子集列表的开始位置。 如果没有 `orderby` 参数存在。 此值可从 `_page.next` 列表响应的属性，用于访问结果的下一页。 如果 `_page.next` 值为null，则没有其他页面可用。<br><br>通常，为获取结果的第一页，会忽略此参数。 之后， `start` 应设置为 `orderby` 字段。 然后，API响应会返回以具有中主排序属性的条目开头的条目 `orderby` 严格大于（升序）或严格小于（降序）指定值。<br><br>例如，如果 `orderby` 参数设置为 `orderby=name,firstname`, `start` 参数将包含 `name` 属性。 在这种情况下，如果您希望在名称“Miller”后立即显示资源的后20个条目，则可以使用： `?orderby=name,firstname&start=Miller&limit=20`. |

{style=&quot;table-layout:auto&quot;}

### 正在筛选 {#filtering}

您可以使用 `property` 参数，用于在检索的资源中对给定JSON属性应用特定运算符。 支持的运算符包括：

| 运算符 | 描述 | 示例 |
| --- | --- | --- |
| `==` | 按属性是否等于提供的值进行筛选。 | `property=title==test` |
| `!=` | 按属性是否不等于提供的值进行筛选。 | `property=title!=test` |
| `<` | 按属性是否小于提供的值进行筛选。 | `property=version<5` |
| `>` | 按属性是否大于提供的值进行筛选。 | `property=version>5` |
| `<=` | 按属性是否小于或等于提供的值进行筛选。 | `property=version<=5` |
| `>=` | 按属性是否大于或等于提供的值进行筛选。 | `property=version>=5` |
| `~` | 按属性是否与提供的正则表达式匹配进行筛选。 | `property=title~test$` |
| (None) | 仅声明属性名称仅返回存在属性的条目。 | `property=title` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>您可以使用 `property` 用于按其兼容类筛选架构字段组的参数。 例如， `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` 仅返回与兼容的字段组 [!DNL XDM Individual Profile] 类。

## 兼容性模式 {#compatibility}

[!DNL Experience Data Model] (XDM)是一项公开记录的规范，由Adobe驱动，旨在提高数字体验的互操作性、表现力和功能。 Adobe在 [GitHub上的开源项目](https://github.com/adobe/xdm/). 这些定义以XDM标准符号编写，使用JSON-LD（链接数据的JavaScript对象符号）和JSON模式作为定义XDM模式的语法。

在公共存储库中查看正式的XDM定义时，您可以看到标准XDM与在Adobe Experience Platform中看到的不同。 您在中看到的内容 [!DNL Experience Platform] 称为兼容模式，它提供了标准XDM与内部使用方式之间的简单映射 [!DNL Platform].

### 兼容性模式的工作原理

兼容性模式允许XDM JSON-LD模型通过更改标准XDM中的值来使用现有数据基础结构，同时保持语义相同。 它使用嵌套的JSON结构，以类似树的格式显示架构。

在标准XDM和兼容性模式之间，您会注意到的主要区别是删除了字段名称的“xdm：”前缀。

下面是一个并排比较，其中显示了标准XDM和兼容性模式中与生日相关的字段（删除了“描述”属性）。 请注意，兼容模式字段包括对“meta:xdmField”和“meta:xdmType”属性中XDM字段及其数据类型的引用。

<table style="table-layout:auto">
  <th>标准XDM</th>
  <th>兼容性模式</th>
  <tr>
  <td>
  <pre class=" language-json">
{ "xdm:birthDate":{ "title":“出生日期”、“类型”："string", "format":"date" }, "xdm:birthDayAndMonth":{ "title":“出生日期”、“类型”："string", "pattern":"[0-1][0-9]-[0-9][0-9]" }, "xdm:pirthYear":{ "title":“出生年”、“类型”："integer", "minimum":1, "maximum":32767 }
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{ "birthDate":{ "title":“出生日期”、“类型”："string", "format":"date", "meta:xdmField":"xdm:birthDate", "meta:xdmType":"date" }, "birthDayAndMonth":{ "title":“出生日期”、“类型”："string", "pattern":“[0-1][0-9]-[0-9][0-9]”，“meta:xdmField”："xdm:birthDayAndMonth", "meta:xdmType":"string" }, "birthYear":{ "title":“出生年”、“类型”："integer", "minimum":1, "maximum":32767, "meta:xdmField":"xdm:birthYear", "meta:xdmType":"short" }
      </pre>
  </td>
  </tr>
</table>

### 为何需要兼容模式？

Adobe Experience Platform旨在与多个解决方案和服务结合使用，每个解决方案和服务都有各自的技术挑战和限制（例如，某些技术如何处理特殊字符）。 为了克服这些限制，开发了兼容性模式。

最多 [!DNL Experience Platform] 服务包括 [!DNL Catalog], [!DNL Data Lake]和 [!DNL Real-Time Customer Profile] use [!DNL Compatibility Mode] 代替标准XDM。 的 [!DNL Schema Registry] API还使用 [!DNL Compatibility Mode]，本文档中的示例全部使用 [!DNL Compatibility Mode].

有必要知道，标准XDM与其在中的操作方式之间存在映射 [!DNL Experience Platform]，但不应影响您的使用 [!DNL Platform] 服务。

您可以使用开源项目，但是当涉及通过与资源交互时， [!DNL Schema Registry]，本文档中的API示例提供了您应了解和遵循的最佳实践。

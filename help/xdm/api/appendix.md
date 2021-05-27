---
keywords: Experience Platform；主页；热门主题；API;XDM;XDM系统；体验数据模型；体验数据模型；体验数据模型；数据模型；数据模型；模式注册表；模式注册表；兼容性；兼容性；兼容性模式；兼容性模式；兼容性模式；字段类型；字段类型；
solution: Experience Platform
title: 架构注册API指南附录
description: 本文档提供了与使用架构注册表API相关的补充信息。
topic-legacy: developer guide
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---

# 架构注册API指南附录

本文档提供了与使用[!DNL Schema Registry] API相关的补充信息。

## 使用查询参数 {#query}

[!DNL Schema Registry]支持在列出资源时使用查询参数来筛选页面和结果。

>[!NOTE]
>
>组合多个查询参数时，必须用与号(`&`)分隔。

### 分页 {#paging}

用于分页的最常见查询参数包括：

| 参数 | 描述 |
| --- | --- |
| `start` | 指定列出的结果的开始位置。 此值可从列表响应的`_page.next`属性中获取，并用于访问下一页结果。 如果`_page.next`值为null，则没有其他页面可用。 |
| `limit` | 限制返回的资源数。 示例：`limit=5`将返回五个资源的列表。 |
| `orderby` | 按特定属性对结果排序。 示例：`orderby=title`将按标题以升序(A-Z)对结果排序。 在参数值(`orderby=-title`)之前添加`-`将按标题以降序(Z-A)对项目进行排序。 |

{style=&quot;table-layout:auto&quot;}

### 筛选 {#filtering}

您可以使用`property`参数筛选结果，该参数用于对检索资源中的给定JSON属性应用特定运算符。 支持的运算符包括：

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
>可以使用`property`参数按其兼容类筛选架构字段组。 例如，`property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile`只返回与[!DNL XDM Individual Profile]类兼容的字段组。

## 兼容性模式 {#compatibility}

[!DNL Experience Data Model] (XDM)是一项公开记录的规范，由Adobe驱动，旨在提高数字体验的互操作性、表现力和功能。Adobe在GitHub](https://github.com/adobe/xdm/)上的[开源项目中维护源代码和正式的XDM定义。 这些定义以XDM标准符号编写，使用JSON-LD（链接数据的JavaScript对象符号）和JSON模式作为定义XDM模式的语法。

在公共存储库中查看正式的XDM定义时，您可以看到标准XDM与在Adobe Experience Platform中看到的不同。 您在[!DNL Experience Platform]中看到的内容称为兼容模式，它在标准XDM与在[!DNL Platform]中使用方式之间提供了简单的映射。

### 兼容性模式的工作原理

兼容性模式允许XDM JSON-LD模型通过更改标准XDM中的值来使用现有数据基础结构，同时保持语义相同。 它使用嵌套的JSON结构，以类似树的格式显示架构。

在标准XDM和兼容性模式之间，您会注意到的主要区别是删除了字段名称的“xdm：”前缀。

下面是一个并排比较，其中显示了标准XDM和兼容性模式中与生日相关的字段（删除了“描述”属性）。 请注意，兼容模式字段包括对“meta:xdmField”和“meta:xdmType”属性中XDM字段及其数据类型的引用。

<table style="table-layout:auto">
  <th>标准XDM</th>
  <th>兼容性模式</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        {
          "xdm:birthDate":{
              "title":"出生日期",
              "type":"string",
              "format":"date",
          },
          "xdm:birthDayAndMonth":{
              "title":"出生日期",
              "type":"string",
              "pattern":"[0-1][0-9]-[0-9][0-9]",
          },
          "xdm:birthYear":{
              "title":"出生年"
              "type":"integer",
              "minimum":1,
              "maximum":32767
        }
  </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        {
          "birthDate":{
              "title":"出生日期",
              "type":"string",
              "format":"date",
              "meta:xdmField":"xdm:birthDate",
              "meta:xdmType":"date"
          },
          "birthDayAndMonth":{
              "title":"出生日期",
              "type":"string",
              "pattern":"[0-1][0-9]-[0-9][0-9]",
              "meta:xdmField":"xdm:birthDayAndMonth",
              "meta:xdmType":"string"
          },
          "birthYear":{
              "title":"出生年"
              "type":"integer",
              "minimum":1,
              "maximum":32767,
              "meta:xdmField":"xdm:birthYear",
              "meta:xdmType":"short"
        }
      </pre>
  </td>
  </tr>
</table>

### 为何需要兼容模式？

Adobe Experience Platform旨在与多个解决方案和服务结合使用，每个解决方案和服务都有各自的技术挑战和限制（例如，某些技术如何处理特殊字符）。 为了克服这些限制，开发了兼容性模式。

大多数[!DNL Experience Platform]服务（包括[!DNL Catalog]、[!DNL Data Lake]和[!DNL Real-time Customer Profile]）使用[!DNL Compatibility Mode]代替标准XDM。 [!DNL Schema Registry] API还使用[!DNL Compatibility Mode]，本文档中的示例全部使用[!DNL Compatibility Mode]显示。

您应该知道，标准XDM与在[!DNL Experience Platform]中运行它的方式之间存在映射，但这不应影响您对[!DNL Platform]服务的使用。

开源项目可供您使用，但是当涉及通过[!DNL Schema Registry]与资源交互时，本文档中的API示例提供了您应该了解和遵循的最佳实践。

---
keywords: Experience Platform；主页；热门主题；API;XDM;XDM系统；体验数据模型；体验数据模型；数据模型；模式注册；模式注册；兼容性；兼容性模式；兼容性模式；字段类型；字段类型；
solution: Experience Platform
title: 模式注册表API指南附录
description: 本文档提供与使用模式 Registry API相关的补充信息。
topic-legacy: developer guide
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# 模式注册表API指南附录

本文档提供与使用[!DNL Schema Registry] API相关的补充信息。

## 使用查询参数{#query}

[!DNL Schema Registry]支持在列出资源时使用查询参数来筛选结果。

>[!NOTE]
>
>组合多个查询参数时，必须用&amp;符号(`&`)分隔。

### 分页{#paging}

用于分页的最常见查询参数包括：

| 参数 | 描述 |
| --- | --- |
| `start` | 指定列出的结果的开始位置。 此值可以从列表响应的`_page.next`属性中获取，并用于访问结果的下一页。 如果`_page.next`值为null，则没有其他页可用。 |
| `limit` | 限制返回的资源数。 示例：`limit=5`将返回一个包含5个资源的列表。 |
| `orderby` | 按特定属性对结果排序。 示例：`orderby=title`将按标题按升序(A-Z)对结果排序。 在参数值(`orderby=-title`)之前添加`-`将按降序(Z-A)按标题对项目排序。 |

### 筛选 {#filtering}

您可以使用`property`参数筛选结果，该参数用于对检索的资源中的给定JSON属性应用特定运算符。 支持的运算符包括：

| 运算符 | 描述 | 示例 |
| --- | --- | --- |
| `==` | 过滤器：属性是否等于提供的值。 | `property=title==test` |
| `!=` | 过滤器：属性是否不等于提供的值。 | `property=title!=test` |
| `<` | 过滤器该属性是否小于提供的值。 | `property=version<5` |
| `>` | 过滤器该属性是否大于提供的值。 | `property=version>5` |
| `<=` | 过滤器。 | `property=version<=5` |
| `>=` | 过滤器。 | `property=version>=5` |
| `~` | 过滤器。 | `property=title~test$` |
| (None) | 仅声明属性名称只返回存在属性的条目。 | `property=title` |

>[!TIP]
>
>可以使用`property`参数按其兼容类过滤混音。 例如，`property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile`只返回与[!DNL XDM Individual Profile]类兼容的混合。

## 兼容性模式

[!DNL Experience Data Model] (XDM)是一个公开记录的规范，它由Adobe驱动，旨在提高数字体验的互操作性、表现力和强大功能。Adobe在GitHub](https://github.com/adobe/xdm/)上的[开放源项目中维护源代码和正式的XDM定义。 这些定义以XDM标准表示法编写，使用JSON-LD（链接数据的JavaScript对象表示法）和JSON模式作为定义XDM模式的语法。

在公共存储库中查看正式的XDM定义时，您会发现标准XDM与您在Adobe Experience Platform中看到的不同。 您在[!DNL Experience Platform]中看到的内容称为兼容性模式，它在标准XDM和在[!DNL Platform]中使用它的方式之间提供了简单映射。

### 兼容模式的工作方式

兼容性模式允许XDM JSON-LD模型通过更改标准XDM中的值并保持语义相同，与现有数据基础结构配合使用。 它使用嵌套JSON结构，以类树格式显示模式。

您将注意到标准XDM和兼容性模式的主要区别是删除了字段名称的“xdm：”前缀。

以下是一个并排比较，它显示标准XDM和兼容模式中与生日相关的字段（删除了“description”属性）。 请注意，兼容性模式字段包括对“meta:xdmField”和“meta:xdmType”属性中XDM字段及其数据类型的引用。

<table>
  <th>标准XDM</th>
  <th>兼容性模式</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        {
          "xdm:pirthDate":{
              “标题”："出生日期"
              “类型”："string",
              “格式”：“日期”，
          },
          "xdm:phirthDayAndMonth":{
              “标题”："出生日期"
              “类型”："string",
              “模式”："[0-1][0-9]-[0-9][0-9]",
          },
          “xdm:prishYear”：{
              “标题”："出生年"
              “类型”："integer",
              “minimum”：1,
              “maximum”：32767
        }
  </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        {
          "birthDate":{
              “标题”："出生日期"
              “类型”："string",
              “格式”：“日期”，
              "meta:xdmField":"xdm:pirthDate",
              "meta:xdmType":"日期"
          },
          “byrthDayAndMonth”：{
              “标题”："出生日期"
              “类型”："string",
              “模式”："[0-1][0-9]-[0-9][0-9]",
              "meta:xdmField":"xdm:phirtyDayAndMonth",
              "meta:xdmType":"字符串"
          },
          “parthYear”：{
              “标题”："出生年"
              “类型”："integer",
              “minimum”：1,
              “maximum”：32767,
              "meta:xdmField":"xdm:prishYear",
              "meta:xdmType":"short"
        }
      </pre>
  </td>
  </tr>
</table>

### 为什么需要兼容模式？

Adobe Experience Platform设计为使用多个解决方案和服务，每个解决方案和服务都有各自的技术挑战和限制（例如，某些技术如何处理特殊字符）。 为了克服这些限制，开发了兼容模式。

大多数[!DNL Experience Platform]服务（包括[!DNL Catalog]、[!DNL Data Lake]和[!DNL Real-time Customer Profile]）使用[!DNL Compatibility Mode]代替标准XDM。 [!DNL Schema Registry] API也使用[!DNL Compatibility Mode]，此文档中的示例全部使用[!DNL Compatibility Mode]显示。

应该知道，标准XDM与在[!DNL Experience Platform]中操作它的方式之间发生映射，但这不应影响您对[!DNL Platform]服务的使用。

开放源项目可供您使用，但在通过[!DNL Schema Registry]与资源交互时，此文档中的API示例提供了您应该了解和遵循的最佳实践。

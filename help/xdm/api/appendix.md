---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;compatibility;Compatibility;compatibility mode;Compatibility mode;field type;field types;
solution: Experience Platform
title: 模式注册开发人员附录
description: 本文档提供与使用模式注册表API相关的补充信息。
topic: developer guide
translation-type: tm+mt
source-git-commit: 42d3bed14c5f926892467baeeea09ee7a140ebdc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 附录

本文档提供与使用API相关的补充 [!DNL Schema Registry] 信息。

## 兼容性模式

[!DNL Experience Data Model] (XDM)是一个公开的文档规范，它由Adobe驱动，旨在提高数字体验的互操作性、表现力和强大功能。 Adobe在GitHub上的开放源项目中维护 [源代码和正式的XDM定义](https://github.com/adobe/xdm/)。 这些定义以XDM标准表示法编写，使用JSON-LD（链接数据的JavaScript对象表示法）和JSON模式作为定义XDM模式的语法。

在公共存储库中查看正式的XDM定义时，您会发现标准XDM与您在Adobe Experience Platform看到的不同。 您在中看到的 [!DNL Experience Platform] 内容称为兼容性模式，它提供了标准XDM与内部使用方式之间的简单映射 [!DNL Platform]。

### 兼容性模式的工作原理

兼容性模式允许XDM JSON-LD模型通过更改标准XDM中的值并保持语义相同，与现有数据基础结构配合使用。 它使用嵌套JSON结构，以类树格式显示模式。

标准XDM和兼容性模式之间的主要区别是删除字段名称的“xdm:”前缀。

以下是标准XDM和兼容性模式中与生日相关的字段（删除了“描述”属性）的并排比较。 请注意，兼容性模式字段包括对“meta:xdmField”和“meta:xdmType”属性中XDM字段及其数据类型的引用。

<table>
  <th>标准XDM</th>
  <th>兼容性模式</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        { "xdm:birthDate":{ "title":“出生日期”、“类型”:"string", "format":"date", }, "xdm:birdhDayAndMonth":{ "title":“出生日期”、“类型”:"string", "pattern":"[0-1][0-9]-[0-9][0-9]", }, "xdm:pirthYear":{ "title":“出生年”、“类型”:"integer", "minimum":1, "maximum":32767 }
  </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        { "birthDate":{ "title":“出生日期”、“类型”:"string", "format":"date", "meta:xdmField":"xdm:birthDate", "meta:xdmType":"date" }, "birthDayAndMonth":{ "title":“出生日期”、“类型”:"string", "pattern":"[0-1][0-9]-[0-9][0-9]", "meta:xdmField":"xdm:birdyDayAndMonth", "meta:xdmType":"string" }, "birthYear":{ "title":“出生年”、“类型”:"integer", "minimum":1, "maximum":32767, "meta:xdmField":"xdm:birthYear", "meta:xdmType":"short" }
      </pre>
  </td>
  </tr>
</table>

### 为什么需要兼容模式？

Adobe Experience Platform设计为使用多种解决方案和服务，每种解决方案和服务都有各自的技术挑战和限制（例如，某些技术如何处理特殊特性）。 为了克服这些限制，开发了兼容模式。

大多 [!DNL Experience Platform] 数服 [!DNL Catalog]务，包括 [!DNL Data Lake]、和 [!DNL Real-time Customer Profile] 用于 [!DNL Compatibility Mode] 替代标准XDM。 该 [!DNL Schema Registry] API还使 [!DNL Compatibility Mode]用，此文档中的示例都使用 [!DNL Compatibility Mode]。

应该知道标准XDM与其操作方式之间存在映射，但 [!DNL Experience Platform]它不应影响您对服务的使 [!DNL Platform] 用。

开放源项目可供您使用，但在涉及通过与资源交互时，此文档中的 [!DNL Schema Registry]API示例提供您应了解和遵循的最佳实践。
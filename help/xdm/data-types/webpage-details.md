---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；网页详细信息；数据类型；数据类型；数据类型；网页
solution: Experience Platform
title: 网页详细信息数据类型
description: 了解网页详细信息Experience Data Model (XDM)数据类型。
exl-id: 31108e57-d416-485b-a6c3-4ebc4f5b1152
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 11%

---

# [!UICONTROL 网页详细信息]数据类型

[!UICONTROL 网页详细信息]是一个标准的体验数据模型(XDM)数据类型，它描述了有关刚刚加载和查看的网页的详细信息（由ExperienceEvent记录）。

数据类型适用于单页Web应用程序(SPA)的完整页面详细信息和初始页面加载。 对于在加载的页面上发生的不会触发新页面加载的交互，请参阅[Web交互](./web-interaction.md)数据类型。

![网页详细信息](../images/data-types/web-page-details.PNG){width="500"}

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL 度量值]](./measure.md) | 网页的查看次数。 |
| `URL` | 字符串 | 网页的规范或常用URL。 这可能是也可能不是用于访问页面的实际URL。 若要记录用于访问页面的URL，请使用`webLink`。 URI格式应遵循[RFC 3986](https://tools.ietf.org/html/rfc3986)标准。 |
| `isErrorPage` | 布尔值 | 此属性使用标志来指示页面是否为错误页面。 此标记用于对Web交互进行广泛分类。 该错误由应用程序定义，并可对应于提供HTTP错误代码的页面。 |
| `isHomePage` | 布尔值 | 此属性使用标志来指示页面是否为主页。 此标记用于对Web交互进行广泛分类。 主页的定义由应用程序决定。 |
| `name` | 字符串 | 网页的规范名称。此名称不一定是页面标题或直接与页面内容相关联，而用于整理站点页面以进行分类。 |
| `server` | 字符串 | 承载网页的规范或常用服务器。 这可能是也可能不是实际提供页面交互的主机或服务器。 |
| `siteSection` | 字符串 | 此网页所在的站点部分的规范名称。 这可用于对交互进行分类或归类。 |
| `viewName` | 字符串 | 页面中视图的名称。 此属性通常用于具有更改大部分页面布局的选项卡或控件的单页应用程序或页面。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.example.2.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webpagedetails.schema.json)

---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式；网页详细信息；数据类型；数据类型；网页
solution: Experience Platform
title: 网页详细信息数据类型
topic: overview
description: 此文档概述了网页详细信息体验数据模型(XDM)数据类型。
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 2%

---


# [!UICONTROL 网页详细] 信息数据类型

[!UICONTROL 网页详] 细信息是一种标准的体验数据模型(XDM)数据类型，它描述由ExperienceEvent记录的刚加载和查看的网页的详细信息。

数据类型适用于单页Web应用程序(SPA)的完整页面详细信息和初始页面加载。 有关在加载的页面上发生的不触发新页面加载的交互，请参阅[Web交互](./web-interactions.md)数据类型。

<img src="../images/data-types/web-page-details.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `pageViews` | [[!UICONTROL 度量]](./measure.md) | 网页上的视图数。 |
| `URL` | 字符串 | 网页的规范性或常规URL。 这可能是用于访问页面的实际URL，也可能不是。 要记录用于访问页面的URL，请使用`webLink`。 URI格式应遵循[RFC 3986](https://tools.ietf.org/html/rfc3986)标准。 |
| `isErrorPage` | 布尔值 | 此属性使用标记来指示该页面是否为错误页面。 此标志用于对Web交互进行广泛分类。 该错误由应用程序定义，并且可以与HTTP错误代码所提供的页面对应。 |
| `isHomePage` | 布尔值 | 此属性使用标志来指示页面是否为主页。 此标志用于对Web交互进行广泛分类。 主页的定义由应用程序确定。 |
| `name` | 字符串 | 网页的规范名称。 此名称不一定是页面标题或与页面内容直接关联，但用于组织站点的页面以进行分类。 |
| `server` | 字符串 | 承载网页的规范服务器或常规服务器。 这可能是实际为页面交互提供服务的主机或服务器，也可能不是。 |
| `siteSection` | 字符串 | 此网页所在站点部分的规范名称。 这可用于对交互进行分类或分类。 |
| `viewName` | 字符串 | 页面中视图的名称。 此属性通常用于单页应用程序或具有选项卡或控件的页面，这些选项卡或控件可更改大部分页面布局。 |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.example.2.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webpagedetails.schema.json)
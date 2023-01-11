---
keywords: Experience Platform；主页；热门主题；模式；模式；XDM；字段；模式；模式；Web交互；数据类型；数据类型；
solution: Experience Platform
title: Web交互数据类型
description: 本文档概述了Web交互体验数据模型(XDM)数据类型。
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 4%

---

# [!UICONTROL Web交互] 数据类型

[!UICONTROL Web交互] 是一种标准的体验数据模型(XDM)数据类型，用于描述有关初始页面加载完成后在网页上发生的交互的信息。 它用于记录富Web应用程序中不会触发新页面加载的交互，例如单页Web应用程序(SPA)。

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL 测量]](./measure.md) | 跟踪Web链接点击的测量。 |
| `URL` | 字符串 | 用于此Web交互的实际链接或URL。 |
| `name` | 字符串 | 用于此Web链接的规范名称。 它用于分类目的。 |
| `type` | 字符串 | 链接类型。 此属性必须等于以下枚举值之一： <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.schema.json)

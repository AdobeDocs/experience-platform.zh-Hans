---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式;web交互；数据类型；数据类型；
solution: Experience Platform
title: Web交互数据类型
topic: overview
description: 本文档概述了Web交互体验数据模型(XDM)数据类型。
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 2%

---


# [!UICONTROL Web交] 互数据类型

[!UICONTROL Web交] 互是一种标准的体验数据模型(XDM)数据类型，它描述有关在初始页面加载完成后在网页上发生的交互的信息。它用于在不触发新页面加载的富Web应用程序中记录交互，如单页Web应用程序(SPA)。

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL 度量]](./measure.md) | 跟踪Web链接单击的度量。 |
| `URL` | 字符串 | 用于此Web交互的实际链接或URL。 |
| `name` | 字符串 | 用于此Web链接的规范名称。 这用于分类目的。 |
| `type` | 字符串 | 链接类型。 此属性必须等于以下枚举值之一： <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.schema.json)
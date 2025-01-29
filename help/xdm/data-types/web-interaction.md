---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；Web交互；数据类型；数据类型；
solution: Experience Platform
title: Web交互数据类型
description: 了解Web交互Experience Data Model (XDM)数据类型。
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 10%

---

# [!UICONTROL Web交互]数据类型

[!UICONTROL Web交互]是标准的体验数据模型(XDM)数据类型，用于描述初始页面加载完成后在网页上发生的交互信息。 它用于记录富Web应用程序(例如单页Web应用程序(SPA))中不会触发新页面加载的交互。

![Web交互图像](../images/data-types/web-interaction.PNG){width=500}

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL 度量值]](./measure.md) | 跟踪Web链接点击的测量。 |
| `URL` | 字符串 | 用于此 Web 交互的实际链接或 URL。 |
| `name` | 字符串 | 此Web链接使用的规范名称。 这用于分类目的。 |
| `type` | 字符串 | 链接类型。 此属性必须等于以下枚举值之一： <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.schema.json)

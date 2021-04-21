---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；字段；模式;模式;web交互；datatype；数据类型；
solution: Experience Platform
title: Web交互数据类型
topic-legacy: overview
description: 本文档概述了Web交互体验数据模型(XDM)数据类型。
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 2%

---

# [!UICONTROL Web interaction] 数据类型

[!UICONTROL Web interaction] 是标准的体验数据模型(XDM)数据类型，用于描述在完成初始页面加载后在网页上发生的交互的信息。它用于在不触发新页面加载的富Web应用程序中记录交互，如单页Web应用程序(SPA)。

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Measure]](./measure.md) | 跟踪Web链接单击的度量。 |
| `URL` | 字符串 | 用于此Web交互的实际链接或URL。 |
| `name` | 字符串 | 用于此Web链接的规范名称。 这用于分类目的。 |
| `type` | 字符串 | 链接类型。 此属性必须等于以下枚举值之一： <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

有关数据类型的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinteraction.schema.json)

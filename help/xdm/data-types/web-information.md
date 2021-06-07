---
keywords: Experience Platform；主页；热门主题；模式；模式；XDM；字段；模式；模式；网页详细信息；数据类型；数据类型；网页
solution: Experience Platform
title: Web信息数据类型
topic-legacy: overview
description: 本文档概述了Web信息体验数据模型(XDM)数据类型。
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 3%

---

# [!UICONTROL Web信] 息数据类型

[!UICONTROL Web信] 息是标准的体验数据模型(XDM)数据类型，用于描述通过特定于万维网渠道（包括网页、反向链接和/或与页面交互相关的链接）的体验事件记录的信息。

![](../images/data-types/web-information.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Web交互]](./web-interaction.md) | 描述有关与交互对应的Web链接或URL的详细信息。 |
| `webPageDetails` | [[!UICONTROL 网页详细信息]](./webpage-details.md) | 描述发生Web交互的网页的详细信息。 |
| `webReferrer` | [!UICONTROL 对象] | 描述Web交互的反向链接，即访客在记录当前Web交互之前所从的URL。 包含以下子属性： <ul><li>`URL`:反向链接URL。</li><li>`type`:反向链接类型。</li></ul> |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinfo.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/web/webinfo.schema.json)

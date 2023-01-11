---
keywords: Experience Platform；主页；热门主题；模式；模式；XDM；字段；模式；模式；网页详细信息；数据类型；数据类型；网页
solution: Experience Platform
title: Web信息数据类型
description: 本文档概述了Web信息体验数据模型(XDM)数据类型。
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 3%

---

# [!UICONTROL Web信息] 数据类型

[!UICONTROL Web信息] 是一种标准的体验数据模型(XDM)数据类型，用于描述通过特定于万维网渠道的体验事件记录的信息，包括与页面交互相关的网页、反向链接和/或链接。

![](../images/data-types/web-information.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Web交互]](./web-interaction.md) | 描述有关与交互对应的Web链接或URL的详细信息。 |
| `webPageDetails` | [[!UICONTROL 网页详细信息]](./webpage-details.md) | 描述发生Web交互的网页的详细信息。 |
| `webReferrer` | [!UICONTROL 对象] | 描述Web交互的反向链接，即访客在记录当前Web交互之前所从的URL。 包含以下子属性： <ul><li>`URL`:反向链接URL。</li><li>`type`:反向链接类型。</li></ul> |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)

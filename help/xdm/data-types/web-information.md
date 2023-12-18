---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；字段；架构；架构；网页详细信息；数据类型；数据类型；数据类型；网页
solution: Experience Platform
title: Web信息数据类型
description: 了解Web信息Experience Data Model (XDM)数据类型。
exl-id: bfb00835-5908-4baf-af2a-6d845710e340
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 2%

---

# [!UICONTROL Web信息] 数据类型

[!UICONTROL Web信息] 是一个标准的体验数据模型(XDM)数据类型，它描述通过特定于万维网渠道的体验事件记录的信息，包括网页、反向链接和/或与页面上的交互相关的链接。

![](../images/data-types/web-information.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `webInteraction` | [[!UICONTROL Web交互]](./web-interaction.md) | 描述与交互相对应的Web链接或URL的详细信息。 |
| `webPageDetails` | [[!UICONTROL 网页详细信息]](./webpage-details.md) | 描述有关发生Web交互的网页的详细信息。 |
| `webReferrer` | [!UICONTROL 对象] | 描述Web交互的反向链接，即在记录当前Web交互之前，访客所使用的URL。 包含以下子属性： <ul><li>`URL`：反向链接URL。</li><li>`type`：反向链接类型。</li></ul> |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/datatypes/webinfo.schema.json)

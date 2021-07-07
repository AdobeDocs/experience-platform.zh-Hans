---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM;ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；
solution: Experience Platform
title: Web Details Schema Field Group
topic-legacy: overview
description: 本文档概述了Web详细信息架构字段组。
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 3%

---


# [!UICONTROL Web Details] schema field group

>[!NOTE]
>
>The names of several schema field groups have changed. See the document on [field group name updates](../name-updates.md) for more information.

[!UICONTROL Web详] 细信息是类的标准架构字段 [[!DNL XDM ExperienceEvent] 组](../../classes/experienceevent.md)，用于描述有关Web详细信息事件（如交互、页面详细信息和反向链接）的信息。

![](../../images/field-groups/web-details.png)

| 属性 | Data type | 描述 |
| --- | --- | --- |
| `web` | [Web信息](../../data-types/web-information.md) | Describes link clicks, web page details, referrer information, and browser details. |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-web.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-web.schema.json)

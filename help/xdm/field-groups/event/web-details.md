---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM;ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；
solution: Experience Platform
title: Web详细信息架构字段组
description: 本文档概述了Web详细信息架构字段组。
exl-id: eb42606b-ade4-4d72-b601-c560009c98e8
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 3%

---

# [!UICONTROL Web详细信息] 架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 请参阅 [字段组名称更新](../name-updates.md) 以了解更多信息。

[!UICONTROL Web详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md)，用于描述有关Web详细信息事件（如交互、页面详细信息和反向链接）的信息。

![](../../images/field-groups/web-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `web` | [Web信息](../../data-types/web-information.md) | 描述链接点击量、网页详细信息、反向链接信息和浏览器详细信息。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-web.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-web.schema.json)

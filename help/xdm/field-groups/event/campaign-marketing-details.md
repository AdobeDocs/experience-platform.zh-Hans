---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM;ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；
solution: Experience Platform
title: Campaign Marketing Details Schema Field Group
topic-legacy: overview
description: 本文档概述了“营销活动详细信息”架构字段组。
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 3%

---


# [!UICONTROL Campaign Marketing Details] schema field group

>[!NOTE]
>
>多个架构字段组的名称已更改。 有关详细信息，请参阅[字段组名称更新](../name-updates.md)上的文档。

[!UICONTROL 促销活] 动营销详细信息类的标准 [[!DNL XDM ExperienceEvent] 架构字段组](../../classes/experienceevent.md)，用于描述促销活动信息，如促销活动组、名称和跟踪代码。

![](../../images/field-groups/campaign-marketing-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `marketing` | [营销](../../data-types/marketing.md) | An object that describes marketing campaign information such as campaign group, name, and tracking code. |

{style=&quot;table-layout:auto&quot;}

For more details on the field group, refer to the public XDM repository:

* [Populated example](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.schema.json)

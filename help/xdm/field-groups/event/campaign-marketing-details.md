---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；
solution: Experience Platform
title: 营销活动详细信息架构字段组
description: 了解Campaign营销详细信息架构字段组。
exl-id: be08b38b-68a0-4a74-9b8f-0344a0637395
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 3%

---

# [!UICONTROL 营销活动营销详细信息]架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 有关详细信息，请参阅有关[字段组名称更新](../name-updates.md)的文档。

[!UICONTROL 促销活动营销详细信息]是[[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md)的标准架构字段组，用于描述促销活动信息，如促销活动组、名称和跟踪代码。

![](../../images/field-groups/campaign-marketing-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `marketing` | [营销](../../data-types/marketing.md) | 描述营销活动信息（如营销活动组、名称和跟踪代码）的对象。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-marketing.schema.json)

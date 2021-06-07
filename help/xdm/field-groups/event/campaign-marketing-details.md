---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM;ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；
solution: Experience Platform
title: 营销活动营销详细信息架构字段组
topic-legacy: overview
description: 本文档概述了“营销活动详细信息”架构字段组。
source-git-commit: cb4afb0979bd65a9a82a6018323fa7beacdbf605
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 3%

---


# [!UICONTROL 营销活动营销] 详细信息架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 有关详细信息，请参阅[字段组名称更新](../name-updates.md)上的文档。

[!UICONTROL 促销活] 动营销详细信息类的标准 [[!DNL XDM ExperienceEvent] 架构字段组](../../classes/experienceevent.md)，用于描述促销活动信息，如促销活动组、名称和跟踪代码。

![](../../images/field-groups/campaign-marketing-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `marketing` | [营销](../../data-types/marketing.md) | 描述营销活动信息（如促销活动组、名称和跟踪代码）的对象。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-marketing.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-marketing.schema.json)

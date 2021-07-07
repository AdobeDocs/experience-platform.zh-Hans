---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM;ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；
solution: Experience Platform
title: 渠道详细信息架构字段组
topic-legacy: overview
description: 本文档概述了渠道详细信息架构字段组。
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 3%

---


# [!UICONTROL Channel Details] schema field group

>[!NOTE]
>
>多个架构字段组的名称已更改。 有关详细信息，请参阅[字段组名称更新](../name-updates.md)上的文档。

[!UICONTROL 渠道] 详细信息类的标准架构字段 [[!DNL XDM ExperienceEvent] 组](../../classes/experienceevent.md)，用于描述渠道信息，如ID、渠道类型、媒体类型和位置类型。

![](../../images/field-groups/channel-details.png)

| 属性 | Data type | 描述 |
| --- | --- | --- |
| `channel` | [体验渠道](../../data-types/experience-channel.md) | 描述产品退货、保修注册和购物车/订购流程的对象。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [Full schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)

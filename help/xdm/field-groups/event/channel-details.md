---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM;ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；
solution: Experience Platform
title: 渠道详细信息架构字段组
description: 本文档概述了渠道详细信息架构字段组。
exl-id: b8ec2f57-6882-466e-9b22-61fb2178fb1e
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 3%

---

# [!UICONTROL 渠道详细信息] 架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 请参阅 [字段组名称更新](../name-updates.md) 以了解更多信息。

[!UICONTROL 渠道详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md)，用于描述渠道信息，如ID、渠道类型、媒体类型和位置类型。

![](../../images/field-groups/channel-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `channel` | [体验渠道](../../data-types/experience-channel.md) | 描述产品退货、保修注册和购物车/订购流程的对象。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)

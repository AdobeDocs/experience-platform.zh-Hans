---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM;ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；最终用户ID；最终用户；ID;
solution: Experience Platform
title: 最终用户ID详细信息架构字段组
description: 本文档概述了最终用户ID详细信息架构字段组。
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 5%

---


# [!UICONTROL 最终用户ID详细信息] 架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 请参阅 [字段组名称更新](../name-updates.md) 以了解更多信息。

[!UICONTROL 最终用户ID详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md)，用于在多个Adobe应用程序中描述个人的身份信息。 字段组提供根级别 `endUserIDs` 对象，其本身包含只读 `_experience` 字段，其值会在摄取数据时自动更新。

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `aacustomid` | [标识](../../data-types/identity.md) | 自定义最终用户ID，用于Adobe Analytics Cloud。 |
| `aaid` | [标识](../../data-types/identity.md) | Adobe Analytics Cloud的最终用户ID。 |
| `acid` | [标识](../../data-types/identity.md) | Adobe Campaign的最终用户ID。 |
| `adcloud` | [标识](../../data-types/identity.md) | Adobe Advertising Cloud的最终用户ID。 |
| `emailid` | [标识](../../data-types/identity.md) | 电子邮件地址ID。 |
| `mcid` | [标识](../../data-types/identity.md) | Adobe Marketing Cloud ID(MCID)。 MCID现在称为Experience CloudID(ECID)。 |
| `phonenumberid` | [标识](../../data-types/identity.md) | 电话号码ID。 |
| `tntid` | [标识](../../data-types/identity.md) | Adobe Target的最终用户ID。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)

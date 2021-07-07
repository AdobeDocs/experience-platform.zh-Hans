---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM;ExperienceEvent；字段；架构；架构；架构设计；字段组；字段组；最终用户ID；最终用户；ID;
solution: Experience Platform
title: 最终用户ID详细信息架构字段组
topic-legacy: overview
description: 本文档概述了最终用户ID详细信息架构字段组。
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 2%

---


# [!UICONTROL 最终用户ID详细] 信息架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 有关详细信息，请参阅[字段组名称更新](../name-updates.md)上的文档。

[!UICONTROL 最终用户ID] 详细信息类的标准架构字段 [[!DNL XDM ExperienceEvent] 组](../../classes/experienceevent.md)，用于在多个Adobe应用程序中描述个人的身份信息。字段组提供一个根级别`endUserIDs`对象，该对象本身包含一个只读`_experience`字段，其值会在摄取数据时自动更新。

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `aacustomid` | [身份](../../data-types/identity.md) | 自定义最终用户ID，用于Adobe Analytics Cloud。 |
| `aaid` | [身份](../../data-types/identity.md) | Adobe Analytics Cloud的最终用户ID。 |
| `acid` | [身份](../../data-types/identity.md) | Adobe Campaign的最终用户ID。 |
| `adcloud` | [身份](../../data-types/identity.md) | Adobe Advertising Cloud的最终用户ID。 |
| `emailid` | [身份](../../data-types/identity.md) | 电子邮件地址ID。 |
| `mcid` | [身份](../../data-types/identity.md) | Adobe Marketing Cloud ID。 |
| `phonenumberid` | [身份](../../data-types/identity.md) | 电话号码ID。 |
| `tntid` | [身份](../../data-types/identity.md) | Adobe Target的最终用户ID。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)

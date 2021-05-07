---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM;ExperienceEvent；字段；模式;模式;模式设计；字段组；字段组；端用户id；最终用户；id;
solution: Experience Platform
title: 最终用户ID详细信息模式字段组
topic-legacy: overview
description: 此文档概述了“最终用户ID详细信息”模式字段组。
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# [!UICONTROL End User ID Details] 模式字段组

>[!NOTE]
>
>多个模式字段组的名称已更改。 有关详细信息，请参阅[字段组名称更新](../name-updates.md)上的文档。

[!UICONTROL End User ID Details] 是类的标准模式字段 [[!DNL XDM ExperienceEvent] 组](../../classes/individual-profile.md)，用于跨多个Adobe应用程序描述个人的身份信息。字段组提供一个根级别`endUserIDs`对象，该对象本身包含一个只读`_experience`字段，该字段的值在摄取数据时自动更新。

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `aacustomid` | [身份](../../data-types/identity.md) | Adobe Analytics Cloud的自定义最终用户ID。 |
| `aaid` | [身份](../../data-types/identity.md) | Adobe Analytics Cloud的最终用户ID。 |
| `acid` | [身份](../../data-types/identity.md) | 最终用户ID，用于Adobe Campaign。 |
| `adcloud` | [身份](../../data-types/identity.md) | Adobe Advertising Cloud的最终用户ID。 |
| `emailid` | [身份](../../data-types/identity.md) | 电子邮件地址ID。 |
| `mcid` | [身份](../../data-types/identity.md) | Adobe Marketing Cloud ID。 |
| `phonenumberid` | [身份](../../data-types/identity.md) | 电话号码ID。 |
| `tntid` | [身份](../../data-types/identity.md) | Adobe Target的最终用户ID。 |

有关字段组的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)

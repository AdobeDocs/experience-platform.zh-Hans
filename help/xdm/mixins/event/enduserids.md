---
keywords: Experience Platform；主题；热门主题；模式;模式;XDM；体验事件；字段；模式;模式;模式设计；混音；混合；最终用户；最终用户；id;
solution: Experience Platform
title: 最终用户ID详细信息混合
topic: overview
description: 此文档提供最终用户ID详细信息混合的概述。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---


# [!UICONTROL 最终用户ID ] Detailsmixin

>[!NOTE]
>
>几个混音的名称已经更改。 有关详细信息，请参阅[mixin name updates](../name-updates.md)上的文档。

[!UICONTROL 最终用户ID] 详细信息是类的标 [[!DNL XDM ExperienceEvent] 准混合](../../classes/individual-profile.md)，用于跨多个Adobe应用程序描述个人的身份信息。mixin提供一个根级别`endUserIDs`对象，该对象本身包含一个只读`_experience`字段，该字段的值在摄取数据时自动更新。

<img src="../../images/mixins/enduserids.png" width="700" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `aacustomid` | [身份](../../data-types/identity.md) | Adobe Analytics Cloud的自定义最终用户ID。 |
| `aaid` | [身份](../../data-types/identity.md) | Adobe Analytics Cloud的最终用户ID。 |
| `acid` | [身份](../../data-types/identity.md) | 最终用户ID用于Adobe Campaign。 |
| `adcloud` | [身份](../../data-types/identity.md) | Adobe Advertising Cloud的最终用户ID。 |
| `emailid` | [身份](../../data-types/identity.md) | 电子邮件地址ID。 |
| `mcid` | [身份](../../data-types/identity.md) | Adobe Marketing Cloud。 |
| `phonenumberid` | [身份](../../data-types/identity.md) | 电话号码ID。 |
| `tntid` | [身份](../../data-types/identity.md) | Adobe Target的最终用户ID。 |

有关混音的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)

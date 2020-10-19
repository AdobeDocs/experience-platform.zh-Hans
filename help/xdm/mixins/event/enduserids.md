---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;mixin;mixin;enduserids;end-user;end user;ids;
solution: Experience Platform
title: ExperienceEvent EndUserID混音
topic: overview
description: 此文档概述了ExperienceEvent EndUserID混合。
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 1%

---


# [!UICONTROL ExperienceEvent EndUserID] mixin

[!UICONTROL ExperienceEvent EndUser] ID是类的标准混音 [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md)，用于跨多个Adobe应用程序描述个人的身份信息。 mixin提供根级对象，该 `endUserIDs` 对象本身包含只读字段，该 `_experience` 字段的值在摄取数据时自动更新。

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

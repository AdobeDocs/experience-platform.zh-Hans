---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixins;work details;profile work;
solution: Experience Platform
title: 混合工作联系人详细信息
topic: overview
description: 此文档概述了“工作联系人详细信息”混合。
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 3%

---


# [!UICONTROL 混合工作联系人] “详细信息”

>[!NOTE]
>
>几个混音的名称已经更改。 有关详细信息，请 [参阅混合名称](../name-updates.md) 更新文档。

[!UICONTROL 工作联系人详] 细信息是课程的标准混 [[!DNL XDM Individual Profile] 音符](../../classes/individual-profile.md)。 混音提供了多个字段，用于捕获有关个人的职业信息，如工作地址、工作电子邮件、工作电话号码以及该人所属的组织。

<img src="../../images/mixins/profile-work-details.png" width="550" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `workAddress` | [邮政地址](../../data-types/postal-address.md) | 描述人员的工作地址。 |
| `workEmail` | [电子邮件地址](../../data-types/email-address.md) | 描述人员的工作电子邮件地址。 |
| `workPhone` | [电话号码](../../data-types/phone-number.md) | 描述人员的工作电话号码。 |
| `organizations` | 字符串（数组） | 自由形式字符串的数组，它们表示此人所属的组织。 |

有关混音的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)
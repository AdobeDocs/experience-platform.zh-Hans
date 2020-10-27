---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;personal details;Schema design;mixin;Mixin;
solution: Experience Platform
title: 个人联系人详细信息混合
topic: overview
description: 此文档概述了“个人联系人详细信息”混合。
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 7%

---


# [!UICONTROL 混合个人联系人详] 情

>[!NOTE]
>
>几个混音的名称已经更改。 有关详细信息，请 [参阅混合名称](../name-updates.md) 更新文档。

[!UICONTROL “个人联系人] 详细信息”是课程的标准 [[!DNL XDM Individual Profile] 混合](../../classes/individual-profile.md) ，用于描述个人的联系信息。

<img src="../../images/mixins/profile-personal-details.png" width="700" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `faxPhone` | [电话号码](../../data-types/phone-number.md) | 描述该人的传真号码。 |
| `homeAddress` | [邮政地址](../../data-types/postal-address.md) | 描述人员的住宅地址。 |
| `homePhone` | [电话号码](../../data-types/phone-number.md) | 描述该人的家庭电话号码。 |
| `mobilePhone` | [电话号码](../../data-types/phone-number.md) | 描述该人员的移动电话号码。 |
| `personalEmail` | [电子邮件地址](../../data-types/email-address.md) | 描述人员的电子邮件地址。 |

有关混音的详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)

---
keywords: Experience Platform；主题；热门主题；模式;模式;XDM；个人用户档案；字段；模式;模式；个人细节；模式设计；混音；混音；
solution: Experience Platform
title: 混合个人联系人详细信息
topic: overview
description: 此文档概述了“个人联系人详细信息”混合。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 6%

---


# [!UICONTROL 个人联系人详] 细信息

>[!NOTE]
>
>几个混音的名称已经更改。 有关详细信息，请参阅[mixin name updates](../name-updates.md)上的文档。

[!UICONTROL 个人联] 系信息详细说明课程的 [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) 标准混合信息，其中描述个人的联系信息。

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

---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；个人用户档案；字段；模式;模式；个人细节；模式设计；混音；混音；
solution: Experience Platform
title: 个人联系人详细信息混合
topic-legacy: overview
description: 此文档概述了“个人联系人详细信息”混合。
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 6%

---

# [!UICONTROL Personal Contact Details] mixin

>[!NOTE]
>
>几个混音的名称已经更改。 有关详细信息，请参阅[mixin name updates](../name-updates.md)上的文档。

[!UICONTROL Personal Contact Details] 是类的标准混音， [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) 它描述个人的联系信息。

<img src="../../images/mixins/profile-personal-details.png" width="700" /><br />

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `faxPhone` | [电话号码](../../data-types/phone-number.md) | 描述此人的传真号码。 |
| `homeAddress` | [邮政地址](../../data-types/postal-address.md) | 描述人员的住宅地址。 |
| `homePhone` | [电话号码](../../data-types/phone-number.md) | 描述此人的家庭电话号码。 |
| `mobilePhone` | [电话号码](../../data-types/phone-number.md) | 描述此人的移动电话号码。 |
| `personalEmail` | [电子邮件地址](../../data-types/email-address.md) | 描述人员的电子邮件地址。 |

有关混音的更多详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)

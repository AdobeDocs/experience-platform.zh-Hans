---
keywords: Experience Platform；主页；热门主题；模式;模式;XDM；个人用户档案；字段；模式;模式;模式设计；混音；混音；工作细节；用户档案工作；
solution: Experience Platform
title: 工作联系人详细信息模式字段组
topic-legacy: overview
description: 此文档概述了“工作联系人详细信息”模式字段组。
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
translation-type: tm+mt
source-git-commit: 4755f9b7666efd8354a5f15aeed40a7da4a06efe
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 3%

---


# [!UICONTROL Work Contact Details] 模式字段组

>[!NOTE]
>
>多个模式字段组的名称已更改。 有关详细信息，请参阅[字段组名称更新](../name-updates.md)上的文档。

[!UICONTROL Work Contact Details] 是类的标准模式字 [[!DNL XDM Individual Profile] 段组](../../classes/individual-profile.md)。该字段组提供了多个字段，用于捕获有关个人的职业信息，例如工作地址、工作电子邮件、工作电话号码以及该人所属的组织。

![](../../images/field-groups/work-contact-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `workAddress` | [邮政地址](../../data-types/postal-address.md) | 描述人员的工作地址。 |
| `workEmail` | [电子邮件地址](../../data-types/email-address.md) | 描述人员的工作电子邮件地址。 |
| `workPhone` | [电话号码](../../data-types/phone-number.md) | 描述人员的工作电话号码。 |
| `organizations` | 字符串（数组） | 自由格式字符串的数组，表示此人是其成员的组织。 |

有关字段组的详细信息，请参阅公共XDM存储库：

* [已填充示例](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)

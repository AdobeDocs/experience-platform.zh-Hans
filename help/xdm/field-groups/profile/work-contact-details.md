---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；个人配置文件；字段；架构；架构；架构设计；mixin；mixin；工作详细信息；配置文件工作；
solution: Experience Platform
title: 工作联系人详细信息架构字段组
description: 本文档概述了“工作联系人详细信息”架构字段组。
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 3%

---


# [!UICONTROL 工作联系人详细信息] 架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 查看文档 [字段组名称更新](../name-updates.md) 了解更多信息。

[!UICONTROL 工作联系人详细信息] 是的标准架构字段组 [[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md). 字段组提供了多个字段，用于捕获有关个人的职业信息，例如工作地址、工作电子邮件、工作电话号码和人员所属的组织。

![](../../images/field-groups/work-contact-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `workAddress` | [邮政地址](../../data-types/postal-address.md) | 描述人员的工作地址。 |
| `workEmail` | [电子邮件地址](../../data-types/email-address.md) | 描述人员的工作电子邮件地址。 |
| `workPhone` | [电话号码](../../data-types/phone-number.md) | 描述人员的工作电话号码。 |
| `organizations` | 字符串（数组） | 自由格式字符串的数组，表示人员所属的组织。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.schema.json)

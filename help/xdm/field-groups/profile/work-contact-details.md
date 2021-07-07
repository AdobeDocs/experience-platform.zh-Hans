---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；单个配置文件；字段；架构；架构；架构设计；混合；混合；工作详细信息；配置文件工作；
solution: Experience Platform
title: Work Contact Details Schema Field Group
topic-legacy: overview
description: This document provides an overview of the Work Contact Details schema field group.
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 4%

---


# [!UICONTROL Work Contact Details] schema field group

>[!NOTE]
>
>The names of several schema field groups have changed. 有关详细信息，请参阅[字段组名称更新](../name-updates.md)上的文档。

[!UICONTROL 工作联系] 人详细信息类的标准架构字 [[!DNL XDM Individual Profile] 段组](../../classes/individual-profile.md)。The field group provides several fields that capture occupational information regarding an individual person, such as work address, work email, work phone number, and organizations to which the person belongs.

![](../../images/field-groups/work-contact-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `workAddress` | [Postal address](../../data-types/postal-address.md) | 描述人员的工作地址。 |
| `workEmail` | [电子邮件地址](../../data-types/email-address.md) | 描述人员的工作电子邮件地址。 |
| `workPhone` | [电话号码](../../data-types/phone-number.md) | Describes the person&#39;s work phone number. |
| `organizations` | String (Array) | 自由格式字符串的数组，表示人员所属的组织。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.schema.json)

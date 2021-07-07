---
keywords: Experience Platform；主页；热门主题；架构；架构；XDM；个人配置文件；字段；架构；个人详细信息；架构设计；字段组；字段组；
solution: Experience Platform
title: 个人联系人详细信息架构字段组
topic-legacy: overview
description: 本文档概述了个人联系人详细信息架构字段组。
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 7%

---


# [!UICONTROL 个人联系人] 详细信息架构字段组

>[!NOTE]
>
>多个架构字段组的名称已更改。 有关详细信息，请参阅[字段组名称更新](../name-updates.md)上的文档。

[!UICONTROL 个人联] 系人详细信息此类的标准架构字 [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) 段组，描述个人的联系信息。

![](../../images/field-groups/personal-contact-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `faxPhone` | [电话号码](../../data-types/phone-number.md) | 描述人员的传真号码。 |
| `homeAddress` | [邮政地址](../../data-types/postal-address.md) | 描述人员的住宅地址。 |
| `homePhone` | [电话号码](../../data-types/phone-number.md) | 描述人员的家庭电话号码。 |
| `mobilePhone` | [电话号码](../../data-types/phone-number.md) | 描述人员的手机号码。 |
| `personalEmail` | [电子邮件地址](../../data-types/email-address.md) | 描述人员的电子邮件地址。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

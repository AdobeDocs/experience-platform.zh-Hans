---
title: XDM业务人员组件架构字段组
description: 本文档概述了XDM业务人员组件架构字段组。
source-git-commit: 319d508925d22e76a3d75ae473f6ea000b5c655b
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 3%

---


# [!UICONTROL XDM业务人员组] 件架构字段组

>[!NOTE]
>
>此字段组仅适用于有权访问B2B版实时客户数据平台(Real-time CDP)的组织。

[!UICONTROL XDM业务人员] 组件是类的标准架构字段组，可 [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) 以捕获人员的多个源记录以及人员分段所需的其他属性。

在B2B版本的实时CDP中，通过[Real-time Customer Profile](../../../profile/home.md)为人员创建用户档案时，用于创建该用户档案的信息可能来自许多源记录。 例如，如果一个人为两个不同的公司工作，则许多CRM系统会创建该人的特意副本，以便一个副本链接到公司A，而另一个副本链接到公司B。将该数据导入Adobe Experience Platform时，此字段组用于将这些不同的源记录合并到单个表示中。

字段组提供根级别`personComponents`字段，该字段是对象数组。 数组中的每个对象表示不同的源记录。

![](../../images/field-groups/business-person-components.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 与人员关联的帐户的复合标识符。 |
| `sourceConvertedContactKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 如果此潜在客户已转换，则相关联系人的复合标识符。 |
| `sourceExternalKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 源系统的人员数据源的复合标识符。 |
| `sourcePersonKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 人员的组合标识符。 |
| `workEmail` | [[!UICONTROL 电子邮件地址]](../../data-types/b2b-source.md) | 人员的工作电子邮件ID。 |
| `personGroupID` | 字符串 | 人员的组标识符。 |
| `personScore` | 字符串 | 由CRM系统为人员生成的分数。 |
| `personSource` | 字符串 | 源系统的基于字符串的唯一标识符，即人员数据源自的。 |
| `personStatus` | 字符串 | 人员的当前营销或销售状态。 |
| `personType` | 字符串 | B2B上下文中的人员类型。 |
| `sourceAccountID` | 字符串 | 源系统中与人员关联的帐户基于字符串的唯一标识符。 系统会将此字段用作外键，以查找此人员工作的不同公司。 |
| `sourceConvertedContactID` | 字符串 | 如果转换了此潜在客户，则相关联系人的基于字符串的唯一标识符。 |
| `sourceExternalID` | 字符串 | 人员数据源自的源系统基于字符串的唯一标识符。 |
| `sourcePersonID` | 字符串 | 人员的基于字符串的唯一标识符。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)

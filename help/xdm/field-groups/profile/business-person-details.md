---
title: XDM业务人员详细信息架构字段组
description: 本文档概述了XDM业务人员详细信息架构字段组。
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: 57370e4ed0807bcebf30c73af629671b5390d90d
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 6%

---

# [!UICONTROL XDM业务人员详] 细信息架构字段组（测试版）

>[!IMPORTANT]
>
>此字段组作为Real-time Customer Data Platform B2B Edition的一部分提供，该B2B Edition目前处于测试阶段。 文档和功能可能会发生更改。

[!UICONTROL XDM业务人员] 详细信息是类的标准架构字 [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) 段组，用于捕获个人在企业对企业(B2B)企业环境中的信息。

![](../../images/field-groups/business-person-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `b2b` | 对象 | 用于捕获有关人员的B2B特定详细信息的对象。 |
| `b2b.accountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 与人员相关的业务帐户的组合标识符。 |
| `b2b.convertedContactKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 如果转换了潜在客户，则关联联系人的组合标识符。 |
| `b2b.personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 人员或用户档案片段的复合标识符。 |
| `b2b.accountID` | 字符串 | 此人员关联的业务帐户的唯一ID。 |
| `b2b.blockedCause` | 字符串 | 如果人员被阻止，则此资产会提供原因。 |
| `b2b.convertedContactID` | 字符串 | 成功转换潜在客户时的联系人ID。 |
| `b2b.convertedDate` | DateTime | 成功转化潜在客户时的转化日期。 |
| `b2b.isBlocked` | 布尔型 | 指示是否阻止该人员。 |
| `b2b.isConverted` | 布尔型 | 指示是否转换了潜在客户。 |
| `b2b.isMarketingSuspended` | 布尔型 | 指示营销是否为人员暂停。 |
| `b2b.marketingSuspendedCause` | 字符串 | 如果人员的营销已暂停，则此资产会提供原因。 |
| `b2b.personGroupID` | 字符串 | 人员的组标识符。 |
| `b2b.personScore` | 双精度 | 由CRM系统为人员生成的分数。 |
| `b2b.personSource` | 字符串 | 收到人员信息的来源。 |
| `b2b.personStatus` | 字符串 | 人员的当前营销或销售状态。 |
| `b2b.personType` | 字符串 | B2B人员的类型。 |
| `extSourceSystemAudit` | [外部源系统审核属性](../../data-types/external-source-system-audit-attributes.md) | 如果业务人员关系来自外部源系统，则此对象会捕获该系统的审核属性。 |
| `extendedWorkDetails` | 对象 | 捕获有关人员的其他与工作相关的详细信息。 |
| `extendedWorkDetails.assistantDetails` | 对象 | 捕获与人员助理相关的以下属性： <ul><li>`name`:([人员姓名](../../data-types/person-name.md))助理的全名。</li><li>`phone`:([电话号码](../../data-types/phone-number.md))助理的电话号码。</li></ul> |
| `extendedWorkDetails.departments` | 字符串数组 | 人员工作所在的部门名称列表。 |
| `extendedWorkDetails.jobTitle` | 字符串 | 人的职位。 |
| `extendedWorkDetails.photoUrl` | 字符串 | 指向人员照片的URL。 |
| `extendedWorkDetails.reportsToID` | 字符串 | 人员报表管理员的标识符。 |
| `faxPhone` | [电话号码](../../data-types/phone-number.md) | 此人的传真电话号码。 |
| `homeAddress` | [邮政地址](../../data-types/postal-address.md) | 此人的家庭地址。 |
| `homePhone` | [电话号码](../../data-types/phone-number.md) | 此人的家庭电话号码。 |
| `mobilePhone` | [电话号码](../../data-types/phone-number.md) | 人员的手机号码。 |
| `otherAddress` | [邮政地址](../../data-types/postal-address.md) | 人员的备用地址。 |
| `otherPhone` | [电话号码](../../data-types/phone-number.md) | 人员的备用电话号码。 |
| `person` | [人员](../../data-types/person.md) | 个人行为者、联系人或所有者。 |
| `personalEmail` | [电子邮件地址](../../data-types/email-address.md) | 人员的个人电子邮件地址。 |
| `workAddress` | [邮政地址](../../data-types/postal-address.md) | 人员的工作地址。 |
| `workEmail` | [电子邮件地址](../../data-types/email-address.md) | 人员的工作电子邮件地址。 |
| `workPhone` | [电话号码](../../data-types/phone-number.md) | 此人的工作电话号码。 |
| `identityMap` | 地图 | 一个映射字段，其中包含人员的一组命名进度标识。 在摄取身份数据时，系统会自动更新此字段。 为了正确使用[实时客户资料](../../../profile/home.md)的此字段，请不要尝试在数据操作中手动更新字段的内容。<br /><br />有关架构组合基础知识的用例的更 [多信息，请](../../schema/composition.md#identityMap) 参阅标识映射一节。 |
| `organizations` | 字符串数组 | 人员工作所在的组织名称列表。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)

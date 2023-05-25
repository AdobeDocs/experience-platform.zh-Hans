---
title: XDM业务人员详细信息架构字段组
description: 本文档概述了XDM业务人员详细信息架构字段组。
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 6%

---

# [!UICONTROL XDM业务人员详细信息] 架构字段组

[!UICONTROL XDM业务人员详细信息] 是的标准架构字段组 [[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md) 捕获企业对企业(B2B)背景下个人的信息。

![](../../images/field-groups/business-person-details.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `b2b` | 对象 | 捕获有关人员的B2B特定详细信息的对象。 |
| `b2b.accountKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 与人员相关的业务帐户的复合标识符。 |
| `b2b.convertedContactKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 如果商机已转化，则为相关联系人的复合标识符。 |
| `b2b.personKey` | [[!UICONTROL B2B源]](../../data-types/b2b-source.md) | 人员或个人资料片段的复合标识符。 |
| `b2b.accountID` | 字符串 | 此人员关联的业务帐户的唯一ID。 |
| `b2b.blockedCause` | 字符串 | 如果人员被阻止，则此属性提供原因。 |
| `b2b.convertedContactID` | 字符串 | 如果商机成功转化，则为联系人ID。 |
| `b2b.convertedDate` | 日期时间 | 成功转化商机的日期。 |
| `b2b.isBlocked` | 布尔值 | 指示人员是否被阻止。 |
| `b2b.isConverted` | 布尔值 | 指示商机是否已转化。 |
| `b2b.isMarketingSuspended` | 布尔值 | 指示人员营销是否暂停。 |
| `b2b.marketingSuspendedCause` | 字符串 | 如果对人员暂停营销，则此属性提供原因。 |
| `b2b.personGroupID` | 字符串 | 人员的组标识符。 |
| `b2b.personScore` | 双精度 | CRM系统为人员生成的分数。 |
| `b2b.personSource` | 字符串 | 个人信息的来源。 |
| `b2b.personStatus` | 字符串 | 人员的当前营销或销售状态。 |
| `b2b.personType` | 字符串 | B2B人员的类型。 |
| `extSourceSystemAudit` | [外部源系统审计属性](../../data-types/external-source-system-audit-attributes.md) | 如果业务人员关系来自外部源系统，则此对象捕获该系统的审核属性。 |
| `extendedWorkDetails` | 对象 | 捕获有关人员的其他工作相关详细信息。 |
| `extendedWorkDetails.assistantDetails` | 对象 | 捕获与人员助理相关的以下属性： <ul><li>`name`：([人员姓名](../../data-types/person-name.md))该助理的全名。</li><li>`phone`：([电话号码](../../data-types/phone-number.md))助理的电话号码。</li></ul> |
| `extendedWorkDetails.departments` | 字符串数组 | 人员工作的部门名称列表。 |
| `extendedWorkDetails.jobTitle` | 字符串 | 人员的职务。 |
| `extendedWorkDetails.photoUrl` | 字符串 | 人员的照片的URL。 |
| `extendedWorkDetails.reportsToID` | 字符串 | 人员的报表管理器的标识符。 |
| `faxPhone` | [电话号码](../../data-types/phone-number.md) | 人员的传真电话号码。 |
| `homeAddress` | [邮政地址](../../data-types/postal-address.md) | 人员的家庭地址。 |
| `homePhone` | [电话号码](../../data-types/phone-number.md) | 人员的住宅电话号码。 |
| `mobilePhone` | [电话号码](../../data-types/phone-number.md) | 人员的手机号码。 |
| `otherAddress` | [邮政地址](../../data-types/postal-address.md) | 人员的备用地址。 |
| `otherPhone` | [电话号码](../../data-types/phone-number.md) | 人员的备用电话号码。 |
| `person` | [人员](../../data-types/person.md) | 单独的操作者、联系人或所有者。 |
| `personalEmail` | [电子邮件地址](../../data-types/email-address.md) | 人员的个人电子邮件地址。 |
| `workAddress` | [邮政地址](../../data-types/postal-address.md) | 人员的工作地址。 |
| `workEmail` | [电子邮件地址](../../data-types/email-address.md) | 人员的工作电子邮件地址。 |
| `workPhone` | [电话号码](../../data-types/phone-number.md) | 人员的工作电话号码。 |
| `identityMap` | 地图 | 包含人员的一组命名空间标识的映射字段。 此字段在摄取身份数据时由系统自动更新。 为了正确使用此字段 [Real-time Customer Profile](../../../profile/home.md)中，请勿尝试在数据操作中手动更新字段内容。<br /><br />请参阅中有关身份映射的部分 [模式组合基础](../../schema/composition.md#identityMap) 以了解有关其用例的更多信息。 |
| `isDeleted` | 布尔值 | 指示此人是否已在Marketo Engage中删除。<br><br>使用时 [Marketo源连接器](../../../sources/connectors/adobe-applications/marketo/marketo.md)，则在Marketo中删除的任何记录都会自动反映在实时客户档案中。 但是，与这些用户档案相关的记录仍可能会保留在数据湖中。 通过设置 `isDeleted` 到 `true`，则可在查询数据湖时，使用字段过滤出已从源中删除的记录。 |
| `organizations` | 字符串数组 | 人员工作的组织名称列表。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)

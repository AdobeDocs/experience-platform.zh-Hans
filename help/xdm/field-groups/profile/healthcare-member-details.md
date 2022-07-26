---
title: 医疗保健成员详细信息架构字段组
description: 本文档概述了医疗保健成员详细信息架构字段组。
source-git-commit: a51079ff1686ecae3e5fe9f0170b28bc16bcef86
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 4%

---

# [!UICONTROL 医疗保健会员详细信息] 架构字段组

[!UICONTROL 医疗保健会员详细信息] 是的标准架构字段组 [[!DNL XDM Individual Profile] 类](../../classes/individual-profile.md) ，可捕获拥有或将接受医疗服务或护理的人员的详细信息，例如联系信息、初级保健医生和计划信息。

![字段组结构](../../images/field-groups/healthcare-member-details/structure.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL 邮政地址]](../../data-types/postal-address.md) | 人员的帐单地址。 |
| `faxPhone` | [[!UICONTROL 电话号码]](../../data-types/phone-number.md) | 此人的传真电话号码。 |
| `homeAddress` | [[!UICONTROL 邮政地址]](../../data-types/postal-address.md) | 此人的家庭地址。 |
| `homePhone` | [[!UICONTROL 电话号码]](../../data-types/phone-number.md) | 此人的家庭电话号码。 |
| `mailingAddress` | [[!UICONTROL 邮政地址]](../../data-types/postal-address.md) | 此人的通讯地址。 |
| `memberDetails` | 对象 | 一个对象，其中包含有关人员的医疗保健相关属性和关系的详细信息。 请参阅 [下文](#memberDetails) 以了解有关对象结构的详细信息。 |
| `mobilePhone` | [[!UICONTROL 电话号码]](../../data-types/phone-number.md) | 人员的手机号码。 |
| `person` | [[!UICONTROL 人员]](../../data-types/person.md) | 与人员的医疗会员资格相关的个人行为者、联系人或所有者。 |
| `personalEmail` | [[!UICONTROL 电子邮件地址]](../../data-types/email-address.md) | 人员的个人电子邮件地址。 |
| `shippingAddress` | [[!UICONTROL 邮政地址]](../../data-types/postal-address.md) | 人的送货地址。 |

{style=&quot;table-layout:auto&quot;}

## `memberDetails` {#memberDetails}

`memberDetails` 是一个对象，其中包含有关人员医疗保健相关属性和关系的详细信息。 的结构 `memberDetails` 下面介绍了。

![memberDetails结构](../../images/field-groups/healthcare-member-details/memberDetails.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `emergencyContact` | 对象 | 为人员捕获以下紧急联系详细信息： <ul><li>`fullName`:（字符串）紧急联系人的全名。</li><li>`phone`:（字符串）紧急联系人的电话号码。</li><li>`relationshipToMember`:（字符串）紧急联系人与人员的关系。</li></ul> |
| `medications` | 对象数组 | 列出与人员相关的当前和过去药物的详细信息。 每个数组项目都是一个用于捕获以下详细信息的对象： <ul><li>`refillLocation`:([[!UICONTROL 邮政地址]](../../data-types/postal-address.md))药物的填充位置。</li><li>`ID`:（字符串）药物ID。</li><li>`isCurrent`:（布尔值）指示药物是当前还是过去。</li><li>`numberOfRefills`:（整数）由本药物供应商规定的重填次数。</li><li>`startDate`:(DateTime)人开始服药的日期。</li></ul> |
| `multipleBirth` | 对象 | 捕获与多胎有关的详细信息： <ul><li>`isMultipleBirth`:（布尔值）指示人是否分娩过多次。</li><li>`multipleBirthNumber`:（整数）如果 `isMultipleBirth` 是真的。</li></ul> |
| `plans` | 对象数组 | 列出与人员关联的当前和过去医疗计划的详细信息。 每个数组项目都是一个用于捕获以下详细信息的对象： <ul><li>`coverageEndDate`:(DateTime)计划范围结束的日期。</li><li>`coverageStartDate`:(DateTime)计划覆盖范围开始的日期。</li><li>`isActive`:（布尔值）指示计划是否处于活动状态。</li><li>`planId`:（字符串）计划ID。</li></ul> |
| `primaryCarePhysicians` | 对象数组 | 列出与该人相关的初级保健医师的详细信息。 每个数组项目都是一个用于捕获以下详细信息的对象： <ul><li>`endDate`:(DateTime)初级保健医师结束对该人的护理的日期。</li><li>`fullname`:（字符串）医生的全名。</li><li>`providerId`:（字符串）医生的唯一标识符。</li><li>`startDate`:(DateTime)初级保健医师开始照料人的日期。</li></ul> |
| `specialists` | 对象数组 | 列出与该人员关联的医疗保健专家的详细信息。 每个数组项目都是一个用于捕获以下详细信息的对象： <ul><li>`fullname`:（字符串）专家的全名。</li><li>`providerId`:（字符串）专家的唯一标识符。</li><li>`specialty`:（字符串）提供者的专业（如麻醉学、泌尿科、放射科、皮肤病学等）。</li></ul> |
| `beneficiaryRelationship` | 字符串 | 如果该人是受扶养人，则与医疗保健成员的受益关系（例如，自己、配偶、子女等）。 |
| `billingAccountID` | 字符串 | 人员账单帐户的唯一标识符。 |
| `dateAgeCollected` | DateTime | 收集人的年龄的日期。 |
| `deceasedDate` | DateTime | 死者死亡的日期。 |
| `isDeceased` | 布尔型 | 指示此人是否已死亡。 |
| `isDependent` | 布尔型 | 指示人员是否为从属人员。 |
| `nationality` | 字符串 | 人与其国家之间的法律关系，使用ISO 3166-1 Alpha-2代码表示。 |
| `preferredAvailability` | 字符串 | 人员首选的约会日期和时间。 |
| `primaryMemberID` | 字符串 | 主用户的唯一标识符（如果人员是从属用户）。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充的示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [完整模式](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

有关如何使用此字段组来提供通用字段的更多信息，请参阅行业模式文档 [医疗保健行业用例](../../schema/industries/healthcare.md).

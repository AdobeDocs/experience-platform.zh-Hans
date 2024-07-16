---
title: 医疗保健提供商架构字段组
description: 了解医疗保健提供商架构字段组。
exl-id: e39b4082-4b66-47b3-a8e2-951d8a96f742
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 3%

---

# [!UICONTROL 医疗保健提供商]架构字段组

[!UICONTROL 医疗保健提供商]是[[!UICONTROL 提供商]类](../../classes/provider.md)的标准架构字段组。 它提供单个对象类型字段`healthcareProvider`，该字段捕获与获得授权提供医疗保健诊断和治疗服务的个人医疗保健专业人员或医疗保健机构组织相关的属性。

![](../../images/field-groups/healthcare-provider.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `addressDetails` | 对象数组 | 列出提供商的地址详细信息。 每个对象都包含以下属性： <ul><li>`address`： （[[!UICONTROL 邮政地址]](../../data-types/postal-address.md)）：提供商的邮政地址。</li><li>`addressType`： （字符串）地址的类型，指示提供程序在何处提供服务。</li></ul> |
| `emailAddress` | [[!UICONTROL 电子邮件地址]](../../data-types/email-address.md) | 提供商的电子邮件地址。 |
| `fax` | [[!UICONTROL 电话号码]](../../data-types/phone-number.md) | 提供商的传真号码。 |
| `phoneNumber` | [[!UICONTROL 电话号码]](../../data-types/phone-number.md) | 提供商的电话号码。 |
| `qualifications` | 对象数组 | 列出与提供护理相关的认证、许可证或培训。 每个对象都包含以下属性： <ul><li>`issuer`： （[[!UICONTROL 帐户详细信息]](../../data-types/account-details.md)）：管理和发布资格鉴定的组织。</li><li>`activePeriod`： （整数）资格有效之前的年份。</li><li>`code`： （字符串）资格的编码表示形式。</li></ul> |
| `classification` | 字符串 | 基于类别或类别（例如患者护理、非患者护理等）的服务提供商分类。 |
| `isActive` | 布尔值 | 指示提供程序是否处于活动状态。 |
| `languages` | 字符串数组 | 提供商在其下执行操作的语言的列表。 |
| `practiceGroupName` | 字符串 | 服务提供商的实践组名称。 |
| `practiceGroupType` | 字符串 | 服务提供商的实践组类型。 |
| `practiceType` | 字符串 | 服务提供商的实践类型。 |
| `specialties` | 字符串数组 | 此提供商提供的专业列表。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅[公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json)。

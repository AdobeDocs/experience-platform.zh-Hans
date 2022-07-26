---
title: 医疗保健提供商架构字段组
description: 本文档概述了医疗保健提供商架构字段组。
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 5%

---

# [!UICONTROL 医疗保健提供商] 架构字段组

[!UICONTROL 医疗保健提供商] 是的标准架构字段组 [[!UICONTROL 提供程序] 类](../../classes/provider.md). 它提供单个对象类型字段 `healthcareProvider` 其捕获与个人健康专业人员或获得提供医疗诊断和治疗服务许可的医疗设施组织有关的属性。

![](../../images/field-groups/healthcare-provider.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `addressDetails` | 对象数组 | 列出提供商的地址详细信息。 每个对象包含以下属性： <ul><li>`address`:([[!UICONTROL 邮政地址]](../../data-types/postal-address.md)):提供商的邮政地址。</li><li>`addressType`:（字符串）地址类型，指示提供商提供服务的位置。</li></ul> |
| `emailAddress` | [[!UICONTROL 电子邮件地址]](../../data-types/email-address.md) | 提供商的电子邮件地址。 |
| `fax` | [[!UICONTROL 电话号码]](../../data-types/phone-number.md) | 提供商的传真号码。 |
| `phoneNumber` | [[!UICONTROL 电话号码]](../../data-types/phone-number.md) | 提供商的电话号码。 |
| `qualifications` | 对象数组 | 列出与提供护理相关的认证、许可或培训。 每个对象包含以下属性： <ul><li>`issuer`:([[!UICONTROL 帐户详细信息]](../../data-types/account-details.md)):规范和颁发资格的组织。</li><li>`activePeriod`:（整数）资格有效的年份。</li><li>`code`:（字符串）资格的编码表示形式。</li></ul> |
| `classification` | 字符串 | 服务提供商基于类别或类别（如患者护理、非患者护理等）的分类。 |
| `isActive` | 布尔型 | 指示提供程序是否处于活动状态。 |
| `languages` | 字符串数组 | 提供商执行操作的语言列表。 |
| `practiceGroupName` | 字符串 | 服务提供商的惯例组名称。 |
| `practiceGroupType` | 字符串 | 服务提供商的惯例组类型。 |
| `practiceType` | 字符串 | 服务提供商的实践类型。 |
| `specialties` | 字符串数组 | 该提供商提供的专业课程列表。 |

{style=&quot;table-layout:auto&quot;}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).

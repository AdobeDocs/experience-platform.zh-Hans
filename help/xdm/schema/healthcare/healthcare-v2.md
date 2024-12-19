---
title: 医疗保健数据模型V2
description: 了解一些常见医疗保健用例以及要使用的最佳类、相关字段组和数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a796b58b-b36f-4277-870b-0d3939af8061
source-git-commit: 6d1745b93d2ad7cf6ef96510bd5128a43de9ef03
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 3%

---

# [!UICONTROL 医疗保健]数据模型V2

## 字段组和类 {#field-groups}

下表概述了多个常见医疗保健用例的推荐类和架构字段组。

| 用例 | 字段组和兼容类 |
| --- | --- |
| **创建/更新患者**：当患者到达医院前台时，将建立患者记录，包括诸如标识符（可选）、患者姓名、出生日期、性别和地址等人口统计详细信息。 这是医疗保健IT的重要组成部分。 | <ul><li>**[XDM个人资料](../../classes/individual-profile.md)**：<ul><li>[患者](./field-groups/patient.md)</li></ul></li></ul> |
| **疫苗接种**：促进疫苗接种过程，管理患者免疫记录，并将EMR与疫苗管理系统集成。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**：<ul><li>[免疫](./field-groups/immunization.md)</li></ul></li><li>**[XDM个人资料](../../classes/individual-profile.md)**：<ul><li>[药物分配](./field-groups/medication-dispense.md)</li><li>[药物请求](./field-groups/medication-request.md)</li><li>[患者](./field-groups/patient.md)</li></ul></li><li>**[位置](./classes/location.md)**：<ul><li>[位置](./field-groups/location.md)</li></ul><li>**[药物](../../classes/medication.md)**：<ul><li>[药物](./field-groups/medication.md)</li><li>[药物分配](./field-groups/medication-dispense.md)</li><li>[药物请求](./field-groups/medication-request.md)</li></ul></li><li>**[提供程序](../../classes/provider.md)**：<ul><li>[药物分配](./field-groups/medication-dispense.md)</li><li>[药物请求](./field-groups/medication-request.md)</li></ul></li></ul> |
| **后期护理遵守情况**：激励病人和护理人员完成他们的治疗计划并降低汇款率。 | <ul><li>**[XDM个人资料](../../classes/individual-profile.md)**：<ul><li>[保护计划](./field-groups/care-plan.md)</li><li>[目标](./field-groups/goal.md)</li><li>[患者](./field-groups/patient.md)</li></ul></li><li>**[位置](./classes/location.md)**：<ul><li>[位置](./field-groups/location.md)</li></ul><li>**[提供程序](../../classes/provider.md)**：<ul><li>[目标](./field-groups/goal.md)</li></ul></li></ul> |
| **保险的消费者体验**：改善购买保险的消费者的数字获取和体验。 示例包括： <li> 了解消费者向访问包含常规信息（如计划、计划名称/层、Medicaid或健康计划）页面的用户发送促销电子邮件或定向第三方广告的行为</li><li> 向寻找心脏健康和疫苗信息的人发送有关心脏健康的疫苗信息，以建立品牌意识，或请求安排疫苗接种时间。 </li> | <ul><li>**[XDM个人资料](../../classes/individual-profile.md)**：<ul><li>[帐户](./field-groups/account.md)</li><li>[药物分配](./field-groups/medication-dispense.md)</li><li>[药物请求](./field-groups/medication-request.md)</li><li>[患者](./field-groups/patient.md)</li></ul></li><li>**[位置](./classes/location.md)**：<ul><li>[位置](./field-groups/location.md)</li></ul><li>**[药物](../../classes/medication.md)**：<ul><li>[药物](./field-groups/medication.md)</li><li>[药物分配](./field-groups/medication-dispense.md)</li><li>[药物请求](./field-groups/medication-request.md)</li></ul></li><li>**[提供程序](../../classes/provider.md)**：<ul><li>[帐户](./field-groups/account.md)</li><li>[药物分配](./field-groups/medication-dispense.md)</li><li>[药物请求](./field-groups/medication-request.md)</li></ul><li>**[计划](../../classes/plan.md)**：<ul><li>[目标](./field-groups/coverage.md)</li></ul></li></ul> |
| **增强的提供程序体验**：使用EMR系统中的提供程序数据根据约会可用性、位置和专业建议替代提供程序。<br> <br>改进提供程序搜索以显示具有所需可用性的结果，验证所选提供程序是否为付款人网络的一部分，并提供成本估算。 | <ul><li>**[XDM个人资料](../../classes/individual-profile.md)**：<ul><li>[约会](./field-groups/appointment.md)</li><li>[组织](./field-groups/organization.md)</li><li>[患者](./field-groups/patient.md)</li><li>[从业者](./field-groups/practioner.md)</li><li>[计划](./field-groups/schedule.md)</li></ul></li><li>**[位置](./classes/location.md)**：<ul><li>[位置](./field-groups/location.md)</li></ul><li>**[提供程序](../../classes/provider.md)**：<ul><li>[约会](./field-groups/appointment.md)</li><li>[组织](./field-groups/organization.md)</li><li>[从业者](./field-groups/practioner.md)</li><li>[计划](./field-groups/schedule.md)</li></ul></li></ul> |

{style="table-layout:fixed"}

## 数据类型 {#data-types}

下表概述了根据[!DNL HL7 FHIR Release 5]规范创建的数据类型。

| 名称 | 描述 |
| --- | --- |
| [[!UICONTROL 地址]](./data-types/address.md) | 描述使用邮政惯例表示的地址（与GPS或其他位置定义格式不同）。 |
| [[!UICONTROL 批注]](./data-types/annotation.md) | 归因于作者的文本节点。 |
| [[!UICONTROL 可用性]](./data-types/availability.md) | 项目的可用性数据。 |
| [[!UICONTROL 可编码的概念]](./data-types/codeable-concept.md) | 从一个资源到另一个资源的引用。 |
| [[!UICONTROL 可编码引用]](./data-types/codeable-reference.md) | 对资源或概念的引用。 |
| [[!UICONTROL 编码]](./data-types/coding.md) | 对术语系统定义的代码的引用。 |
| [[!UICONTROL 联系点]](./data-types/contact-point.md) | 人员的联系详细信息。 |
| [[!UICONTROL 剂量]](./data-types/dosage.md) | 服药方式或应服药方式。 |
| [[!UICONTROL 持续时间]](./data-types/duration.md) | 时间长度。 |
| [[!UICONTROL 扩展的联系人详细信息]](./data-types/extended-contact-detail.md) | 扩展联系人的信息。 |
| [[!UICONTROL 人名]](./data-types/human-name.md) | 有关人类或其他生命实体的名称的信息。 |
| [[!UICONTROL 标识符]](./data-types/identifier.md) | 用于计算的标识符。 |
| [[!UICONTROL 钱]](./data-types/money.md) | 以某种公认货币表示的经济效用金额。 |
| [[!UICONTROL 周期]](./data-types/period.md) | 由开始和结束日期/时间定义的时间段。 |
| [[!UICONTROL 人员]](./data-types/person.md) | 有关一般人员记录的信息。 |
| [[!UICONTROL 数量]](./data-types/quantity.md) | 可衡量的金额。 |
| [[!UICONTROL Range]](./data-types/range.md) | 由低值和高值绑定的一组值。 |
| [[!UICONTROL 比率]](./data-types/ratio.md) | 通过分子和分母两个[[!UICONTROL 数量]](./data-types/quantity.md)值的比率。 |
| [[!UICONTROL 引用]](./data-types/reference.md) | 从一个资源到另一个资源的引用。 |
| [[!UICONTROL 重复]](./data-types/repeat.md) | 描述事件计划时间的一组规则。 |
| [[!UICONTROL 简单数量]](./data-types/simple-quantity.md) | 可衡量的金额。 |
| [[!UICONTROL 计时]](./data-types/timing.md) | 有关可能发生多次的事件的信息。 |
| [[!UICONTROL 虚拟服务详细信息]](./data-types/virtual-service-detail.md) | 虚拟服务联系人详细信息。 |


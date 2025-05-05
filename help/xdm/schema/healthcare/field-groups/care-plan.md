---
title: 关怀计划架构字段组
description: 了解护理计划架构字段组。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e6cbf44f-6c39-42bd-b083-a975860a64db
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 4%

---

# [!UICONTROL 保护计划]架构字段组

[!UICONTROL 保护计划]是[[!DNL XDM Individual Profile] 类](../../../classes/individual-profile.md)的标准架构字段组。 它提供单个对象类型字段`healthcareCarePlan`，用于捕获患者或组的医疗保健计划。

![字段组结构](../../../images/healthcare/field-groups/care-plan/care-plan.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 活动] | `activity` | 对象数组 | 标识已在计划中发生或计划在计划中发生的操作。 有关详细信息，请参阅下面[&#128279;](#activity)的部分。 |
| [!UICONTROL 地址] | `addresses` | [[!UICONTROL 可编码引用]](../data-types/codeable-reference.md)的数组 | 确定护理计划处理的条件或问题。 |
| [!UICONTROL 基于] | `basedOn` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 由此护理计划全部或部分履行的更高级别请求资源。 |
| [!UICONTROL 关怀团队] | `careTeam` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 确定预期将参与此计划所设想的护理的所有人员和组织。 |
| [!UICONTROL 类别] | `category` | [[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)的数组 | 确定这是什么类型的计划，以支持区分多个并存计划。 |
| [!UICONTROL 参与者] | `contributor` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 标识提供护理计划内容的个人、组织或设备。 |
| [!UICONTROL 保管人] | `custodian` | [[!UICONTROL 引用]](../data-types/reference.md) | 填充后，托管人将负责并归属于该托管计划。 |
| [!UICONTROL 相遇] | `encounter` | [[!UICONTROL 引用]](../data-types/reference.md) | 创建护理计划的过程。 |
| [!UICONTROL 目标] | `goal` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 执行计划的预定目标。 |
| [!UICONTROL 标识符] | `identifier` | [[!UICONTROL 标识符]](../data-types/identifier.md)的数组 | 执行者或其他系统分配给此保护计划的业务标识符在资源更新时保持不变，并在服务器之间传播。 |
| [!UICONTROL 注释] | `note` | [[!UICONTROL 批注]](../data-types/annotation.md)的数组 | 有关其他属性中未涵盖的护理计划的一般说明。 |
| 的部分 | `partOf` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 大型护理计划，其中此特定护理计划是组成部分或步骤。 |
| [!UICONTROL 周期] | `period` | [[!UICONTROL 周期]](../data-types/period.md) | 指示计划何时生效（或计划何时生效）以及何时结束。 |
| [!UICONTROL 替换] | `replaces` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 已完成或已终止的护理计划，其功能由此护理计划接管。 |
| [!UICONTROL 主题] | `subject` | [[!UICONTROL 引用]](../data-types/reference.md) | 确定计划描述其预期护理的病人或组。 |
| [!UICONTROL 支持信息] | `supportingInfo` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 标识影响计划制定的患者记录部分。 这些可能包括共病、最近的程序、限制或最近的评估。 |
| [!UICONTROL 已创建] | `created` | 日期时间 | 表示在系统中创建此医疗保健计划的时间，这通常是系统生成的日期。 |
| [!UICONTROL 描述] | `description` | 字符串 | 对计划的范围和性质的描述。 |
| [!UICONTROL 实例化Canonical] | `instantiatesCanonical` | 字符串数组 | 指向FHIR定义的协议、指南、调查表或此计划完全或部分遵守的其他定义的URL。 |
| [!UICONTROL 实例化URI] | `instantiatesUri` | 字符串数组 | 指向外部维护的协议、指南、调查表或此计划完全或部分遵守的其他定义的URL，表示为URI。 |
| [!UICONTROL 意图] | `intent` | 字符串 | 护理计划的目的。 此属性的值必须等于以下已知枚举值之一。 <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `option` </li> <li> `directive` </li> |
| [!UICONTROL 状态] | `status` | 字符串 | 护理计划的状态。 此属性的值必须等于以下已知枚举值之一。 <li> `draft` </li> <li> `active` </li> <li> `on-hold` </li> <li> `revoked` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `unknown` </li> |
| [!UICONTROL 标题] | `title` | 字符串 | 护理计划的名称。 |

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.schema.json)

## `activity` {#activity}

`activity`作为对象数组提供。 每个对象的结构如下所述。

![活动结构](../../../images/healthcare/field-groups/care-plan/activity.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 已执行活动] | `performedActivity` | [[!UICONTROL 可编码引用]](../data-types/codeable-reference.md)的数组 | 活动的结果，如约会或程序。 |
| [!UICONTROL 计划的活动引用] | `plannedActivityReference` | [[!UICONTROL 引用]](../data-types/reference.md) | 建议活动的详细信息。 |
| [!UICONTROL 进度] | `progress` | [[!UICONTROL 批注]](../data-types/annotation.md)的数组 | 有关活动的遵守、状态或进度的说明。 |

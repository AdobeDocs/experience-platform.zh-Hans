---
title: 约会架构字段组
description: 了解约会架构字段组。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8224a2ee-51ac-4512-b0e4-5f1ab6bfddc4
source-git-commit: cb39966de77846758c16153f78fcf521f6a421e3
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 5%

---

# [!UICONTROL 约会]架构字段组

[!UICONTROL 约会]是[[!DNL XDM Individual Profile] 类](../../../classes/individual-profile.md)和[[!DNL Provider class]](../../../classes/provider.md)的标准架构字段组。 它提供单个对象类型字段`healthcareAppointment`，该字段包含有关患者、从业者、相关人员和/或设备在特定日期和时间预订医疗保健事件的信息。

![约会字段组结构的架构图。](../../../images/healthcare/field-groups/appointment/appointment.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 帐户] | `account` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 预期用于计费的帐户集。 |
| [!UICONTROL 约会类型] | `appointmentType` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 插槽中已预订的预约或患者的类型（不是服务类型）。 |
| [!UICONTROL 基于] | `basedOn` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 分配任用以进行评估的请求，如程序请求。 |
| [!UICONTROL 取消原因] | `cancellationReason` | [[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)的数组 | 取消约会的编码原因。 这通常用于报表、帐单或处理，以确定是否需要执行进一步操作或是否需支付特定费用。 |
| [!UICONTROL 类] | `class` | [[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)的数组 | 代表患者遭遇的分类（如动态、门诊、住院或紧急）的概念。 |
| [!UICONTROL 标识符] | `identifier` | [[!UICONTROL 标识符]](../data-types/identifier.md)的数组 | 链接到约会的唯一标识符列表。 这些标识符是根据业务规则分配的，或者在日程安排的直接URL链接不合适时分配的。 |
| [!UICONTROL 注释] | `note` | [[!UICONTROL 批注]](../data-types/annotation.md)的数组 | 有关约会的附加注释或评论。 |
| [!UICONTROL 原始约会] | `originatingAppointment` | [[!UICONTROL 引用]](../data-types/reference.md) | 定期相关约会集中的原始约会。 |
| [!UICONTROL 参与者] | `participant` | 对象数组 | 参与预约的参与者名单。 有关详细信息，请参阅下面[&#128279;](#participant)的部分。 |
| [!UICONTROL 患者说明] | `patientInstruction` | [[!UICONTROL 可编码引用]](../data-types/reference.md)的数组 | 诊断与约会相关。 |
| [!UICONTROL 上一个约会] | `previousAppointment` | [[!UICONTROL 引用]](../data-types/reference.md) | 历次相关任用中的上一个任用。 |
| [!UICONTROL 优先级] | `priority` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 预约的优先级，在需要重新确定预约优先级时，可用于做出明智的决策。 iCal标准将`0`指定为未定义，`1`指定为最高优先级，`9`指定为最低优先级。 |
| [!UICONTROL 原因] | `reason` | [[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)的数组 | 安排约会的原因，通常是条件或过程。 |
| [!UICONTROL 周期性模板] | `recurrenceTemplate` | 对象数组 | 包含用于创建定期约会的定期模式或模板的详细信息。  有关详细信息，请参阅下面[&#128279;](#recurrence)的部分。 |
| [!UICONTROL 替换] | `replaces` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 此约会将替换此约会。 如果存在取消操作，则可以在引用资源的`cancellationReason`属性中找到取消操作的详细信息。 |
| [!UICONTROL 请求时段] | `requestedPeriod` | [[!UICONTROL 周期]](../data-types/period.md)的数组 | 一组日期范围（可能包括时间），在此期间最好安排约会。 |
| [!UICONTROL 服务类别] | `serviceCategory` | [[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)的数组 | 要在约会期间执行的服务的广泛分类。 |
| [!UICONTROL 服务类型] | `serviceType` | [[!UICONTROL 可编码引用]](../data-types/codeable-reference.md)的数组 | 在约会期间要执行的特定服务。 |
| [!UICONTROL 插槽] | `slot` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 参与者日程安排中将由约会填充的时段。 |
| [!UICONTROL 专业] | `speciality` | [[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)的数组 | 执行此约会中要求的服务所需的从业人员的专长。 |
| [!UICONTROL 主题] | `subject` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 与约会关联的患者或组。 |
| [!UICONTROL 支持信息] | `supportingInformation` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 在做出支持该计划的预约时提供的其他信息。 |
| [!UICONTROL 虚拟服务] | `virtualService` | [[!UICONTROL 虚拟服务详细信息]](../data-types/virtual-service-detail.md)的数组 | 虚拟服务（如电话会议）的连接详细信息。 |
| [!UICONTROL 取消日期] | `cancellationDate` | 日期时间 | 取消约会的日期和时间。 |
| [!UICONTROL 已创建] | `created` | 日期时间 | 约会的创建日期和时间。 |
| [!UICONTROL 描述] | `description` | 字符串 | 约会的简要说明。 详细或扩展的信息应放在`note`字段中。 |
| [!UICONTROL 结束] | `end` | 日期时间 | 约会结束的日期和时间。 |
| [!UICONTROL 分钟持续时间] | `minutesDuration` | 整数 | 约会的时间（分钟）。 此值可以小于开始时间和结束时间之间的持续时间。 可接受的最小值为`0`。 |
| [!UICONTROL 实例已更改] | `occurenceChanged` | 布尔值 | 指示此约会是否不同于定期模式的标志。 |
| [!UICONTROL RecurrenceId] | `RecurrenceId` | 整数 | 以循环模式标识特定约会的序列号。 最小值为`0`。 |
| [!UICONTROL 开始] | `start` | 日期时间 | 约会的日期和时间。 |
| [!UICONTROL 状态] | `status` | 字符串 | 约会的状态。 此属性的值必须等于以下已知枚举值之一： <li> `proposed` </li> <li> `pending` </li> <li> `booked` </li> <li> `arrived` </li> <li> `fulfilled` </li> <li> `cancelled` </li> <li> `noshow` </li> <li> `entered-in-error` </li> <li> `checked-in` </li> <li> `waitlist` </li> |


有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/appointment.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/appointment.schema.json)

## `participant` {#participant}

`participant`作为对象数组提供。 每个对象的结构如下所述。

![参与者对象结构的架构图。](../../../images/healthcare/field-groups/appointment/participant.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 操作者] | `actor` | [[!UICONTROL 引用]](../data-types/reference.md) | 参与约会的个人、设备、位置或服务。 |
| [!UICONTROL 周期] | `period` | [[!UICONTROL 周期]](../data-types/period.md) | 参与人（行为人）参与预约的时间段。 |
| [!UICONTROL 类型] | `type` | [[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)的数组 | 参与人（行为人）在任用中的角色。 |
| [!UICONTROL 必需] | `required` | 布尔值 | 是否要求此参与者出席。 |
| [!UICONTROL 状态] | `status` | 字符串 | 参与者的接受状态。 此属性的值必须等于以下已知枚举值之一： <li> `accepted` </li> <li> `declined` </li> <li> `tentative` </li> <li> `needs-action` </li> |

## `recurrenceTemplate` {#recurrence}

`recurrenceTemplate`作为对象数组提供。 每个对象的结构如下所述。

![周期性模板对象结构的架构图。](../../../images/healthcare/field-groups/appointment/recurrence-template.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 每月模板] | `monthlyTemplate` | 对象数组 | 有关每月定期约会的信息。 有关详细信息，请参阅下面[&#128279;](#monthly-template)的部分。 |
| [!UICONTROL 周期性类型] | `recurrenceType` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 约会系列应重复出现的频率，如每周、每月或每年。 |
| [!UICONTROL 时区] | `timezone` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 定期约会的时区。 |
| [!UICONTROL 每周模板] | `weeklyTemplate` | 对象数组 | 有关每周定期约会的信息。 有关详细信息，请参阅下面[&#128279;](#weekly-template)的部分。 |
| [!UICONTROL 年度模板] | `yearlyTemplate` | 对象 | 有关年度定期约会的信息。 包含一个属性`yearInterval`，该属性包含一个整数值，指示约会每隔n年进行一次。 |
| [!UICONTROL 不包括日期] | `excludingDate` | 日期数组 | 应从循环中排除的任何日期，例如节假日。 |
| [!UICONTROL 排除周期性Id] | `excludingRecurrenceId` | 整数数组 | 应从循环中排除的任何循环ID。 这是`excludingDate`的替代方法，其中您指示要排除的约会`reccurenceID`。 |
| [!UICONTROL 上次出现日期] | `lastOccurenceDate` | 日期 | 不再计划定期约会的截止日期。 |
| [!UICONTROL 实例计数] | `occurenceCount` | 整数 | 循环中计划的约会数。 最小值为`0`。 |
| [!UICONTROL 发生日期] | `occurenceDate` | 日期数组 | 安排约会的具体日期列表。 |

## `weeklyTemplate` {#weekly-template}

`weeklyTemplate`作为对象数组提供。 每个对象的结构如下所述。

![每周模板对象结构的架构图。](../../../images/healthcare/field-groups/appointment/weekly-template.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 星期五] | `friday` | 布尔值 | 指示定期约会应在星期五。 |
| [!UICONTROL 星期一] | `monday` | 布尔值 | 指示定期约会应在星期一进行。 |
| [!UICONTROL 星期六] | `saturday` | 布尔值 | 指示定期约会应在星期六进行。 |
| [!UICONTROL 星期日] | `sunday` | 布尔值 | 指示定期约会应在星期日进行。 |
| [!UICONTROL 星期四] | `thursday` | 布尔值 | 指示定期约会应在星期四进行。 |
| [!UICONTROL 星期二] | `tuesday` | 布尔值 | 指示定期约会应在星期二进行。 |
| [!UICONTROL 星期三] | `wednesday` | 布尔值 | 指示定期约会应在星期三。 |
| [!UICONTROL 周间隔] | `weekInterval` | 整数 | 指定约会重复发生的频率（以每隔n周为单位）。 默认值为每周，因此典型值为2或更高。 |

## `monthlyTemplate` {#monthly-template}

`monthlyTemplate`作为对象数组提供。 每个对象的结构如下所述。

![每月模板对象结构的架构图。](../../../images/healthcare/field-groups/appointment/monthly-template.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 星期] | `dayOfWeek` | [[!UICONTROL 编码]] | 指示约会在一周中的这一天进行。 |
| 每月的第[!UICONTROL 周] | `nthWeekOfMonth` | [[!UICONTROL 编码]](../data-types/coding.md) | 指示约会应在一个月的第n周。 |
| [!UICONTROL 日期] | `dayOfMonth` | 整数 | 指示约会应该发生在当月的这一天。 |
| [!UICONTROL 月间隔] | `monthInterval` | 整数 | 指示定期约会应每隔n个月发生一次。 |


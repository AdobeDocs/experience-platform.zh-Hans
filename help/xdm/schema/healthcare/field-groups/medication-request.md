---
title: 药物请求架构字段组
description: 了解药物请求架构字段组。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8502380f-9557-4ca6-84bc-65010dfc6066
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 3%

---

# [!UICONTROL 药物请求]架构字段组

[!UICONTROL 药物请求]是[[!DNL Medication] 类](../../../classes/medication.md)、[[!DNL XDM Individual Profile] 类](../../../classes/individual-profile.md)和[[!DNL Provider class]](../../../classes/provider.md)的标准架构字段组。 它提供单个对象类型字段`healthcareMedicationDispense`，该字段捕获向患者提供药物和药物管理的指令的订单或请求。

![字段组结构](../../../images/healthcare/field-groups/medication-request/medication-request.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 基于] | `basedOn` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 由此药物请求履行的计划或请求。 |
| [!UICONTROL 类别] | `category` | [[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)的数组 | 药物请求的分类或分组。 |
| [!UICONTROL 治疗类型] | `courseOfTherapyType` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 对患者给药的整体模式的描述。 |
| [!UICONTROL 设备] | `device` | [[!UICONTROL 可编码引用]](../data-types/codeable-reference.md)的数组 | 用于给药的设备类型。 |
| [!UICONTROL 分配请求] | `dispenseRequest` | 对象 | 指示分配请求的特定详细信息，通常称为药物订单。 有关详细信息，请参阅下面[&#128279;](#dispense-request)的部分。 |
| [!UICONTROL 剂量说明] | `dosageInstructions` | [[!UICONTROL 剂量]](../data-types/dosage.md)的数组 | 病人如何使用该药物的具体说明。 |
| [!UICONTROL 有效剂量期] | `effectiveDosePeriod` | [[!UICONTROL 周期]](../data-types/period.md) | 服药的时限。 有多个`dosageInstruction`行的情况下（例如，逐步减少剂量时），这是剂量说明的最早日期和最晚日期。 |
| [!UICONTROL 相遇] | `encounter` | [[!UICONTROL 引用]](../data-types/reference.md) | 创建请求时遇到的情况。 |
| [!UICONTROL 事件历史记录] | `eventHistory` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 链接到与药物请求相关的事件记录，例如完成请求、关键状态过渡时间或相关更新。 |
| [!UICONTROL 组标识符] | `groupIdentifier` | [[!UICONTROL 标识符]](../data-types/identifier.md) | 由单个作者激活的多个独立请求实例中的共享标识符。 |
| [!UICONTROL 标识符] | `identifier` | [[!UICONTROL 标识符]](../data-types/identifier.md)的数组 | 与药物请求关联的标识符，这些标识符由业务流程定义，和/或在对资源本身的直接URL引用不合适时用于引用它。 |
| [!UICONTROL 信息Source] | `informationSource` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 为请求提供信息的人员或组织（如果源不是`requester`）。 |
| [!UICONTROL 保险] | `insurance` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 提供所请求的服务可能需要的保险计划、保险范围扩展、预授权和/或预确定。 |
| [!UICONTROL 药物] | `medication` | [[!UICONTROL 可编码引用]](../data-types/codeable-reference.md) | 标识正在请求的药物。 这应该是一个指向表示药物详细信息的资源的链接，或者是一个标识该药物的代码。 |
| [!UICONTROL 注释] | `note` | [[!UICONTROL 批注]](../data-types/annotation.md)的数组 | 其他属性无法传递的有关处方的其他信息。 |
| [!UICONTROL 执行者] | `performer` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 药物治疗/管理的指定执行者。 对于装置，这是用于执行药物管理的装置。 |
| [!UICONTROL 执行者类型] | `performerType` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 指示药物管理的执行者类型。 |
| [!UICONTROL 先前的处方] | `priorPrescription` | [[!UICONTROL 引用]](../data-types/reference.md) | 对由此请求替换的订单或处方进行的引用。 |
| [!UICONTROL 原因] | `reason` | [[!UICONTROL 可编码引用]](../data-types/reference.md)的数组 | 订购或不订购药物的原因或指示。 |
| [!UICONTROL 录制器] | `recorder` | [[!UICONTROL 引用]](../data-types/reference.md) | 代表另一个人输入订单的人员。 |
| [!UICONTROL 请求者] | `requester` | [[!UICONTROL 引用]](../data-types/reference.md) | 发起请求并负责激活请求的个人、组织或设备。 |
| [!UICONTROL 状态原因] | `statusReason` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 请求的当前状态的原因。 |
| [!UICONTROL 主题] | `subject` | [[!UICONTROL 引用]](../data-types/reference.md) | 申请药物的个人或团体。 |
| [!UICONTROL 替换] | `substitution` | 对象 | 指示替代是否可以或应该成为分配的一部分。 包含三个属性： <li>`allowedBoolean`：如果处方符允许替换，则布尔值为true。</li> <li>`allowedCodeableConcept`： [[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)值，在处方符允许替换时提供代码。</li> <li>`reason`：指示替代原因的[[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)值。</li> |
| [!UICONTROL 支持信息] | `supportingInformation` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 支持满足药物要求的信息，如患者的身高和体重。 |
| [!UICONTROL 创作于] | `authoredOn` | 日期时间 | 处方编写的日期(和（可选）时间。 |
| [!UICONTROL 不执行] | `doNotPerform` | 布尔值 | 一个布尔指示器，如果为true，则患者应停止（或不开始）服药。 |
| [!UICONTROL 意图] | `intent` | 字符串 | 请求的目的。 此属性的值必须等于以下已知枚举值之一。 <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `original-order` </li> <li> `reflex-order` </li> <li> `filler-order` </li> <li> `instance-order` </li> <li> `option` </li> |
| [!UICONTROL 优先级] | `priority` | 字符串 | 请求的优先级。 此属性的值必须等于以下已知枚举值之一。 <li> `routine` </li> <li> `urgent` </li> <li> `asap` </li> <li> `stat` </li> |
| [!UICONTROL 已渲染剂量说明] | `renderedDosageInstruction` | 字符串 | 所有剂量说明中包括的剂量的完整表示。 当包含多个剂量说明以表示例如增加或逐渐减少的剂量的复合剂量时使用。 |
| [!UICONTROL 已报告] | `reported` | 布尔值 | 指示此记录是否被捕获为辅助报告记录而不是原始主要真实来源记录。 |
| [!UICONTROL 状态] | `status` | 字符串 | 分发的状态。 此属性的值必须等于以下已知枚举值之一。 <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL 状态已更改] | `statusChanged` | 日期时间 | 状态更改的日期(和（可选）时间。 |

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.schema.json)

## `dispenseRequest` {#dispense-request}

`dispenseRequest`作为对象数组提供。 每个对象的结构如下所述。

![分配请求结构](../../../images/healthcare/field-groups/medication-request/dispense-request.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 分配间隔] | `dispenseInterval` | [[!UICONTROL 持续时间]](../data-types/duration.md) | 在药物分配之间必须发生的最短时间段。 |
| [!UICONTROL 分发器] | `dispenser` | [[!UICONTROL 引用]](../data-types/reference.md) | 按照处方人规定负责配药的组织。 |
| [!UICONTROL 分配器指令] | `dispenserInstruction` | [[!UICONTROL 批注]](../data-types/annotation.md)的数组 | 用于分配器的附加信息，例如要提供给患者的咨询 |
| [!UICONTROL 剂量管理辅助] | `doseAdministrationAid` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 有关为药物分配提供的粘合性包装类型的信息。 |
| [!UICONTROL 预期供应持续时间] | `expectedSupplyDuration` | [[!UICONTROL 持续时间]](../data-types/duration.md) | 所供应产品预计使用的时间段，或分配预计持续的时长。 |
| [!UICONTROL 初始填充] | `initialFill` | 对象 | 初始填充的信息。 包含两个属性： <li>`quantity`： [[!UICONTROL 简单数量]](../data-types/simple-quantity.md)值，提供第一次分配期间要提供的数量。</li> <li>`duration`： [[!UICONTROL Duration]](../data-types/duration.md)值，它提供第一个分配预期持续的时间长度。</li> |
| [!UICONTROL 数量] | `quantity` | [[!UICONTROL 简单数量]](../data-types/simple-quantity.md) | 为填充分配的金额。 |
| [!UICONTROL 有效期] | `validityPeriod` | [[!UICONTROL 周期]](../data-types/period.md) | 处方的有效期。 |
| [!UICONTROL 允许的重复次数] | `numberOfRepeatsAllowed` | 整数 | 授权的重新填充次数，最小值为0。 |

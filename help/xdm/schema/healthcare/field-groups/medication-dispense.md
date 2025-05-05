---
title: 药物分配架构字段组
description: 了解“药物配发”架构字段组。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e897c4e0-23ad-4d79-834f-cfbe2dbec771
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 3%

---

# [!UICONTROL 药物配发]架构字段组

[!UICONTROL 药物分配]是[[!DNL Medication] 类](../../../classes/medication.md)、[[!DNL XDM Individual Profile] 类](../../../classes/individual-profile.md)和[[!DNL Provider class]](../../../classes/provider.md)的标准架构字段组。 它提供单个对象类型字段`healthcareMedicationDispense`，该字段捕获有关要或已经分配给指定人员/患者的药物的信息。

![字段组结构](../../../images/healthcare/field-groups/medication-dispense/medication-dispense.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 授权处方] | `authorizingPrescription` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 允许配方的命令。 |
| [!UICONTROL 基于] | `basedOn` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 药物配发计划是依据的。 |
| [!UICONTROL 类别] | `category` | [[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)的数组 | 发放药品的种类，如药品法定种类或者药品种类。 |
| [!UICONTROL 天供应] | `daysSupply` | [[!UICONTROL 简单数量]](../data-types/simple-quantity.md) | 药物将为患者提供的天数。 |
| [!UICONTROL 目标] | `destination` | [[!UICONTROL 引用]](../data-types/reference.md) | 作为配发事件的一部分，药物曾经或即将发运到的设施或位置。 |
| [!UICONTROL 剂量说明] | `dosageInstruction` | [[!UICONTROL 剂量]](../data-types/dosage.md)的数组 | 描述患者要如何使用药物。 |
| [!UICONTROL 相遇] | `encounter` | [[!UICONTROL 引用]](../data-types/reference.md) | 建立此事件上下文的接触。 |
| [!UICONTROL 事件历史记录] | `eventHistory` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 围绕配发所发生的事件的摘要。 |
| [!UICONTROL 标识符] | `identifier` | [[!UICONTROL 标识符]](../data-types/identifier.md)的数组 | 与分配相关联的标识符。 标识符应由业务流程定义，和/或在直接URL引用不合适时用于引用它。 |
| [!UICONTROL 位置] | `location` | [[!UICONTROL 引用]](../data-types/reference.md) | 配发药物的主要物理位置。 |
| [!UICONTROL 药物] | `medication` | [[!UICONTROL 可编码引用]](../data-types/codeable-reference.md) | 标识正在请求的药物。 这应该是一个指向表示药物详细信息的资源的链接，或者是一个标识该药物的代码。 |
| [!UICONTROL 未执行原因] | `notPerformedReason` | [[!UICONTROL 可编码引用]](../data-types/codeable-reference.md) | 没有配药的原因。 |
| [!UICONTROL 注释] | `note` | [[!UICONTROL 批注]](../data-types/annotation.md)的数组 | 有关分配的附加信息。 |
| 的部分 | `partOf` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 触发分发的过程或药物请求。 |
| [!UICONTROL 执行者] | `performer` | 对象数组 | 指示执行分配事件的人员或人员。 有关详细信息，请参阅下面[&#128279;](#performer)的部分。 |
| [!UICONTROL 数量] | `quantity` | [[!UICONTROL 简单数量]](../data-types/simple-quantity.md) | 已分配的药物量，包括测量单位。 |
| [!UICONTROL 接收器] | `receiver` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 标识提取药物的人或交付药物的位置。 |
| [!UICONTROL 主题] | `subject` | [[!UICONTROL 引用]](../data-types/reference.md) | 指向资源的链接，该资源表示将向其提供药物的人或组。 |
| [!UICONTROL 替换] | `substitution` | 对象 | 指示是否在分配过程中进行了替换。 包含四个属性： <li>`wasSubstituted`：如果分发器请求替换，则布尔值为true。</li> <li>`type`： [[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)值，该值提供表示是否进行了替换的代码。</li> <li>`reason`：包含替代原因的[[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)值的数组。</li> <li>`responsibleParty`： [[!UICONTROL 引用]](../data-types/reference.md)值，它提供负责替代的人员或参与方。 </li> |
| [!UICONTROL 支持信息] | `supportingInformation` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 支持所分发药物的其他信息。 |
| [!UICONTROL 类型] | `type` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 描述所执行的分配事件的类型，例如紧急填充或部分填充。 |
| [!UICONTROL 已录制] | `recorded` | 日期时间 | 如果未填充`whenPrepared`或`whenHandedOver`，则为分配活动开始的日期和时间。 |
| [!UICONTROL 已渲染剂量说明] | `renderedDosageInstruction` | 字符串 | 所有剂量说明中包括的剂量的完整表示。 当包含多个剂量说明以表示例如增加或逐渐减少的剂量的复合剂量时使用。 |
| [!UICONTROL 状态] | `status` | 字符串 | 分发的状态。 此属性的值必须等于以下已知枚举值之一。 <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL 状态已更改] | `statusChanged` | 日期时间 | 配发记录状态更改的日期和时间。 |
| 移交时 | `whenHandedOver` | 日期时间 | 向患者提供所配发药物的日期和时间。 |
| [!UICONTROL 准备时] | `whenPrepared` | 日期时间 | 配发药品的包装和检查日期和时间。 |

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.schema.json)

## `performer` {#performer}

`performer`作为对象数组提供。 每个对象的结构如下所述。

![执行者结构](../../../images/healthcare/field-groups/medication-dispense/performer.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 操作者] | `actor` | [[!UICONTROL 引用]](../data-types/reference.md) | 执行操作的操作者（或类似人员）。 应该假定该行为者是药物的分配者。 |
| [!UICONTROL 函数] | `function` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 分发中的执行者类型，如日期输入者、打包者或最终检查者。 |

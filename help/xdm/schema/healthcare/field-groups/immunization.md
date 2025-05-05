---
title: 免疫方案字段组
description: 了解免疫模式字段组。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a392e26b-7631-4f54-b9ad-cc4586673ac5
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 8%

---

# [!UICONTROL 免疫]架构字段组

[!UICONTROL 免疫]是[[!DNL XDM Experience Event] 类](../../../classes/experienceevent.md)的标准架构字段组。 它提供捕获免疫事件信息的单个对象类型字段`healthcareImmunization`。

![字段组结构](../../../images/healthcare/field-groups/immunization/immunization.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 管理的产品] | `administeredProduct` | [[!UICONTROL 可编码引用]](../data-types/codeable-reference.md) | 受管理的产品。 |
| [!UICONTROL 基于] | `basedOn` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 免疫活动所依据的权威。 |
| [!UICONTROL 剂量数量] | `doseQuantity` | [[!UICONTROL 简单数量]](../data-types/simple-quantity.md) | 接种疫苗的量。 |
| [!UICONTROL 相遇] | `encounter` | [[!UICONTROL 引用]](../data-types/reference.md) | 免疫接种是这次事件的一部分。 |
| [!UICONTROL 为Source提供资金] | `fundingSource` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 疫苗的资金来源。 |
| [!UICONTROL 标识符] | `identifier` | [[!UICONTROL 标识符]](../data-types/identifier.md)的数组 | 业务标识符。 |
| [!UICONTROL 信息Source] | `informationSource` | [[!UICONTROL 可编码引用]](../data-types/codeable-reference.md) | 指示所报告记录的源。 |
| [!UICONTROL 位置] | `location` | [[!UICONTROL 引用]](../data-types/reference.md) | 免疫接种发生的地点。 |
| [!UICONTROL 制造商] | `manufacturer` | [[!UICONTROL 可编码引用]](../data-types/codeable-reference.md) | 疫苗制造商。 |
| [!UICONTROL 注释] | `note` | [[!UICONTROL 批注]](../data-types/annotation.md)的数组 | 额外的免疫接种说明。 |
| [!UICONTROL 患者] | `patient` | [[!UICONTROL 引用]](../data-types/reference.md) | 谁接种过疫苗。 |
| [!UICONTROL 批次] | `performer` | 对象数组 | 谁执行了免疫活动。 有关详细信息，请参阅下面[&#128279;](#performer)的部分。 |
| [!UICONTROL 计划资格] | `programEligibility` | 对象数组 | 患者是否有资格参加特定的疫苗接种计划。 有关详细信息，请参阅下面[&#128279;](#program-eligibility)的部分。 |
| 已应用[!UICONTROL 协议] | `protocolApplied` | 对象数组 | 提供商提供的协议。 有关详细信息，请参阅下面[&#128279;](#protocol-applied)的部分。 |
| [!UICONTROL 反应] | `reaction` | 对象数组 | 免疫接种后的反应细节。 有关详细信息，请参阅下面[&#128279;](#reaction)的部分。 |
| [!UICONTROL 原因] | `reason` | [[!UICONTROL 可编码引用]](../data-types/codeable-reference.md)的数组 | 免疫接种的原因。 |
| [!UICONTROL 路由] | `route` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 疫苗是如何进入人体的。 |
| [!UICONTROL 站点] | `site` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 接种疫苗的身体部位 |
| [!UICONTROL 状态原因] | `statusReason` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 当前状态的原因。 |
| [!UICONTROL 次幂原因] | `subpotentReason` | [[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)的数组 | 疫苗效力低的原因。 |
| [!UICONTROL 支持信息] | `supportingInformation` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 支持免疫接种的其他信息。 |
| [!UICONTROL 疫苗代码] | `vaccineCode` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 所接种疫苗的编码。 |
| [!UICONTROL 到期日期] | `expirationDate` | 日期 | 疫苗的有效期。 |
| [!UICONTROL 是次幂] | `isSubpotent` | 布尔值 | 该疫苗是否效力减弱的指标。 |
| [!UICONTROL 批号] | `lotNumber` | 字符串 | 疫苗的批号。 |
| [!UICONTROL 发生日期时间] | `occurenceDateTime` | 日期时间 | 疫苗接种日期。 |
| [!UICONTROL 出现字符串] | `occurenceString` | 字符串 | 疫苗接种日期。 |
| [!UICONTROL 主Source] | `primarySource` | 布尔值 | 指示是否从主源捕获数据。 |
| [!UICONTROL 状态] | `status` | 字符串 | 免疫接种的状态。 此属性的值必须等于以下已知枚举值之一。 <li> `completed` </li> <li> `entered-in-error` </li> <li> `not-done` </li> |

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/immunization.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/immunization.schema.json)

## `performer` {#performer}

`performer`作为对象数组提供。 每个对象的结构如下所述。

![执行者结构](../../../images/healthcare/field-groups/immunization/performer.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 操作者] | `actor` | [[!UICONTROL 引用]](../data-types/reference.md) | 执行操作的个人或组织。 |
| [!UICONTROL 函数] | `function` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 执行了何种类型的性能。 |

## `programEligibility` {#program-eligibility}

`programEligibility`作为对象数组提供。 每个对象的结构如下所述。

![项目资格结构](../../../images/healthcare/field-groups/immunization/program-eligibility.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 项目] | `program` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 声明其资格的程序。 |
| [!UICONTROL 项目状态] | `programStatus` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 患者参与计划的资格状态。 |

## `protocolApplied` {#protocol-applied}

`protocolApplied`作为对象数组提供。 每个对象的结构如下所述。

![协议应用的结构](../../../images/healthcare/field-groups/immunization/protocol-applied.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 授权] | `authority` | [[!UICONTROL 引用]](../data-types/reference.md) | 负责发布推荐的人员。 |
| [!UICONTROL 目标疾病] | `targetDisease` | [[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)的数组 | 疫苗所针对的可预防疾病。 |
| [!UICONTROL 剂量数] | `doseNumber` | 字符串 | 系列中的剂量数。 |
| [!UICONTROL 系列] | `series` | 字符串 | 疫苗系列的名称。 |
| [!UICONTROL 系列剂量] | `seriesDoses` | 字符串 | 建议的免疫剂量数量。 |

## `reaction` {#reaction}

`reaction`作为对象数组提供。 每个对象的结构如下所述。

![反应结构](../../../images/healthcare/field-groups/immunization/reaction.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 显示方式] | `manifestation` | [[!UICONTROL 可编码引用]](../data-types/codeable-concept.md) | 有关反应的其他信息。 |
| [!UICONTROL 日期] | `date` | 日期时间 | 反应开始的时候。 |
| [!UICONTROL 已报告] | `reported` | 字符串 | 指示反应是否为自我报告。 |

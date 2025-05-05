---
title: 覆盖范围架构字段组
description: 了解覆盖范围架构字段组。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 7b84c0cf-3bd4-4ba8-a8cc-85e6b3f2b59e
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 6%

---

# [!UICONTROL 覆盖范围]架构字段组

[!UICONTROL 覆盖率]是[[!DNL Plan] 类](../../../classes/plan.md)的标准架构字段组。 它提供单个对象类型字段`healthcareCoverage`，用于提供保险计划的高级标识符和描述符，通常是显示在保险卡上的信息，该信息可用于部分或全部支付医疗保健产品和服务的费用。

![字段组结构](../../../images/healthcare/field-groups/coverage/coverage.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 计划受益人] | `beneficiary` | [[!UICONTROL 引用]](../data-types/reference.md) | 享受保险的一方和提供产品或服务时的病人。 |
| [!UICONTROL 类] | `class` | 对象数组 | 包销商特定分类器的套件。 有关详细信息，请参阅下面[&#128279;](#class)的部分。 |
| [!UICONTROL 联系人] | `contract` | [[!UICONTROL 引用]](../data-types/reference.md)的数组 | 构成此保险的保单。 |
| [!UICONTROL 受益人成本] | `costToBeneficiary` | 对象数组 | 指示成本类别和相关金额的一套代码，这些代码已在政策中详述并且可能包含在健康卡上。 有关详细信息，请参阅下面[&#128279;](#cost-to-beneficiary)的部分。 |
| [!UICONTROL 异常] | `exception` | 对象数组 | 一组代码，用于指示患者成本及其有效期的例外或降低。 有关详细信息，请参阅下面[&#128279;](#exception)的部分。 |
| [!UICONTROL 标识符] | `identifier` | [[!UICONTROL 标识符]](../data-types/identifier.md)的数组 | 保险商颁发的保险的标识符。 |
| [!UICONTROL 保险计划] | `insurancePlan` | [[!UICONTROL 引用]](../data-types/reference.md) | 保险计划详细说明了构成此保险的福利和成本。 |
| [!UICONTROL 保险人] | `insurer` | [[!UICONTROL 引用]](../data-types/reference.md) | 计划或计划的承保人、付款人或保险公司。 |
| [!UICONTROL 付款方式：] | `paymentBy` | 对象数组 | 与支付方的链接，以及支付方将负责支付的内容（可选）。 有关详细信息，请参阅下面[&#128279;](#payment-by)的部分。 |
| [!UICONTROL 保险范围的开始和结束日期] | `period` | [[!UICONTROL 周期]](../data-types/period.md) | 保险范围处于活动状态的时段。 缺少开始日期表示开始日期未知，缺少结束日期表示保险范围正在进行中。 |
| [!UICONTROL 策略持有者] | `policyHolder` | [[!UICONTROL 引用]](../data-types/reference.md) | 持有保险单的一方。 |
| [!UICONTROL 受益人关系] | `relationship` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 受益人与订阅者的关系。 |
| [!UICONTROL 订阅者] | `subscriber` | [[!UICONTROL 引用]](../data-types/reference.md) | 与政策保持合同关系的一方。 |
| [!UICONTROL 订阅者标识符] | `subscriberId` | [[!UICONTROL 标识符]](../data-types/identifier.md)的数组 | 订阅者的保险分配ID。 |
| [!UICONTROL 类型] | `type` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 保险类型。 |
| [!UICONTROL 相关数字] | `dependent` | 字符串 | 覆盖下的家属指示符。 |
| [!UICONTROL 种类] | `kind` | 字符串 | 这种报道。 此属性的值必须等于以下已知枚举值之一。 <li> `insurance` </li> <li> `self-pay` </li> <li> `other` </li> |
| [!UICONTROL 保险公司网络] | `network` | 字符串 | 受益人可能寻求治疗的提供商网络，该网络将按网络内费率覆盖，否则将适用网络外条款和条件。 |
| [!UICONTROL 覆盖范围订单] | `order` | 整数 | 覆盖的相对顺序，最小值为`0`。 |
| [!UICONTROL 状态] | `status` | 字符串 | 保险的状态。 此属性的值必须等于以下已知枚举值之一。 <li> `active` </li> <li> `cancelled` </li> <li> `draft` </li> <li> `entered-in-error` </li> |
| [!UICONTROL 代位权] | `subrogation` | 布尔值 | 当`true`时，此保险实例已包括在内，不是为了裁决，而是为了向保险公司提供用于收回费用的详细信息。 |

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.schema.json)

## `class` {#class}

`class`作为对象数组提供。 每个对象的结构如下所述。

![类结构](../../../images/healthcare/field-groups/coverage/class.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 类型] | `type` | [[!UICONTROL 可编码概念]](../data-types/codeable-concept.md)的数组 | 提供特定于保险商的类别标签或编号和可选名称的分类类型。 例如，类型可用于标识保险类别、雇主组、政策或计划。 |
| [!UICONTROL 值] | `value` | [[!UICONTROL 标识符]](../data-types/identifier.md) | 与保险公司颁发的标签关联的字母数字标识符。 |
| [!UICONTROL 名称] | `name` | 字符串 | 类的简短描述。 |

## `costToBeneficiary` {#cost-to-beneficiary}

`costToBeneficiary`作为对象数组提供。 每个对象的结构如下所述。

![受益人结构的成本](../../../images/healthcare/field-groups/coverage/cost-to-beneficiary.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 类别] | `category` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 用于标识提供产品和服务的福利的常规类型的代码。 |
| [!UICONTROL 网络] | `network` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 用于指示权益是指网络内还是网络外提供商的代码。 |
| [!UICONTROL 术语] | `term` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 值的术语，如最大生命周期收益。 |
| [!UICONTROL 类型] | `type` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 与治疗相关的以患者为中心的成本类别。 |
| [!UICONTROL 单位] | `unit` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 指示福利是适用于个人还是适用于家庭。 |

## `exception` {#exception}

`exception`作为对象数组提供。 每个对象的结构如下所述。

![异常结构](../../../images/healthcare/field-groups/coverage/exception.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 类型] | `type` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 特定异常的代码。 |
| [!UICONTROL 周期] | `period` | [[!UICONTROL 周期]](../data-types/period.md) | 例外处于活动状态的时间范围。 |

## `paymentBy` {#payment-by}

`paymentBy`作为对象数组提供。 每个对象的结构如下所述。

![按结构付款](../../../images/healthcare/field-groups/coverage/payment-by.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 参与方] | `party` | [[!UICONTROL 引用]](../data-types/reference.md) | 为治疗费用提供非保险付款的各方名单。 |
| [!UICONTROL 责任] | `responsibility` | 字符串 | 财务责任的描述。 |

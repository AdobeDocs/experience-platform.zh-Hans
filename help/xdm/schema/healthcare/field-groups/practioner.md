---
title: 从业人员架构字段组
description: 了解Practioner架构字段组。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 71210303-a3dd-458c-9c8a-ac8b546c2b1d
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 7%

---

# [!UICONTROL Practioner]架构字段组

[!UICONTROL Practioner]是[[!DNL XDM Individual Profile] 类](../../../classes/individual-profile.md)和[[!DNL Provider class]](../../../classes/provider.md)的标准架构字段组。 它提供单个对象类型字段`healthcarePractioner`，该字段包含直接或间接参与提供医疗保健或相关服务的人员的信息。

![字段组结构](../../../images/healthcare/field-groups/practitioner/practitioner.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 地址] | `address` | [[!UICONTROL 地址]](../data-types/address.md)的数组 | 从业人员在工作场所以外的地址，如家庭地址。 |
| [!UICONTROL 通信] | `communication` | 对象数组 | 可用于与从业人员通信的语言。 有关详细信息，请参阅下面的[部分](#communication) |
| [!UICONTROL 标识符] | `identifier` | [[!UICONTROL 标识符]](../data-types/identifier.md)的数组 | 适用于此角色中人员的标识符。 |
| [!UICONTROL 名称] | `name` | [[!UICONTROL 人工名称]](../data-types/human-name.md)的数组 | 与从业者关联的名称。 |
| [!UICONTROL 资格] | `qualification` | 对象数组 | 正式资格、认证、认证、培训、执照或类似情况，这些授权或以其他方式与从业者提供的护理相关。 有关详细信息，请参阅下面[&#128279;](#qualification)的部分。 |
| [!UICONTROL 联系人详细信息] | `telecom` | [[!UICONTROL 联系点]](../data-types/contact-point.md)的数组 | 从业者的联系详细信息。 |
| [!UICONTROL 活动] | `active` | 布尔值 | 指示从业者记录是否正在使用中。 |
| [!UICONTROL 出生日期] | `birthDate` | 日期 | 从业者的出生日期。 |
| [!UICONTROL 已死亡的指示器] | `deceasedBoolean` | 布尔值 | 指示从业者是否死亡。 |
| [!UICONTROL 已死亡的日期时间] | `deceasedDateTime` | 日期时间 | 医生的死亡日期和时间。 |
| [!UICONTROL 性别] | `gender` | 字符串 | 人员的性别身份。 此属性的值必须等于以下已知枚举值之一。 <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/practitioner.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/practitioner.schema.json)

## `communication` {#communication}

`communication`作为对象数组提供。 每个对象的结构如下所述。

![通信结构](../../../images/healthcare/field-groups/practitioner/communication.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 语言] | `language` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 可用于与个人沟通有关其健康情况的语言。 |
| [!UICONTROL 是首选语言] | `preferred` | 布尔值 | 指示语言是否为他们的首选语言。 |

## `qualification` {#qualification}

`qualification`作为对象数组提供。 每个对象的结构如下所述。

![资格结构](../../../images/healthcare/field-groups/practitioner/qualification.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 代码] | `code` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 资格的编码表示形式。 |
| [!UICONTROL 标识符] | `identifier` | [[!UICONTROL 标识符]](../data-types/identifier.md)的数组 | 资格的标识符。 |
| [!UICONTROL 颁发者] | `issuer` | [[!UICONTROL 引用]](../data-types/reference.md) | 管理和发布资格的组织。 |
| [!UICONTROL 周期] | `period` | [[!UICONTROL 周期]](../data-types/period.md) | 资格的有效期。 |

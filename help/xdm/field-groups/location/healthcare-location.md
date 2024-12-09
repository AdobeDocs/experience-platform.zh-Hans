---
title: 位置架构字段组
description: 了解位置架构字段组。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 5%

---

# [!UICONTROL 位置]架构字段组

[!UICONTROL 位置]是[[!DNL Location] 类](../../classes/location.md)的标准架构字段组。 它提供单个对象类型字段`healthcareLocation`，用于捕获地标的详细信息和位置信息。

![字段组结构](../../images/field-groups/location.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 地址] | `address` | [[!UICONTROL 地址]](../../data-types/healthcare/address.md) | 物理位置的地址。 |
| [!UICONTROL 特性] | `characteristic` | [[!UICONTROL 可编码概念]](../../data-types/healthcare/codeable-concept.md)的数组 | 位置特征的集合。 |
| [!UICONTROL 联系人] | `contact` | [[!UICONTROL 扩展联系人详细信息]](../../data-types/healthcare/extended-contact-detail.md)的数组 | 位置的联系人详细信息。 |
| [!UICONTROL 终结点] | `endpoint` | [[!UICONTROL 引用]](../../data-types/healthcare/reference.md)的数组 | 为位置提供对操作服务的访问的技术端点。 |
| [!UICONTROL 表单] | `form` | [[!UICONTROL 可编码的概念]](../../data-types/healthcare/codeable-concept.md) | 位置的物理形式。 |
| [!UICONTROL 小时操作] | `hoursOfOperation` | [[!UICONTROL 可用性]](../../data-types/healthcare/availability.md)的数组 | 此位置通常会在哪些日期和时间打开（包括例外）。 |
| [!UICONTROL 标识符] | `identifier` | [[!UICONTROL 标识符]](../../data-types/healthcare/identifier.md)的数组 | 标识位置的唯一代码或编号。 |
| [!UICONTROL 管理组织] | `managingOrganization` | [[!UICONTROL 引用]](../../data-types/healthcare/reference.md) | 负责配置和维护的组织。 |
| [!UICONTROL 操作状态] | `operationalStatus` | [[!UICONTROL 编码]](../../data-types/healthcare/coding.md) | 位置的操作状态。 |
| [!UICONTROL 部分位置] | `partOf` | [[!UICONTROL 引用]](../../data-types/healthcare/reference.md) | 此位置所属的位置。 |
| [!UICONTROL 位置] | `position` | 对象 | 绝对地理位置。 包含双重格式的三个属性： <li>`longitude`：带有WGS84基准的经度</li> <li>`latitude`：具有WGS84基准的纬度。</li> <li>`altitude`：高度与WGS84基准。</li> |
| [!UICONTROL 类型] | `type` | [[!UICONTROL 可编码概念]](../../data-types/healthcare/codeable-concept.md)的数组 | 在该位置执行的功能的类型。 |
| [!UICONTROL 虚拟服务] | `virtualService` | [[!UICONTROL 虚拟服务详细信息]](../../data-types/healthcare/virtual-service-detail.md)的数组 | 虚拟服务的连接详细信息。 |
| [!UICONTROL 别名] | `alias` | 字符串数组 | 该位置称为或以前称为的备用名称列表。 |
| [!UICONTROL 描述] | `description` | 字符串 | 用于标识名称之外的位置的更多信息。 |
| [!UICONTROL 模式] | `mode` | 字符串 | 位置的模式。 此属性的值必须等于以下已知枚举值之一。 <li> `instance` </li> <li> `kind` </li> |
| [!UICONTROL 名称] | `name` | 字符串 | 位置的名称。 |
| [!UICONTROL 状态] | `status` | 字符串 | 位置的状态。 此属性的值必须等于以下已知枚举值之一。 <li> `active` </li> <li> `inactive` </li> <li> `suspended` </li> |

有关字段组的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.schema.json)

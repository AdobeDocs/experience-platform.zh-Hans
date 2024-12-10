---
title: 标识符数据类型
description: 了解标识符体验数据模型(XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 0664f52d-bea6-4aa1-b2a5-de0bd6d5edd9
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 9%

---

# [!UICONTROL 标识符]数据类型

[!UICONTROL Identifier]是标准体验数据模型(XDM)数据类型，它提供了用于计算的标识符。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![标识符数据类型结构](../../../images/healthcare/data-types/identifier.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 周期] | `period` | [[!UICONTROL 周期]](../data-types/period.md) | ID处于或有效使用的时段。 |
| [!UICONTROL 类型] | `type` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 标识符的描述。 |
| [!UICONTROL 分派人] | `assigner` | 字符串 | 颁发ID的组织。 |
| [!UICONTROL 系统] | `system` | 字符串 | 标识符值的命名空间，以URI表示。 |
| [!UICONTROL 使用] | `use` | 字符串 | 标识符的使用。 此属性的值必须等于以下一个或多个已知枚举值。 <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `secondary` </li> <li> `old` </li> |
| [!UICONTROL 值] | `value` | 字符串 | ID的唯一值。 |

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/identifier.schema.json)

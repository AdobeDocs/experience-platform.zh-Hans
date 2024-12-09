---
title: 地址数据类型
description: 了解Address Experience Data Model (XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 9%

---

# [!UICONTROL 地址]数据类型

[!UICONTROL 地址]是一个标准体验数据模型(XDM)数据类型，它描述了使用邮政惯例（而非GPS或其他位置定义格式）表示的地址。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![地址数据类型结构](../../images/data-types/healthcare/address.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 周期] | `period` | [[!UICONTROL 周期]](../healthcare/period.md) | 地址已使用/正在使用的时段。 |
| [!UICONTROL 城市] | `city` | 字符串 | 城市名称。 |
| [!UICONTROL 国家/地区] | `country` | 字符串 | ISO 3166国际标准中描述的国家代码。 代码可以是alpha-2或alpha-3。 |
| [!UICONTROL 地区] | `district` | 字符串 | 地区名称。 |
| [!UICONTROL 行] | `line` | 字符串 | 街道名称、编号、方向、邮政信箱或类似项。 |
| [!UICONTROL 邮政编码] | `postalCode` | 字符串 | 邮政编码。 |
| [!UICONTROL 状态] | `state` | 字符串 | 国家/地区的子单位。 缩写是可以接受的。 |
| [!UICONTROL 文本] | `text` | 字符串 | 地址的文本表示形式。 |
| [!UICONTROL 类型] | `type` | 字符串 | 地址类型。 此属性的值必须等于以下已知枚举值之一。 <li> `postal` </li> <li> `physical` </li> <li> `both` </li> |
| [!UICONTROL 使用] | `use` | 字符串 | 地址的目的。 此属性的值必须等于以下已知枚举值之一。 <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `billing`</li> |

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.schema.json)

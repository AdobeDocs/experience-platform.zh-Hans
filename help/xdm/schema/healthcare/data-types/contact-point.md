---
title: 联系点数据类型
description: 了解联系点体验数据模型(XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: bbb9a5e1-b0d5-4c07-93a9-c1573dacad73
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---

# [!UICONTROL 联系点]数据类型

[!UICONTROL 联系点]是描述人员联系详细信息的标准体验数据模型(XDM)数据类型。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![联系点数据类型结构](../../../images/healthcare/data-types/contact-point.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 周期] | `period` | [[!UICONTROL 周期]](../data-types/period.md) | 联系点正在使用的时段。 |
| [!UICONTROL 排名] | `rank` | 整数 | 表示首选使用联系点的排名。 最小值为`1`，最大值为`2147483647`，其中`1`是最高特异性。 |
| [!UICONTROL 系统] | `system` | 字符串 | 联系他们的系统。 此属性的值必须等于以下已知枚举值之一。 <li> `phone` </li> <li> `fax` </li> <li> `email` </li> <li> `pager`</li> <li> `url`</li> <li> `sms`</li> <li> `other`</li> |
| [!UICONTROL 使用] | `use` | 字符串 | 联系点的目的。 此属性的值必须等于以下已知枚举值之一。 <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `mobile`</li> |
| [!UICONTROL 值] | `value` | 字符串 | 联系点的详细信息。 |

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/contactpoint.schema.json)

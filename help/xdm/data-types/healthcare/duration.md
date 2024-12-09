---
title: 持续时间数据类型
description: 了解持续时间体验数据模型(XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 8%

---

# [!UICONTROL 持续时间]数据类型

[!UICONTROL 持续时间]是描述时间长度的标准体验数据模型(XDM)数据类型。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![持续时间数据类型结构](../../images/data-types/healthcare/duration.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 代码] | `code` | 字符串 | 时间单位的编码形式。 |
| [!UICONTROL 系统] | `system` | 字符串 | 描述编码单位（表示为URI）的系统。 |
| [!UICONTROL 单位] | `unit` | 字符串 | 以毫秒、秒、分钟、小时、天、周、月或年表示的时间单位。 此属性的值必须等于以下一个或多个已知枚举值。 <li> `ms` （毫秒） </li> <li> `s` （秒） </li> <li> `min` （分钟） </li> <li> `h` （小时） </li>  <li> `d` （天） </li> <li> `wk` （周） </li> <li> `mo` （月） </li> <li> `a` （年） </li> |
| [!UICONTROL 值] | `value` | 两次 | 时间单位的数值。 |

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/duration.schema.json)

---
title: 重复数据类型
description: 了解重复体验数据模型(XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 6%

---

# [!UICONTROL 重复]数据类型

[!UICONTROL Repeat]是一个标准的体验数据模型(XDM)数据类型，它提供了一组描述何时安排事件的规则。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![重复数据类型结构](../../images/data-types/healthcare/reference.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 绑定句点] | `boundsPeriod` | [[!UICONTROL 周期]](../healthcare/period.md) | 开始和结束时间。 |
| [!UICONTROL 绑定范围] | `boundsRange` | [[!UICONTROL Range]](../healthcare/range.md) | 范围限制。 |
| [!UICONTROL 绑定持续时间] | `boundsDuration` | [[!UICONTROL 持续时间]](../healthcare/duration.md) | 持续时间限制。 |
| [!UICONTROL 计数] | `count` | 整数 | 重复次数，最小值为`0`。 |
| [!UICONTROL 最大计数] | `countMax` | 整数 | 最大重复次数，最小值为`0`。 |
| [!UICONTROL 星期] | `dayOfWeek` | 字符串数组 | 一个字符串数组，详细说明可用日期。 此属性的值必须等于以下一个或多个已知枚举值。 <li> `mon` </li> <li> `tues` </li> <li> `wed` </li> <li> `thurs`</li>  <li> `fri` </li> <li> `sat`</li> <li> `sun`</li> |
| [!UICONTROL 持续时间] | `duration` | 两次 | 时间长度。 |
| [!UICONTROL 最长持续时间] | `durationMax` | 两次 | 最大时间长度。 |
| [!UICONTROL 持续时间单位] | `durationUnit` | 字符串 | 持续时间单位。 此属性的值必须等于以下一个或多个已知枚举值。 <li> `s` （秒） </li> <li> `min` （分钟） </li> <li> `h` （每小时） </li> <li> `d` （每天） </li>  <li> `wk` （每周） </li> <li> `mo` （每月） </li> <li> `a` （每年）</li> |
| [!UICONTROL 频率] | `frequency` | 两次 | 应在一个时间段内发生的重复次数，最小值为`0`。 |
| [!UICONTROL 最大频率] | `frequencyMax` | 两次 | 带句点的最大重复次数，最小值为`0`。 |
| [!UICONTROL 偏移] | `offset` | 整数 | 事件之前的分钟（之前或之后）。 |
| [!UICONTROL 周期] | `period` | 两次 | 应用频率的持续时间。 |
| [!UICONTROL 最大时段] | `periodMax` | 两次 | 期限的上限。 |
| [!UICONTROL 周期单位] | `periodUnit` | 字符串 | 时间单位。 此属性的值必须等于以下一个或多个已知枚举值。 <li> `s` （秒） </li> <li> `min` （分钟） </li> <li> `h` （每小时） </li> <li> `d` （每天） </li>  <li> `wk` （每周） </li> <li> `mo` （每月） </li> <li> `a` （每年）</li> |
| [!UICONTROL 时间] | `timeOfDay` | 字符串数组 | 操作在一天中发生的时间。 |
| [!UICONTROL When] | `when` | 字符串数组 | 操作时段的代码。 |

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/repeat.schema.json)

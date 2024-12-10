---
title: 计时数据类型
description: 了解Timing Experience Data Model (XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e1bc16ed-4dd8-4316-b3c8-88d49d393859
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 7%

---

# [!UICONTROL 计时]数据类型

[!UICONTROL 计时]是一种标准的体验数据模型(XDM)数据类型，它描述了一个计时计划，该计划提供有关可能发生多次的事件信息。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![计时数据类型结构](../../../images/healthcare/data-types/timing.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 活动] | `event` | 日期时间数组 | 事件发生时。 |
| [!UICONTROL 重复] | `repeat` | [[!UICONTROL 重复]](../data-types/repeat.md) | 有关事件发生时间的信息。 |
| [!UICONTROL 代码] | `code` | [[!UICONTROL 可编码的概念]](../data-types/codeable-concept.md) | 与事件相关的代码。 |

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/timing.schema.json)

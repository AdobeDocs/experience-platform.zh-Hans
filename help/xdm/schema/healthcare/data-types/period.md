---
title: 期间数据类型
description: 了解期间体验数据模型(XDM)数据类型。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: aecd09e4-2797-4d2d-be62-acad28fb7bba
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 10%

---

# [!UICONTROL 周期]数据类型

[!UICONTROL Period]是一个标准体验数据模型(XDM)数据类型，它提供了由开始和结束日期/时间定义的时间段。 此数据类型是根据HL7 FHIR Release 5规范创建的。

![期间数据类型结构](../../../images/healthcare/data-types/period.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 结束] | `end` | 日期时间 | 结束日期和时间。 |
| [!UICONTROL 开始] | `start` | 日期时间 | 开始日期和时间。 |

有关数据类型的更多详细信息，请参阅公共XDM存储库：

* [填充示例](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.example.1.json)
* [完整架构](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/period.schema.json)

---
title: 位置类
description: 了解体验数据模型(XDM)中的Location类。
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 7%

---

# [!UICONTROL 位置]类

在Experience Data Model (XDM)中，[!UICONTROL Location]类捕获实时活动位置信息，如旅游厅或体育场。

![位置类结构](../images/classes/location.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 标识符] | `_id` | [!UICONTROL 字符串] | 系统为记录生成的唯一字符串标识符。 此字段用于跟踪单个记录的唯一性，防止数据重复，并在下游服务中查找该记录。<br><br>由于此字段是系统生成的，因此不需要在数据引入期间向其提供显式值。 但是，如果您愿意，仍然可以选择提供自己的唯一ID值。 |
| [!UICONTROL 位置标识符] | `locationID` | [!UICONTROL 字符串] | 位置的唯一标识符。 |
| [!UICONTROL 位置名称] | `locationName` | [!UICONTROL 字符串] | 位置的名称。 |

可以使用[[!UICONTROL Location]字段组](../field-groups/location/healthcare-location.md)扩展该类，以描述有关位置的更多详细信息。

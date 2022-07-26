---
title: 计划类
description: 本文档概述了Experience Data Model(XDM)中的Plan类。
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 5%

---

# [!UICONTROL 计划] 类

在Experience Data Model(XDM)中， [!UICONTROL 计划] 类可捕获定义计划的最小属性集，如健康计划或保险计划。

![类结构](../images/classes/plan.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_id` | [!UICONTROL 字符串] | 记录的唯一、系统生成的字符串标识符。 此字段用于跟踪单个记录的唯一性，防止重复数据，并在下游服务中查找该记录。<br><br>由于此字段是系统生成的，因此在数据摄取期间不会为其提供显式值。 但是，如果您愿意，您仍可以选择提供您自己的唯一ID值。 |
| `planId` | [!UICONTROL 字符串] | 计划的唯一标识符。 |
| `planName` | [!UICONTROL 字符串] | 计划的名称。 |

{style=&quot;table-layout:auto&quot;}

类可以使用 [[!UICONTROL 医疗保健计划详细信息] 字段组](../field-groups/plan/healthcare-plan-details.md) 详细介绍健康保险计划。

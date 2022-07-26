---
title: 药物治疗类
description: 本文档概述了Experience Data Model(XDM)中的“药物”类。
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 5%

---

# [!UICONTROL 药物] 类

在Experience Data Model(XDM)中， [!UICONTROL 药物] 类可捕获定义用于医疗的物质（特别是药物或药物）的最小属性集。

![类结构](../images/classes/medication.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_id` | [!UICONTROL 字符串] | 记录的唯一、系统生成的字符串标识符。 此字段用于跟踪单个记录的唯一性，防止重复数据，并在下游服务中查找该记录。<br><br>由于此字段是系统生成的，因此在数据摄取期间不会为其提供显式值。 但是，如果您愿意，您仍可以选择提供您自己的唯一ID值。 |
| `medicationId` | [!UICONTROL 字符串] | 药物的唯一标识符。 |
| `medicationName` | [!UICONTROL 字符串] | 药物的名字。 |

{style=&quot;table-layout:auto&quot;}

类可以使用 [[!UICONTROL 一种保健药物] 字段组](../field-groups/medication/healthcare-medication.md) 以详细描述药物或药物。

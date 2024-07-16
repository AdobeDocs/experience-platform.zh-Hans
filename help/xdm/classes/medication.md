---
title: 药物类别
description: 了解Experience Data Model (XDM)中的“药物”类。
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 4%

---

# [!UICONTROL 药物]类

在体验数据模型(XDM)中，[!UICONTROL 药物]类捕获定义用于医疗的物质（特别是药物或药物）的最小属性集。

![类结构](../images/classes/medication.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_id` | [!UICONTROL 字符串] | 系统为记录生成的唯一字符串标识符。 此字段用于跟踪单个记录的唯一性，防止数据重复，并在下游服务中查找该记录。<br><br>由于此字段是系统生成的，因此在数据摄取期间不会向其提供显式值。 但是，如果您愿意，仍然可以选择提供自己的唯一ID值。 |
| `medicationId` | [!UICONTROL 字符串] | 药物的唯一标识符。 |
| `medicationName` | [!UICONTROL 字符串] | 药物的名称。 |

{style="table-layout:auto"}

可以使用[[!UICONTROL 医疗保健药物]字段组](../field-groups/medication/healthcare-medication.md)扩展该类，以描述有关该药物或药物的更多详细信息。

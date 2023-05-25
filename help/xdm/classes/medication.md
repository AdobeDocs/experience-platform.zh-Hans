---
title: 药物类别
description: 本文档概述了Experience Data Model (XDM)中的“药物”类。
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 3%

---

# [!UICONTROL 药物] 类

在Experience Data Model (XDM)中， [!UICONTROL 药物] 类捕获定义用于医疗的物质（尤其是药物或药物）的最小属性集。

![类结构](../images/classes/medication.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_id` | [!UICONTROL 字符串] | 系统为记录生成的唯一字符串标识符。 此字段用于跟踪单个记录的唯一性，防止数据重复，并在下游服务中查找该记录。<br><br>由于此字段是系统生成的，因此不会在数据引入期间向其提供显式值。 但是，如果您愿意，仍然可以选择提供自己的唯一ID值。 |
| `medicationId` | [!UICONTROL 字符串] | 药物的唯一标识符。 |
| `medicationName` | [!UICONTROL 字符串] | 药物的名称。 |

{style="table-layout:auto"}

可以使用扩展类 [[!UICONTROL 医疗保健] 字段组](../field-groups/medication/healthcare-medication.md) 描述药物或药物的进一步细节。

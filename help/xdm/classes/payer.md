---
title: 付款人类别
description: 了解体验数据模型(XDM)中的Payer类。
exl-id: 8d3e0a6d-41eb-4ffe-81dd-c7b7d532a531
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 5%

---

# [!UICONTROL 付款人] 类

在Experience Data Model (XDM)中， [!UICONTROL 付款人] 类捕获定义付款人业务实体的最小资产集，该实体收集与保险公司（例如健康保险）相关的数据。

![类结构](../images/classes/payer.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_id` | [!UICONTROL 字符串] | 系统为记录生成的唯一字符串标识符。 此字段用于跟踪单个记录的唯一性，防止数据重复，并在下游服务中查找该记录。<br><br>由于此字段是系统生成的，因此在数据摄取期间不会向其提供显式值。 但是，如果您愿意，仍然可以选择提供自己的唯一ID值。 |
| `payerId` | [!UICONTROL 字符串] | 付款人的唯一标识符。 |
| `payerName` | [!UICONTROL 字符串] | 付款人的名称。 |

{style="table-layout:auto"}

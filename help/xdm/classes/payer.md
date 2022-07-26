---
title: 付款人分类
description: 本文档概述了体验数据模型(XDM)中的付款人类。
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 5%

---

# [!UICONTROL 付款人] 类

在Experience Data Model(XDM)中， [!UICONTROL 付款人] 类可捕获定义付款人业务实体的最小属性集，该业务实体收集与保险公司相关的数据（如健康保险）。

![类结构](../images/classes/payer.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_id` | [!UICONTROL 字符串] | 记录的唯一、系统生成的字符串标识符。 此字段用于跟踪单个记录的唯一性，防止重复数据，并在下游服务中查找该记录。<br><br>由于此字段是系统生成的，因此在数据摄取期间不会为其提供显式值。 但是，如果您愿意，您仍可以选择提供您自己的唯一ID值。 |
| `payerId` | [!UICONTROL 字符串] | 付款人的唯一标识符。 |
| `payerName` | [!UICONTROL 字符串] | 付款人的名称。 |

{style=&quot;table-layout:auto&quot;}

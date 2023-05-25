---
title: 付款人类别
description: 本文档概述了Experience Data Model (XDM)中的Payer类。
exl-id: 8d3e0a6d-41eb-4ffe-81dd-c7b7d532a531
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 3%

---

# [!UICONTROL 付款人] 类

在Experience Data Model (XDM)中， [!UICONTROL 付款人] class捕获定义付款人业务实体的最低属性集，该实体收集与保险公司（如健康保险）相关的数据。

![类结构](../images/classes/payer.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `_id` | [!UICONTROL 字符串] | 系统为记录生成的唯一字符串标识符。 此字段用于跟踪单个记录的唯一性，防止数据重复，并在下游服务中查找该记录。<br><br>由于此字段是系统生成的，因此不会在数据引入期间向其提供显式值。 但是，如果您愿意，仍然可以选择提供自己的唯一ID值。 |
| `payerId` | [!UICONTROL 字符串] | 付款人的唯一标识符。 |
| `payerName` | [!UICONTROL 字符串] | 付款人的名称。 |

{style="table-layout:auto"}

---
title: 错误详细信息集合数据类型
description: 了解错误详细信息收集Experience Data Model (XDM)数据类型。
source-git-commit: 899c656a7295896b291ac5c80df873711bc6f149
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 8%

---

# [!UICONTROL 错误详细信息] 收藏集数据类型

[!UICONTROL 错误详细信息] 收藏集是一种标准体验数据模型(XDM)数据类型，用于描述错误详细信息。 使用 [!UICONTROL 错误详细信息] 用于捕获错误源和标识的详细信息的集合数据类型。 错误ID标识错误，并且错误源指定它来自播放器还是外部源。

![错误详细信息数据类型的图表。](../images/data-types/error-details-collection.png)

| 显示名称 | 属性 | 数据类型 | 必需 | 描述 |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL 错误Id] | `name` | 字符串 | 否 | 错误ID |
| [!UICONTROL 错误源] | `source` | 字符串 | 否 | 错误源。 已枚举：“player”、“external”以及各自的含义。 |

{style="table-layout:auto"}

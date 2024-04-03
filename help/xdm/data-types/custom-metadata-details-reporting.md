---
title: 自定义元数据详细信息报表数据类型
description: 了解自定义元数据详细信息报表体验数据模型(XDM)数据类型。
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 4%

---

# [!UICONTROL 自定义元数据详细信息] 报表数据类型

[!UICONTROL 自定义元数据详细信息] 报表是一种标准的体验数据模型(XDM)数据类型，它定义了用于存储自定义元数据的结构。 此 [!UICONTROL 自定义元数据详细信息] 报表数据类型会捕获详细信息，例如与内容或交互关联的自定义元数据的名称和值。 媒体报告字段由Adobe服务用于分析用户发送的媒体收集字段。 此数据以及其他特定用户量度一起进行计算和报告。

![自定义元数据详细信息报表数据类型的图表。](../images/data-types/the-custom-metadata-reporting.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL 自定义元数据字段名称] | `name` | 字符串 | 自定义字段的名称。 |
| [!UICONTROL 自定义元数据字段值] | `value` | 字符串 | 自定义字段的值。 |

{style="table-layout:auto"}

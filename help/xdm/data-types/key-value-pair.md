---
title: 键值对数据类型
description: 本文档概述了键值对体验数据模型(XDM)数据类型。
source-git-commit: bf815eb014dc87f74ba3d42478eadcb1e8144c3c
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 5%

---

# [!UICONTROL 键值对] 数据类型

[!UICONTROL 键值对] 是一种标准的体验数据模型(XDM)数据类型，可捕获通用键值对的详细信息。 此数据类型用在 [[!UICONTROL Adobe Analytics ExperienceEvent完整扩展] 字段组](../field-groups/event/analytics-full-extension.md) 用于描述列表变量的数组项。

![键值对结构](../images/data-types/key-value-pair.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `key` | 字符串 | 通用变量或值的键（名称）。 |
| `value` | 字符串 | 变量的值。 |

{style=&quot;table-layout:auto&quot;}

有关数据类型的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).

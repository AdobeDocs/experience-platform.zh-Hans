---
title: 键值对数据类型
description: 了解键值对体验数据模型(XDM)数据类型。
exl-id: 2a1a7537-9019-4cf2-bfa1-9c760f9656dd
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 5%

---

# [!UICONTROL 键值对] 数据类型

[!UICONTROL 键值对] 是一个标准的体验数据模型(XDM)数据类型，可捕获通用键值对的详细信息。 此数据类型用于 [[!UICONTROL Adobe Analytics ExperienceEvent完整扩展] 字段组](../field-groups/event/analytics-full-extension.md) 用于描述列表变量的数组项。

![键值对结构](../images/data-types/key-value-pair.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `key` | 字符串 | 通用变量或值的键（名称）。 |
| `value` | 字符串 | 变量的值。 |

{style="table-layout:auto"}

有关数据类型的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/keyvalue.schema.json).

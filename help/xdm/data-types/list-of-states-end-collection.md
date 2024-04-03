---
title: 状态列表结束收集数据类型
description: 了解状态列表最终收集数据类型Experience Data Model (XDM)数据类型。
source-git-commit: e9107092b60361216744e154752f48546b5bad73
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---

# [!UICONTROL 状态列表结束] 数据类型

状态列表结束收集数据类型数据类型是体验数据模型(XDM)数据类型，旨在表示与各种播放器属性的结束状态相关的信息。 它包括 [!UICONTROL 播放器状态名称] 属性，用于指示特定的属性状态（例如，“fullscreen”、“mute”、“closedCaptioning”）。 此数据类型用于捕获和描述不同播放器状态的初始条件。

![状态列表结束集合数据类型的图表。](../images/data-types/list-of-states-end-collection.png)

| 显示名称 | 属性 | 数据类型 | 必需 | 描述 |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL 播放器状态名称] | `name` | 字符串 | 否 | 播放器状态的名称。 已枚举：“fullscreen”、“mute”、“closedCaptioning”、“pictureInPicture”、“inFocus”以及各自的含义。 |

{style="table-layout:auto"}

---
title: 状态列表结束收集数据类型
description: 了解状态列表最终收集数据类型Experience Data Model (XDM)数据类型。
exl-id: e59d12e0-2f18-4637-8a51-41b7b5b59b57
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 6%

---

# [!UICONTROL 状态列表End]数据类型

状态列表结束收集数据类型数据类型是体验数据模型(XDM)数据类型，旨在表示与各种播放器属性的结束状态相关的信息。 它包括[!UICONTROL 播放器状态名称]属性，这些属性指示特定的属性状态（例如，“fullscreen”、“mute”、“closedCaptioning”）。 此数据类型用于捕获和描述不同播放器状态的初始条件。

![状态列表结束集合数据类型的图表。](../images/data-types/list-of-states-end-collection.png)

| 显示名称 | 属性 | 数据类型 | 必需 | 描述 |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL 播放器状态名称] | `name` | 字符串 | 否 | 播放器状态的名称。 已枚举：“fullscreen”、“mute”、“closedCaptioning”、“pictureInPicture”、“inFocus”以及各自的含义。 |

{style="table-layout:auto"}

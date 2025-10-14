---
title: 状态列表开始收集数据类型
description: 了解状态列表开始数据类型Experience Data Model (XDM)数据类型。
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---

# [!UICONTROL 状态列表开始]数据类型

[!UICONTROL 状态列表开始]数据类型是体验数据模型(XDM)数据类型，旨在表示与各种播放器属性的开始状态相关的信息。 它包括[!UICONTROL 播放器状态名称]属性，这些属性指示特定的属性状态（例如，“fullscreen”、“mute”、“closedCaptioning”）。 此数据类型用于捕获和描述不同播放器状态的初始条件。

![&#x200B; [!UICONTROL 状态列表开始]数据类型的图表。](../images/data-types/list-of-states-start-collection.png)

| 显示名称 | 属性 | 数据类型 | 必需 | 描述 |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL 播放器状态名称] | `name` | 字符串 | 否 | 播放器状态的名称。 已枚举：“fullscreen”、“mute”、“closedCaptioning”、“pictureInPicture”、“inFocus”以及各自的含义。 |

{style="table-layout:auto"}

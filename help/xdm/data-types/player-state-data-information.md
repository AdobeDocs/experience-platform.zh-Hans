---
title: 播放器状态数据信息数据类型
description: 了解播放器状态数据信息体验数据模型(XDM)数据类型。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 4%

---

# [!UICONTROL 播放器状态信息] 数据类型

[!UICONTROL 播放器状态信息] 是一种标准的体验数据模型(XDM)数据类型，用于描述媒体播放器中的各种状态及其发生次数。 使用 [!UICONTROL 播放器状态信息] 用于捕获不同播放器状态（如全屏、静音、隐藏式字幕、画中画和聚焦状态）的数据类型。 对于每个状态，它记录是否设置了状态、发生次数以及媒体播放期间保持活动状态的总持续时间。

![播放器状态数据信息数据类型的图表。](../images/data-types/player-state-data-information.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|-------------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL 播放器状态名称] | `name` | 字符串 | 播放器状态的名称。 已枚举：“fullscreen”、“mute”、“closedCaptioning”、“pictureInPicture”、“inFocus”以及各自的含义。 |
| [!UICONTROL 播放器状态设置] | `isSet` | 布尔 | 是否将播放器状态设置为该状态。 |
| [!UICONTROL 播放器状态计数] | `count` | 整数 | 在流上设置播放器状态的次数。 |
| [!UICONTROL 播放器状态时间] | `time` | 整数 | 该播放器状态的总持续时间。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json)

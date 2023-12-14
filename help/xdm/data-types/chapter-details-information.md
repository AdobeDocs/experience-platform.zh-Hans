---
title: 章节详细信息数据类型
description: 了解章节详细信息体验数据模型(XDM)数据类型。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 6%

---

# [!UICONTROL 章节详细信息] 数据类型

[!UICONTROL 章节详细信息] 是一个标准的体验数据模型(XDM)数据类型，它描述了与媒体内容中的章节或区段相关的各种属性。 使用 [!UICONTROL 章节详细信息] 用于捕获详细信息(如章节名称、持续时间、位置、ID、播放状态（已开始/已完成）以及每个章节逗留的时间等)的数据类型。

![章节详细信息数据类型的图表。](../images/data-types/chapter-details-information.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|---------------------------|---------------|-----------|---------------------------------------------------|
| [!UICONTROL 章节名称] | `friendlyName` | 字符串 | 章节和/或区段的名称。 |
| [!UICONTROL 章节长度或持续时间] | `length` | 整数 | **必填** 章节的长度，以秒为单位。 |
| [!UICONTROL 章节偏移] | `offset` | 整数 | **必填** 内容中章节从开始起的偏移（以秒为单位）。 |
| [!UICONTROL 章节位置] | `index` | 整数 | **必填** 章节在内容中的位置（索引、整数）。 |
| [!UICONTROL 章节Id] | `ID` | 字符串 | 自动生成的章节ID。 |
| [!UICONTROL 章节开始] | `isStarted` | 布尔 | 章节是否已开始。 |
| [!UICONTROL 章节已完成] | `isCompleted` | 布尔 | 章节是否已完成。 |
| [!UICONTROL 章节播放时间] | `timePlayed` | 整数 | 章节花费的时间，以秒为单位。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/chapterdetails.schema.json)

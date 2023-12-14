---
title: 媒体事件信息数据类型
description: 了解媒体事件信息体验数据模型(XDM)数据类型。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 6%

---

# [!UICONTROL 媒体事件信息] 数据类型

[!UICONTROL 媒体事件信息] 是一个标准的体验数据模型(XDM)数据类型，它描述了与体验事件相关的媒体详细信息。

![媒体事件信息数据类型的图表。](../images/data-types/media-event-information.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `mediaCollection` | [[!UICONTROL mediaDetails]](./media-details-information.md) | 与体验事件相关的媒体详细信息。 |
| `mediaEventTimestamp` | [!UICONTROL 字符串] | 发生媒体事件的时间。 |
| `mediaEventType` | [!UICONTROL 字符串] | 媒体事件类型。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)

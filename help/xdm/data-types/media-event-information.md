---
title: 媒体事件信息数据类型
description: 了解媒体事件信息体验数据模型(XDM)数据类型。
exl-id: 91bb7f28-b629-4044-b687-768c545ac8a2
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 5%

---

# [!UICONTROL 媒体事件信息] 数据类型

[!UICONTROL 媒体事件信息] 是一个标准的体验数据模型(XDM)数据类型，它描述了与体验事件相关的媒体详细信息。

![媒体事件信息数据类型的图表。](../images/data-types/media-event-information.png)

| 属性 | 数据类型 | 描述 |
| --- | --- | --- |
| `mediaCollection` | [!UICONTROL mediaDetails] | 与体验事件相关的媒体详细信息。 此数据类型同时用于 [媒体数据收集](./media-collection-details.md) 和 [媒体数据报告](./media-reporting-details.md). |
| `mediaEventTimestamp` | [!UICONTROL 字符串] | 发生媒体事件的时间。 |
| `mediaEventType` | [!UICONTROL 字符串] | 媒体事件类型。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/mediaevent.schema.json)

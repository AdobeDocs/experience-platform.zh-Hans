---
title: MediaAnalytics交互详细信息架构字段组
description: 了解MediaAnalytics交互详细信息架构字段组。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 2%

---

# [!UICONTROL MediaAnalytics交互详细信息] 架构字段组

[!UICONTROL MediaAnalytics交互详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 使用此字段组可捕获扩充的数据字段，这些字段可全面监测和分析跨各种平台或渠道与媒体内容的交互。

![的架构图 [!UICONTROL MediaAnalytics交互详细信息] 架构字段组。](../../images/field-groups/mediaanalytics-interaction.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|---| --- | --- | --- |
| [!UICONTROL 媒体收集详细信息] | `mediaCollection` | [[!UICONTROL 媒体详细信息]](../../data-types/media-details-information.md) | 与媒体项目集合相关的属性。 |
| [!UICONTROL 媒体报告详细信息] | `mediaReporting` | [[!UICONTROL 媒体详细信息]](../../data-types/media-details-information.md) | 与媒体内容关联的报表详细信息和量度。 |
| [!UICONTROL 媒体收藏下载的内容事件列表] | `mediaDownloadedEvents` | [!UICONTROL 数组] 之 [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | 跟踪媒体收藏集中内容的下载的事件。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json)

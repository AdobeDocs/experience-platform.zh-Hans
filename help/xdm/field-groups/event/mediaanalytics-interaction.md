---
title: MediaAnalytics交互详细信息架构字段组
description: 了解MediaAnalytics交互详细信息架构字段组。
exl-id: 1096d28a-5796-49cc-bd45-b3f5188f699e
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# [!UICONTROL MediaAnalytics交互详细信息] 架构字段组

[!UICONTROL MediaAnalytics交互详细信息] 是的标准架构字段组 [[!DNL XDM ExperienceEvent] 类](../../classes/experienceevent.md). 使用此字段组可捕获扩充的数据字段，这些字段可全面监测和分析跨各种平台或渠道与媒体内容的交互。

![的架构图 [!UICONTROL MediaAnalytics交互详细信息] 架构字段组。](../../images/field-groups/mediaanalytics-interaction.png)

| 显示名称 | 属性 | 数据类型 | 描述 |
|---| --- | --- | --- |
| [!UICONTROL 媒体收集详细信息] | `mediaCollection` | [[!UICONTROL 媒体收集详细信息]](../../data-types/media-collection-details.md) | 与媒体项目集合相关的属性。 使用媒体收集字段捕获数据，并将其发送到其他Adobe服务以供进一步处理。 |
| [!UICONTROL 媒体报告详细信息] | `mediaReporting` | [[!UICONTROL 媒体报告详细信息]](../../data-types/media-reporting-details.md) | 与媒体内容关联的报表详细信息和量度。 * Adobe服务使用媒体报告字段来分析用户发送的媒体收集字段。 此数据以及其他特定用户量度一起进行计算和报告。 |
| [!UICONTROL 媒体收藏下载的内容事件列表] | `mediaDownloadedEvents` | [!UICONTROL 数组] 之 [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | 跟踪媒体收藏集中内容的下载的事件。 |

{style="table-layout:auto"}

>[!TIP]
>
>您可以隐藏Media Edge API未使用的字段。 隐藏这些字段使架构更易于阅读和理解，但并非必需。 这些字段仅指以下内容： [!UICONTROL MediaAnalytics交互详细信息] 字段组。 要提高Platform UI的可读性，请按照 [Media Analytics有关如何隐藏未使用字段的文档](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform).

<!-- 
>[!NOTE]
>
>Schemas contain fields that are not used in every context or situation. They provide a potential blueprint to map an object. Schemas displayed for the Media Edge API Collection or Reporting data types only portray the relevant fields. You can manually select and deselect the fields that you want to use if you intend to use a schema for the Media Edge API interaction. You can find instructions on [hiding unnecessary fields](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform) in the guide to install Media Analytics with Experience Platform Edge.
 -->

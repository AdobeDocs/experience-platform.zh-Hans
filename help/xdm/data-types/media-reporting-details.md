---
title: 媒体报告详细信息数据类型
description: 了解Media Reporting Details Experience Data Model (XDM)数据类型。
exl-id: e8bf20a9-9ac0-4339-8200-5d6d9328ce3b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---

# [!UICONTROL 媒体报告详细信息]数据类型

>[!NOTE]
>
>媒体收集字段会捕获数据并将其发送到其他Adobe服务以供进一步处理。 Adobe服务使用媒体报告字段来分析用户发送的媒体收集字段。 此数据以及其他特定用户量度一起进行计算和报告。

[!UICONTROL 媒体报告详细信息]是一个标准体验数据模型(XDM)数据类型，可捕获有关媒体播放事件的重要详细信息。 使用[!UICONTROL 媒体报告详细信息]数据类型捕获详细信息，如内容中的播放头位置、唯一的会话标识符以及与会话相关的各种嵌套属性等。 此数据类型提供了播放体验的全面概述，从而能够跟踪和分析播放会话期间的媒体使用模式和相关事件。

>[!NOTE]
>
>以下提及的字段不直接用于创建请求。 实际上，发送到Adobe Experience Platform或Adobe Analytics的字段集是根据您的请求数据组合在一起的，然后，服务器基础架构会合并或处理这些量度。 在Experience Platform收集各种类型的用户事件时，返回给您的报告将侧重于特定事件，如`media.sessionStart`、`media.adStart`和`media.sessionComplete`。 这意味着，虽然您在收集期间传输了12种类型的事件，但您的报表将仅呈现基于下面列出的五个事件的细分。

+++选择以显示[!UICONTROL 媒体报告详细信息]数据类型的图表。
![ [!UICONTROL 媒体报告详细信息]数据类型的图表。](../images/data-types/media-reporting-details.png)
+++

| 显示名称 | 属性 | 数据类型 | 描述 |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Advertising详细信息] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-reporting.md) | Advertising详细信息是指与体验活动期间广告活动相关的特定信息。 这包括广告元数据、定位详细信息和性能量度。 |
| [!UICONTROL Advertising Pod详细信息] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-reporting.md) | Advertising Pod详细信息包含与体验事件中的Ad Pod相关的信息。 它提供了有关广告序列、内容和参与量度的见解。 |
| [!UICONTROL 章节详细信息] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-reporting.md) | 章节详细信息可捕获与内容的章节或分段部分相关的数据。 它提供有关章节标记、时间轴和相关元数据的信息。 |
| [!UICONTROL 状态列表] | `states` | [[!UICONTROL playerStateData]](./player-state-data-reporting.md) | States属性是一个数组，用于在体验事件中捕获各种状态。 此属性提供有关播放、用户操作或内容更改的顺序数据。 |
| [!UICONTROL Qoe数据详细信息] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-reporting.md) | QoE（体验质量）数据详细信息捕获与性能相关的量度和用户体验数据。 它提供了对质量、响应性和用户交互情况的洞察。 |
| [!UICONTROL 会话详细信息] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-reporting.md) | 会话详细信息包括与体验事件关联的全面信息，提供关于用户交互、持续时间的洞察以及与播放会话相关的上下文数据。 |
| [!UICONTROL 自定义元数据] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-reporting.md) | 自定义元数据包含用户定义的元数据或与体验事件关联的其他元数据。 此元数据允许在事件上下文中包含个性化或特定数据。 |
| [!UICONTROL 播放头] | `playhead` | 整数 | 播放头表示媒体内容中的当前播放位置。 对于实时内容，它表示一天中的当前秒数(0 &lt;=播放头&lt; 86400)。 对于录制的内容，它反映内容时长的当前秒数（0 &lt;=播放头&lt;内容长度）。 |

{style="table-layout:auto"}

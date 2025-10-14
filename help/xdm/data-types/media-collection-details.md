---
title: 媒体收集详细信息数据类型
description: 了解媒体收集详细信息体验数据模型(XDM)数据类型。
exl-id: 1faf60f7-6afb-4ce2-b50d-967776a57715
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# [!UICONTROL 媒体收集详细信息]数据类型

[!UICONTROL 媒体收集详细信息]是一种标准的体验数据模型(XDM)数据类型，可捕获有关媒体播放事件的重要详细信息。 使用[!UICONTROL 媒体收集详细信息]数据类型捕获详细信息，如内容中的播放头位置、唯一的会话标识符以及与会话相关的各种嵌套属性等。 此数据类型提供了播放体验的全面概述，从而能够跟踪和分析播放会话期间的媒体使用模式和相关事件。

>[!NOTE]
>
>媒体收集字段会捕获数据并将其发送到其他Adobe服务以供进一步处理。 Adobe服务使用媒体报告字段来分析用户发送的媒体收集字段。 此数据以及其他特定用户量度一起进行计算和报告。

+++选择以显示[!UICONTROL 媒体收集详细信息]数据类型的图表。
![&#x200B; [!UICONTROL 媒体收集详细信息]数据类型的图表。](../images/data-types/media-collection-details.png)
+++

| 显示名称 | 属性 | 以下项所需的事件 | 数据类型 | 描述 |
| ------------------------------------ | ----------------------- | ---------------------------------------------------------- | --------- | ----------- |
| [!UICONTROL Advertising详细信息] | `advertisingDetails` | `adStart` | [[!UICONTROL advertisingDetails] — 集合](./advertising-details-collection.md) | Advertising详细信息是指与体验活动期间广告活动相关的特定信息。 这包括广告元数据、定位详细信息和性能量度。 |
| [!UICONTROL Advertising Pod详细信息] | `advertisingPodDetails` | `adBreakStart` | [[!UICONTROL advertisingPodDetails] — 收藏集](./advertising-pod-details-collection.md) | Advertising Pod详细信息包含与体验事件中的Ad Pod相关的信息。 它提供了有关广告序列、内容和参与量度的见解。 |
| [!UICONTROL 章节详细信息] | `chapterDetails` | `chapterStart` | [[!UICONTROL chapterDetails] — 集合](./chapter-details-collection.md) | 章节详细信息可捕获与内容的章节或分段部分相关的数据。 它提供有关章节标记、时间轴和相关元数据的信息。 |
| [!UICONTROL 错误详细信息] | `errorDetails` | `error` | [[!UICONTROL errorDetails] — 集合](./error-details-collection.md) | 错误详细信息包含与在体验事件期间遇到的错误有关的信息。 这包括错误代码、描述、时间戳和相关上下文数据。 |
| [!UICONTROL 状态列表结束] | `statesEnd` | 在`statesUpdate`中使用 | [[!UICONTROL statesEnd] — 集合](./list-of-states-end-collection.md) | 状态End提供了一个数组，用于列出体验事件结束时的状态。 它包含有关最终播放状态或内容状态的详细信息。 |
| [!UICONTROL 状态列表开始] | `statesStart` | 在`statesUpdate`中使用 | [[!UICONTROL statesStart] — 集合](./list-of-states-start-collection.md) | 状态开始提供了一个数组，用于列出体验事件开始时的状态。 它提供与播放、用户操作或内容细节相关的数据。 |
| [!UICONTROL Qoe数据详细信息] | `qoeDataDetails` | 所有选项均可选 | [[!UICONTROL qoeDataDetails] — 集合](./qoe-data-details-collection.md) | QoE（体验质量）数据详细信息捕获与性能相关的量度和用户体验数据。 它提供了对质量、响应性和用户交互情况的洞察。 |
| [!UICONTROL 会话详细信息] | `sessionDetails` | `sessionStart` | [[!UICONTROL sessionDetails] — 集合](./session-details-collection.md) | 会话详细信息包括与体验事件关联的全面信息，提供关于用户交互、持续时间的洞察以及与播放会话相关的上下文数据。 |
| [!UICONTROL 自定义元数据] | `customMetadata` | 对于`sessionStart`、`adStart`、`sessionStart`是可选的 | [[!UICONTROL customMetadataDetails] — 集合](./custom-metadata-details-collection.md) | 自定义元数据包含用户定义的元数据或与体验事件关联的其他元数据。 此元数据允许在事件上下文中包含个性化或特定数据。 |
| [!UICONTROL 媒体会话ID] | `sessionID` | 除&#x200B;**`sessionStart`之外的所有事件**&#x200B;和下载的内容。 | 字符串 | 媒体会话ID在单个播放会话期间唯一标识内容流的实例。 它用作用于跟踪和管理与用户或查看者相关联的特定播放体验的独特标识符。<br><em>注意：<em>`sessionId`针对除`sessionStart`之外的所有事件和所有下载的事件发送。 |
| [!UICONTROL 播放头] | `playhead` | 所有事件 | 整数 | 播放头表示媒体内容中的当前播放位置。 对于实时内容，它表示一天中的当前秒数(0 &lt;=播放头&lt; 86400)。 对于录制的内容，它反映内容时长的当前秒数（0 &lt;=播放头&lt;内容长度）。 |

{style="table-layout:auto"}

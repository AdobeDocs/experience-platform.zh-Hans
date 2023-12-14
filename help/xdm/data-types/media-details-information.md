---
title: 媒体详细信息数据类型
description: 了解媒体详细信息体验数据模型(XDM)数据类型。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---

# [!UICONTROL 媒体详细信息] 数据类型

[!UICONTROL 媒体详细信息] 是一个标准的体验数据模型(XDM)数据类型，可捕获有关媒体播放事件的重要详细信息。 使用 [!UICONTROL 媒体详细信息] 用于捕获详细信息（例如内容中的播放头位置、唯一的会话标识符以及与会话相关的各种嵌套属性等）的数据类型。 此数据类型提供了播放体验的全面概述，从而能够跟踪和分析播放会话期间的媒体使用模式和相关事件。

+++选择以显示 [!UICONTROL 媒体详细信息] 数据类型。
![的图表 [!UICONTROL 媒体详细信息] 数据类型。](../images/data-types/media-details-information.png)
+++

| 显示名称 | 属性 | 数据类型 | 描述 |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL 播放头] | `playhead` | 整数 | 播放头表示媒体内容中的当前播放位置。 对于实时内容，它表示一天中的当前秒数(0 &lt;=播放头&lt; 86400)。 对于录制的内容，它反映内容时长的当前秒数（0 &lt;=播放头&lt;内容长度）。 |
| [!UICONTROL 媒体会话ID] | `sessionID` | 字符串 | 媒体会话ID在单个播放会话期间唯一标识内容流的实例。 它用作用于跟踪和管理与用户或查看者相关联的特定播放体验的独特标识符。 |
| [!UICONTROL 会话详细信息] | `sessionDetails` | [[!UICONTROL sessiondetails]](./session-details-information.md) | 会话详细信息包括与体验事件关联的全面信息，提供关于用户交互、持续时间的洞察以及与播放会话相关的上下文数据。 |
| [!UICONTROL 广告详细信息] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-information.md) | 广告详细信息指体验事件中与广告活动相关的特定信息。 这包括广告元数据、定位详细信息和性能量度。 |
| [!UICONTROL Advertising Pod详细信息] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-information.md) | 广告Pod详细信息包含与体验事件中的Ad Pod相关的信息。 它提供了有关广告序列、内容和参与量度的见解。 |
| [!UICONTROL 章节详细信息] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-information.md) | 章节详细信息可捕获与内容的章节或分段部分相关的数据。 它提供有关章节标记、时间轴和相关元数据的信息。 |
| [!UICONTROL 错误详细信息] | `errorDetails` | [[!UICONTROL errorDetails]](./error-details-information.md) | 错误详细信息包含与在体验事件期间遇到的错误有关的信息。 这包括错误代码、描述、时间戳和相关上下文数据。 |
| [!UICONTROL Qoe数据详细信息] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-information.md) | QoE（体验质量）数据详细信息捕获与性能相关的量度和用户体验数据。 它提供了对质量、响应性和用户交互情况的洞察。 |
| [!UICONTROL 状态列表开始] | `statesStart` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | 状态开始提供了一个数组，用于列出体验事件开始时的状态。 它提供与播放、用户操作或内容细节相关的数据。 |
| [!UICONTROL 状态列表结束] | `statesEnd` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | 状态End提供了一个数组，用于列出体验事件结束时的状态。 它包含有关最终播放状态或内容状态的详细信息。 |
| [!UICONTROL 状态列表] | `states` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | States属性是一个数组，用于在体验事件中捕获各种状态。 此属性提供有关播放、用户操作或内容更改的顺序数据。 |
| [!UICONTROL 自定义元数据] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-information.md) | 自定义元数据包含用户定义的元数据或与体验事件关联的其他元数据。 此元数据允许在事件上下文中包含个性化或特定数据。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json)

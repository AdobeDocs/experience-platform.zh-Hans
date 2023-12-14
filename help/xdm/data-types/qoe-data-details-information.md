---
title: QoE（体验质量）数据详细信息信息数据类型
description: 了解QoE（体验质量）数据详细信息数据类型体验数据模型(XDM)数据类型。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 5%

---

# QoE（体验质量）数据详细信息信息数据类型

[!UICONTROL QoE数据详细信息] 是一个标准体验数据模型(XDM)数据类型，它提供了与媒体播放期间的体验质量(QoE)相关的详细量度。 使用 [!UICONTROL QoE数据详细信息] 数据类型，用于捕获比特率信息、帧率、缓冲事件、丢帧等详细信息。 此数据类型支持播放质量分析，从而可以深入了解流性能、用户体验以及播放会话期间遇到的潜在问题。

+++选择以显示QoE数据详细信息数据类型。
![QoE（体验质量）数据详细信息数据类型的图表。](../images/data-types/qoe-data-details-information.png)
+++

| 显示名称 | 属性 | 数据类型 | 描述 |
|----------------------------------------|----------------------------|-----------|--------------------------------------------------------------------------------------------------|
| [!UICONTROL 平均比特率存储桶] | `bitrateAverageBucket` | 字符串 | 在100kbps间隔的预定义存储桶中分类的平均比特率（以kbps为单位）。 |
| [!UICONTROL 比特率] | `bitrate` | 整数 | 比特率值（以kbps为单位）。 |
| [!UICONTROL 平均比特率] | `bitrateAverage` | 数字 | 平均比特率（以kbps为单位，整数）。 计算为比特率值的加权平均值。 |
| [!UICONTROL 受比特率更改影响的流] | `hasBitrateChangeImpactedStreams` | 布尔 | 指示在播放期间流是否受比特率更改的影响。 |
| [!UICONTROL 比特率更改] | `bitrateChangeCount` | 整数 | 播放期间比特率更改的总数。 |
| [!UICONTROL 受丢帧影响的流] | `hasDroppedFrameImpactedStreams` | 布尔 | 指示流在播放期间是否受到丢帧的影响。 |
| [!UICONTROL 丢帧] | `droppedFrames` | 整数 | 播放期间丢帧的总数。 |
| [!UICONTROL 开始前丢帧] | `isDroppedBeforeStart` | 布尔 | 指示用户在视频开始之前是否退出视频（无论是否有广告）。 |
| [!UICONTROL 每秒帧数] | `framesPerSecond` | 整数 | 当前流帧速率（以每秒帧数为单位）。 |
| [!UICONTROL 开始时间] | `timeToStart` | 整数 | 视频加载与开始之间的持续时间（以秒为单位）。 |
| [!UICONTROL 受缓冲影响的流] | `hasBufferImpactedStreams` | 布尔 | 指示流在播放期间是否受缓冲影响。 |
| [!UICONTROL 缓冲事件] | `bufferCount` | 整数 | 播放期间不同缓冲状态的计数。 |
| [!UICONTROL 缓冲总持续时间] | `bufferTime` | 整数 | 播放期间缓冲所花费的总时间（以秒为单位）。 |
| [!UICONTROL 受错误影响的流] | `hasErrorImpactedStreams` | 布尔 | 指示流在播放期间是否遇到错误。 |
| [!UICONTROL 错误] | `errorCount` | 整数 | 播放期间发生的错误总数。 |
| [!UICONTROL 受停滞影响的流] | `hasStallImpactedStreams` | 布尔 | 指示流在播放期间是否遇到停滞。 |
| [!UICONTROL 停滞事件] | `stallCount` | 整数 | 播放期间的停滞事件计数。 |
| [!UICONTROL 总停滞持续时间] | `stallTime` | 整数 | 播放期间播放停止的总时间（以秒为单位）。 |
| [!UICONTROL 播放器SDK错误ID] | `playerSdkErrors` | 字符串数组 | 播放器SDK在播放期间生成的唯一错误ID。 |
| [!UICONTROL 外部错误ID] | `externalErrors` | 字符串数组 | 来自外部源的唯一错误ID，例如CDN错误。 |
| [!UICONTROL 媒体SDK错误ID] | `mediaSdkErrors` | 字符串数组 | Media SDK在播放期间生成的唯一错误ID。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json).


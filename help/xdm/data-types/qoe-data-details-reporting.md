---
title: QoE（体验质量）数据详细信息报表数据类型
description: 了解QoE（体验质量）数据详细信息报表数据类型体验数据模型(XDM)数据类型。
exl-id: 608baa9b-12ca-466c-a962-1401abc0344e
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 4%

---

# QoE（体验质量）数据详细信息报表数据类型

[!UICONTROL QoE数据详细信息]报告是一种标准的体验数据模型(XDM)数据类型，它提供了与媒体播放期间的体验质量(QoE)相关的详细量度。 使用[!UICONTROL QoE数据详细信息]报表数据类型捕获比特率信息、帧率、缓冲事件、丢帧等详细信息。 媒体报告字段由Adobe服务用于分析用户发送的媒体收集字段。 此数据以及其他特定用户量度一起进行计算和报告。 此数据类型支持播放质量分析，从而可以深入了解流性能、用户体验以及播放会话期间遇到的潜在问题。

+++选择以显示QoE数据详细信息报表数据类型。
![QoE（体验质量）数据详细信息报表数据类型的图表。](../images/data-types/qoe-data-details-reporting.png)
+++

>[!NOTE]
>
>每个显示名称都包含一个链接，指向有关其音频和视频参数的更多信息。 链接的页面包含有关Adobe收集的视频广告数据、实现值、网络参数、报表和重要注意事项的详细信息。

| 显示名称 | 属性 | 数据类型 | 描述 |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|---------------------------------------------------------------------------------------------------|
| [[!UICONTROL 平均比特率]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#average-bitrate-1) | `bitrateAverage` | 数字 | 平均比特率（以kbps为单位，整数）。 计算为比特率值的加权平均值。 |
| [[!UICONTROL 平均比特率存储桶]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#average-bitrate) | `bitrateAverageBucket` | 字符串 | 在100kbps间隔的预定义存储桶中分类的平均比特率（以kbps为单位）。 |
| [[!UICONTROL 比特率]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#average-bitrate) | `bitrate` | 整数 | 比特率值（以kbps为单位）。 |
| [[!UICONTROL 受比特率更改影响的流]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#bitrate-change-impacted-streams) | `hasBitrateChangeImpactedStreams` | 布尔 | 指示在播放期间流是否受比特率更改的影响。 |
| [[!UICONTROL 比特率更改]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#bitrate-changes) | `bitrateChangeCount` | 整数 | 播放期间比特率更改的总数。 |
| [[!UICONTROL 缓冲事件]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#buffer-events) | `bufferCount` | 整数 | 播放期间不同缓冲状态的计数。 |
| [[!UICONTROL 受缓冲影响的流]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#buffer-impacted-streams) | `hasBufferImpactedStreams` | 布尔 | 指示流在播放期间是否受缓冲影响。 |
| [[!UICONTROL 受丢帧影响的流]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#dropped-frame-impacted-streams) | `hasDroppedFrameImpactedStreams` | 布尔 | 指示流在播放期间是否受到丢帧的影响。 |
| [[!UICONTROL 丢帧]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#dropped-frames-1) | `droppedFrames` | 整数 | 播放期间丢帧的总数。 |
| [[!UICONTROL 开始前丢帧]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#drops-before-start) | `isDroppedBeforeStart` | 布尔 | 指示用户在视频开始之前是否退出视频（无论是否有广告）。 |
| [[!UICONTROL 错误影响的流]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#error-impacted-streams) | `hasErrorImpactedStreams` | 布尔 | 指示流在播放期间是否遇到错误。 |
| [[!UICONTROL 错误]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#errors-%2F-error-events) | `errorCount` | 整数 | 播放期间发生的错误总数。 |
| [[!UICONTROL 外部错误ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#external-error-ids) | `externalErrors` | 字符串数组 | 来自外部源的唯一错误ID，例如CDN错误。 |
| 每秒[[!UICONTROL 帧数]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#frames-per-second) | `framesPerSecond` | 整数 | 当前流帧速率（以每秒帧数为单位）。 |
| [[!UICONTROL 媒体SDK错误ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#media-sdk-error-ids) | `mediaSdkErrors` | 字符串数组 | Media SDK在播放期间生成的唯一错误ID。 |
| [[!UICONTROL 播放器SDK错误ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#player-sdk-error-ids) | `playerSdkErrors` | 字符串数组 | 播放器SDK在播放期间生成的唯一错误ID。 |
| [[!UICONTROL 停滞事件]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#stalling-events) | `stallCount` | 整数 | 播放期间的停滞事件计数。 |
| [[!UICONTROL 受停滞影响的流]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#stalling-impacted-streams) | `hasStallImpactedStreams` | 布尔 | 指示流在播放期间是否遇到停滞。 |
| [[!UICONTROL 开始时间]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#time-to-start-1) | `timeToStart` | 整数 | 视频加载与开始之间的持续时间（以秒为单位）。 |
| [[!UICONTROL 缓冲总持续时间]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#total-buffer-duration-1) | `bufferTime` | 整数 | 播放期间缓冲所花费的总时间（以秒为单位）。 |
| [[!UICONTROL 总停滞持续时间]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html?lang=zh-Hans#total-stalling-duration) | `stallTime` | 整数 | 播放期间播放停止的总时间（以秒为单位）。 |

{style="table-layout:auto"}

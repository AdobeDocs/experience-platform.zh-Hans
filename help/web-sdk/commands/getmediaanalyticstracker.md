---
title: getMediaAnalyticsTracker
description: 了解如何创建Media Analytics跟踪器对象并使用它跟踪媒体事件。
source-git-commit: 9384c1cc15441199e898d6cc0850e5422253f106
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 3%

---


# `getMediaAnalyticsTracker`

此Web SDK命令可检索Media Analytics跟踪器。 您可以使用此命令创建一个对象实例，然后使用与提供的相同API [Media JS库](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)，跟踪媒体事件。

此 `getMediaAnalyticsTracker` 命令返回旧版Media Analytics API。


| 方法名称 | 描述 | 语法 |
|-----------------|---|----------------|
| `getInstance` | 创建媒体实例以跟踪播放会话。 | `Media.getInstance()` |
| `createMediaObject` | 创建包含媒体信息的对象。 如果传递的参数无效，则返回空对象。 | `Media.createMediaObject(name, id, length, streamType, mediaType)` |
| `createAdBreakObject` | 创建包含广告时间信息的对象。 如果传递的参数无效，则返回空对象。 | `Media.createAdBreakObject(name, position, startTime)` |
| `createAdObject` | 创建包含广告信息的对象。 如果传递的参数无效，则返回空对象。 | `Media.createAdObject(name, id, position, length)` |
| `createChapterObject` | 创建包含章节信息的对象。 如果传递的参数无效，则返回空对象。 | `Media.createChapterObject(name, position, length, startTime)` |
| `createStateObject` | 创建包含状态信息的对象。 如果传递的参数无效，则返回空对象。 | `Media.createStateObject(name)` |
| `createQoEObject` | 创建包含QoE信息的对象。 如果传递的参数无效，则返回空对象。 | `Media.createQoEObject(bitrate, startupTime, fps, droppedFrames)` |

## 实例方法

| 方法名称 | 描述 | 语法 |
|---|---|----|
| `trackSessionStart` | 跟踪开始播放的意图。 这将在媒体跟踪器实例上启动跟踪会话。 | `trackerInstance.trackSessionStart(mediaInfo, contextData)` |
| `trackPlay` | 跟踪上次暂停后的媒体播放或恢复。 | `trackerInstance.trackPlay()` |
| `trackPause` | 跟踪媒体暂停。 | `trackerInstance.trackPause()` |
| `trackComplete` | 跟踪媒体结束。 仅当媒体已完全查看时才调用此方法。 | `trackerInstance.trackComplete()` |
| `trackSessionEnd` | 跟踪查看会话的结束。 即使用户没有查看至媒体结束，也调用此方法。 | `trackerInstance.trackSessionEnd()` |
| `trackError` | 跟踪媒体播放期间发生的错误。 | `trackerInstance.trackError("errorId")` |
| `trackEvent` | 跟踪自定义事件。 | `trackerInstance.trackEvent(event, info, contextData)` |
| `updatePlayhead` | 更新播放头位置。 | `trackerInstance.updatePlayhead(playhead)` |
| `updateQoEObject` | 更新体验质量。 | `trackerInstance.updateQoEObject(qoe)` |

## 常量

| 常量名称 | 描述 | 值 |
|-----------------|--|-----------------|
| `MediaType` | 媒体类型 | `Video`、`Audio` |
| `StreamType` | 流类型 | `VOD`， `Live`， `Linear`， `Podcast`， `Audiobook`， `AOD` |
| `VideoMetadataKeys` | 这会定义视频流的标准元数据键 | `Show`， `Season`， `Episode`， `AssetId`， `Genre`， `FirstAirDate`， `FirstDigitalDate`， `Rating`， `Originator`， `Network`， `ShowType`， `AdLoad`， `MVPD`， `Authorized`， `DayPart`， `Feed`， `StreamFormat` |
| `AudioMetadataKeys` | 这会定义音频流的标准元数据键。 | `Artist`， `Album`， `Label`， `Author`， `Station`， `Publisher` |
| `AdMetadataKeys` | 这会定义广告的标准元数据键。 | `Advertiser`， `CampaignId`， `CreativeId`， `PlacementId`， `SiteId`， `CreativeUrl` |
| `Event` | 这会定义跟踪事件的类型。 | `AdBreakStart`， `AdBreakComplete`， `AdStart`， `AdComplete`， `AdSkip`， `ChapterStart`， `ChapterComplete`， `ChapterSkip`， `SeekStart`， `SeekComplete`， `BufferStart`， `BufferComplete`， `BitrateChange`， `StateStart`， `StateEnd` |
| `PlayerState` | 这将定义用于跟踪播放器状态的标准值。 | `FullScreen`， `ClosedCaption`， `Mute`， `PictureInPicture`， `InFocus` |

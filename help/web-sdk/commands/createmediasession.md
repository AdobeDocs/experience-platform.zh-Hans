---
title: createMediaSession
description: 了解如何配置Web SDK以自动管理媒体会话
source-git-commit: 83d3de67e7680369dc890f58b16d9668058e221c
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 7%

---


# `createMediaSession`

此 `createMediaSession` 命令是Web SDK的一部分 `streamingMedia` 组件。 您可以使用此组件收集与网站上的媒体会话相关的数据。 请参阅 `streamingMedia` [文档](configure/streamingmedia.md) 以了解如何配置此组件。

收集的数据可以包括有关媒体回放、暂停、完成和其他相关事件的信息。 收集后，您可以将此数据发送至 [适用于流媒体的Adobe Analytics](https://experienceleague.adobe.com/zh-hans/docs/media-analytics/using/media-overview)，以聚合量度。 此功能为跟踪和了解您网站上的媒体消费行为提供了全面的解决方案。

您可以通过两种方式在Web SDK中创建媒体会话：

* [自动跟踪的媒体会话](#automatic) 允许Web SDK管理媒体Ping事件向的发送 [适用于流媒体的Adobe Analytics](https://experienceleague.adobe.com/zh-hans/docs/media-analytics/using/media-overview). 这些ping的频率由 [流媒体](configure/streamingmedia.md) 组件。
* [手动跟踪的媒体会话](#manual) 让您能够更好地控制会话ping事件的发送 [适用于流媒体的Adobe Analytics](https://experienceleague.adobe.com/zh-hans/docs/media-analytics/using/media-overview). 此外，您还能够存储 `sessionID` 用于媒体会话。

## 创建自动跟踪的媒体会话 {#automatic}

要自动跟踪媒体会话，请调用 `createMediaSession` 方法，具体选项如下：

```javascript
    alloy("createMediaSession", {
        playerId: "movie-test",
        getPlayerDetails: () => {
            return {
                playhead: document.getElementById("movie-test").currentTime,
                qoeDataDetails: {
                    bitrate: 1000,
                    startupTime: 1000,
                    fps: 30,
                    droppedFrames: 10
                }
            };
        },
        xdm: {
            eventType: "media.sessionStart",
            mediaCollection: {
                sessionDetails: {
                    ...
                }
            }
        }
    });
```

| 属性 | 类型 | 必需 | 描述 |
|---------|----------|---------|---------|
| `playerId` | 字符串 | 是 | 播放器ID，表示媒体会话的唯一标识符。 |
| `getPlayerDetails` | 函数 | 是 | 返回播放器详细信息的函数。 Web SDK将在的每个媒体事件之前调用此回调函数。 `playerId` 已提供。 |
| `xdm.eventType ` | 对象 | 否 | 媒体事件类型。 如果未提供，则会自动将其设置为 `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | 对象 | 是 | 会话详细信息对象。 此 `sessionDetails` 对象应包含会话详细信息属性。 请参阅 [媒体收集架构](../../xdm/data-types/media-collection-details.md) 文档，以了解更多信息。 |


## 创建手动跟踪的媒体会话 {#manual}

要开始手动跟踪媒体会话，请调用 `createMediaSession` 方法，具体选项如下：

```javascript
const sessionPromise = alloy("createMediaSession", {
    xdm: {
        eventType: "media.sessionStart",
        mediaCollection: {
            playhead: 0,
            sessionDetails: {
                ...
            },
            qoeDataDetails: {
                bitrate: 1000,
                startupTime: 1000,
                fps: 30,
                droppedFrames: 10
            }
        }
    }
});
```

| 属性 | 类型 | 已请求 | 描述 |
|---------|----------|---------|---------|
| `xdm.eventType` | 对象 | 否 | 媒体事件类型。 如果未提供，则会自动将其设置为 `media.sessionStart`. |
| `xdm.mediaCollection.sessionDetails` | 对象 | 是 | 会话详细信息对象。 此 `sessionDetails` 对象应包含会话详细信息属性。 请参阅 [媒体收集架构](../../xdm/data-types/media-collection-details.md) 文档，以了解更多信息。 |
| `xdm.mediaCollection.playhead` | 整数 | 是 | 当前播放头。 |
| `xdm.mediaCollection.qoeDataDetails` | 对象 | 否 | 体验数据详细信息的质量。 请参阅 [媒体收集架构](../../xdm/data-types/media-collection-details.md) 文档，以了解更多信息。 |

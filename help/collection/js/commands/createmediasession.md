---
title: createMediaSession
description: 了解如何配置Web SDK以自动管理媒体会话
exl-id: abcb26f6-7249-4235-99eb-e4b9aeecff3e
source-git-commit: 60447ef6f881bf2a34f5502f2259328bf73d08c0
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 7%

---

# `createMediaSession`

`createMediaSession`命令是Web SDK `streamingMedia`组件的一部分。 您可以使用此组件收集与网站上的媒体会话相关的数据。 请参阅`streamingMedia` [文档](configure/streamingmedia.md)以了解如何配置此组件。

收集的数据可以包括有关媒体回放、暂停、完成和其他相关事件的信息。 收集数据后，您可以将此数据发送到[Adobe Analytics for Streaming Media](https://experienceleague.adobe.com/zh-hans/docs/media-analytics/using/media-overview)以聚合量度。 此功能为跟踪和了解您网站上的媒体消费行为提供了全面的解决方案。

您可以通过两种方式在Web SDK中创建媒体会话：

* **自动跟踪的媒体会话**&#x200B;允许Web SDK管理向[Adobe Analytics for Streaming Media](https://experienceleague.adobe.com/zh-hans/docs/media-analytics/using/media-overview)发送媒体Ping事件。 这些ping的频率由[streamingMedia](configure/streamingmedia.md)组件的配置设置决定。
* **手动跟踪的媒体会话**&#x200B;让您能够更好地控制向[Adobe Analytics for Streaming Media](https://experienceleague.adobe.com/zh-hans/docs/media-analytics/using/media-overview)发送会话Ping事件。 此外，您还可以为媒体会话存储`sessionID`。

## 创建自动跟踪的媒体会话 {#automatic}

要自动开始跟踪媒体会话，请使用下述选项调用`createMediaSession`方法：

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
| `getPlayerDetails` | 函数 | 是 | 返回播放器详细信息的函数。 此回调函数将在所提供的`playerId`的每个媒体事件之前由Web SDK调用。 |
| `xdm.eventType` | 对象 | 否 | 媒体事件类型。 如果未提供，此字段将自动设置为`media.sessionStart`。 |
| `xdm.mediaCollection.sessionDetails` | 对象 | 是 | 包含会话详细信息属性。 有关详细信息，请参阅[媒体收集架构](/help/xdm/data-types/media-collection-details.md)。 |

## 创建手动跟踪的媒体会话 {#manual}

要开始手动跟踪媒体会话，请使用如下所述的选项调用`createMediaSession`方法：

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
| `xdm.eventType` | 对象 | 否 | 媒体事件类型。 如果未提供，则它自动设置为`media.sessionStart`。 |
| `xdm.mediaCollection.sessionDetails` | 对象 | 是 | 包含会话详细信息属性。 有关详细信息，请参阅[媒体收集架构](/help/xdm/data-types/media-collection-details.md)。 |
| `xdm.mediaCollection.playhead` | 整数 | 是 | 当前播放头。 |
| `xdm.mediaCollection.qoeDataDetails` | 对象 | 否 | 体验数据详细信息的质量。 有关详细信息，请参阅[媒体收集架构](/help/xdm/data-types/media-collection-details.md)文档。 |

## 使用Web SDK标记扩展创建媒体会话

与此命令等效的Web SDK标记扩展是“[**[!UICONTROL Session start]**](/help/tags/extensions/client/web-sdk/actions/send-media-event.md#session-start)”操作中的[!UICONTROL Send media event]事件类型。

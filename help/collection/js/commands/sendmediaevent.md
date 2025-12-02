---
title: sendMediaEvent
description: 了解如何使用sendMediaEvent命令在Web SDK中跟踪媒体会话。
exl-id: a38626fd-4810-40a0-8893-e98136634fac
source-git-commit: 364b9adc406f732ea5ba450730397c4ce1bf03cf
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# `sendMediaEvent`

`sendMediaEvent`命令是Web SDK `streamingMedia`组件的一部分。 您可以使用此组件收集与网站上的媒体会话相关的数据。 请参阅`streamingMedia` [文档](configure/streamingmedia.md)以了解如何配置此组件。

使用`sendMediaEvent`命令跟踪媒体播放次数、暂停次数、完成次数、播放器状态更新及其他相关事件。

Web SDK可以根据媒体会话跟踪的类型处理媒体事件：

* **自动跟踪会话的事件处理**。 在此模式下，您无需将`sessionID`传递到媒体事件或播放头值。 Web SDK将根据提供的播放器ID和启动媒体会话时提供的`getPlayerDetails`回调函数为您处理此工作。
* **手动跟踪会话的事件处理**。 在此模式下，您需要将`sessionID`以及播放头值（整数值）传递到媒体事件。 如果需要，您还可以传递体验质量数据详细信息。

## 按类型处理媒体事件 {#handle-by-type}

选择下面的选项卡以查看每种事件类型和会话跟踪方法（自动或手动）的事件类型处理示例。

### 播放 {#play}

`media.play`事件类型用于跟踪媒体播放开始的时间。 当播放器从其他状态变为“正在播放”状态时，应发送此事件。 播放器可从中转变为“正在播放”的其他状态包括“正在缓冲”、用户从“已暂停”状态恢复、播放器从错误状态恢复或自动播放。

>[!BEGINTABS]

>[!TAB 自动会话跟踪]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.play"
    }
});
```

>[!TAB 手动会话跟踪]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.play",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### 暂停 {#pause}

`media.pauseStart`事件类型用于跟踪媒体播放何时暂停。 此事件应在用户按&#x200B;**[!UICONTROL Pause]**&#x200B;时发送。 没有恢复事件类型。 在`media.play`之后发送`media.pauseStart`事件时推断为恢复。

>[!BEGINTABS]

>[!TAB 自动会话跟踪]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.pauseStart"
    }
});
```

>[!TAB 手动会话跟踪]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.pauseStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### 错误 {#error}

`media.error`事件类型用于跟踪媒体播放期间发生错误的时间。 当发生错误时，应发送此事件。

>[!BEGINTABS]

>[!TAB 自动会话跟踪]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.error",
        mediaCollection: {
            errorDetails: {
                name: "network-error",
                source: "player"
            }
        }
    }
});
```

>[!TAB 手动会话跟踪]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.error",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                errorDetails: {
                    name: "network-error",
                    source: "player"
                }
            }
        }
    });
});
```

>[!ENDTABS]

### 广告时间开始 {#ad-break-start}

`media.adBreakStart`事件类型用于跟踪广告时间何时开始。 此事件应在广告时间开始时发送。

>[!BEGINTABS]

>[!TAB 自动会话跟踪]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakStart",
        mediaCollection: {
            advertisingPodDetails: {
                friendlyName: "Mid-roll",
                offset: 0,
                index: 1
            }
        }
    }
});
```

>[!TAB 手动会话跟踪]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                advertisingPodDetails: {
                    friendlyName: "Mid-roll",
                    offset: 0,
                    index: 1
                }
            }
        }
    });
});
```

>[!ENDTABS]

### 广告时间结束 {#ad-break-complete}

`media.adBreakComplete`事件类型用于跟踪广告时间何时结束。 此事件应在广告时间结束时发送。

>[!BEGINTABS]

>[!TAB 自动会话跟踪]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adBreakComplete"
    }
});
```

>[!TAB 手动会话跟踪]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adBreakComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### 广告开始 {#ad-start}

`media.adStart`事件类型用于跟踪广告何时开始。 此事件应在广告开始时发送。

>[!BEGINTABS]

>[!TAB 自动会话跟踪]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            advertisingDetails: {
                friendlyName: "Ad 1",
                name: "/uri-reference/001",
                length: 10,
                advertiser: "Adobe Marketing",
                campaignID: "Adobe Analytics",
                creativeID: "creativeID",
                creativeURL: "https://creativeurl.com",
                placementID: "placementID",
                siteID: "siteID",
                podPosition: 11,
                playerName: "HTML5 player"
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB 手动会话跟踪]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
        eventType: "media.adStart",
        mediaCollection: {
            playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
            sessionID,
            advertisingDetails: {
              friendlyName: "Ad 1",
              name: "/uri-reference/001",
              length: 10,
              advertiser: "Adobe Marketing",
              campaignID: "Adobe Analytics",
              creativeID: "creativeID",
              creativeURL: "https://creativeurl.com",
              placementID: "placementID",
              siteID: "siteID",
              podPosition: 11,
              playerName: "HTML5 player"
            },
            customMetadata: [
              {
                name: "myCustomValue3",
                value: "c3"
              },
              {
                name: "myCustomValue2",
                value: "c2"
              },
              {
                name: "myCustomValue1",
                value: "c1"
              }]
        }
        }
    });
});
```

>[!ENDTABS]

### 广告结束 {#ad-complete}

`media.adComplete`事件类型用于跟踪广告何时完成。 此事件应在广告完成时发送。

>[!BEGINTABS]

>[!TAB 自动会话跟踪]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adComplete"
    }
});
```

>[!TAB 手动会话跟踪]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### 广告跳过 {#ad-skip}

`media.adSkip`事件类型用于跟踪何时跳过广告。 此事件应在跳过广告时发送。

>[!BEGINTABS]

>[!TAB 自动会话跟踪]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.adSkip"
    }
});
```

>[!TAB 手动会话跟踪]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.adSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### 章节开始 {#chapter-start}

`media.chapterStart`事件类型用于跟踪章节何时开始。 此事件应在章节开始时发送。

>[!BEGINTABS]

>[!TAB 自动会话跟踪]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterStart",
        mediaCollection: {
            chapterDetails: {
                friendlyName: "Chapter 1",
                position: 1,
                length: 10,
                index: 1,
                offset: 0
            },
            customMetadata: [{
                    name: "myCustomValue3",
                    value: "c3"
                },
                {
                    name: "myCustomValue2",
                    value: "c2"
                },
                {
                    name: "myCustomValue1",
                    value: "c1"
                }
            ]
        }
    }
});
```

>[!TAB 手动会话跟踪]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                chapterDetails: {
                    friendlyName: "Chapter 1",
                    position: 1,
                    length: 10,
                    index: 1,
                    offset: 0
                },
                customMetadata: [{
                        name: "myCustomValue3",
                        value: "c3"
                    },
                    {
                        name: "myCustomValue2",
                        value: "c2"
                    },
                    {
                        name: "myCustomValue1",
                        value: "c1"
                    }
                ]
            }
        }
    });
});
```

>[!ENDTABS]

### 章节结束 {#chapter-complete}

`media.chapterComplete`事件类型用于跟踪章节何时完成。 此事件应在章节结束时发送。

>[!BEGINTABS]

>[!TAB 自动会话跟踪]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterComplete"
    }
});
```

>[!TAB 手动会话跟踪]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### 章节跳过 {#chapter-skip}

`media.chapterSkip`事件类型用于跟踪何时跳过某个章节。 在跳过章节时应发送此事件。

>[!BEGINTABS]

>[!TAB 自动会话跟踪]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.chapterSkip"
    }
});
```

>[!TAB 手动会话跟踪]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.chapterSkip",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### 缓冲开始 {#buffer-start}

`media.bufferStart`事件类型用于跟踪缓冲何时开始。 此事件应在缓冲开始时发送。 没有`bufferResume`事件类型。 在`bufferResume`之后发送播放事件时推断出`bufferStart`。

>[!BEGINTABS]

>[!TAB 自动会话跟踪]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bufferStart"
    }
});
```

>[!TAB 手动会话跟踪]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bufferStart",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### 比特率更改 {#bitrate-change}

`media.bitrateChange`事件类型用于跟踪比特率更改的时间。 此事件应在比特率发生更改时发送。

>[!BEGINTABS]

>[!TAB 自动会话跟踪]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.bitrateChange",
        mediaCollection: {
            qoeDataDetails: {
                framesPerSecond: 1,
                bitrate: 35000,
                droppedFrames: 30,
                timeToStart: 1364
            }
        }
    }
});
```

>[!TAB 手动会话跟踪]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.bitrateChange",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                qoeDataDetails: {
                    bitrate: 35000,
                    droppedFrames: 30,
                    timeToStart: 1364
                }
            }
        }
    });
});
```

>[!ENDTABS]

### 状态更新 {#state-updates}

`media.statesUpdate`事件类型用于跟踪播放器状态何时更改。 当播放器状态更改时，应发送此事件。

>[!BEGINTABS]

>[!TAB 自动会话跟踪]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.statesUpdate",
        mediaCollection: {
            statesStart: [{
                    name: "mute"
                },
                {
                    name: "pictureInPicture"
                }
            ],
            statesEnd: [{
                name: "fullScreen"
            }]
        }
    }
});
```

>[!TAB 手动会话跟踪]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.stateUpdate",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID,
                statesStart: [{
                        name: "mute"
                    },
                    {
                        name: "pictureInPicture"
                    }
                ],
                statesEnd: [{
                    name: "fullScreen"
                }]
            }
        }
    });
});
```

>[!ENDTABS]

### 会话结束 {#session-end}

`media.sessionEnd`事件类型用于通知Media Analytics后端在用户放弃观看内容并且不太可能返回时立即关闭会话。

如果不发送`sessionEnd`事件，则放弃的会话将在未收到任何事件的时间达到10分钟后超时，或者播放头没有发生移动的时间达到30分钟后超时。 会话将自动删除。

>[!BEGINTABS]

>[!TAB 自动会话跟踪]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionEnd"
    }
});
```

>[!TAB 手动会话跟踪]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionEnd",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

### 会话结束 {#session-complete}

`media.sessionComplete`事件类型用于跟踪媒体会话何时完成。 当到达主内容的结尾时，应发送此事件。

>[!BEGINTABS]

>[!TAB 自动会话跟踪]

```javascript
alloy("sendMediaEvent", {
    playerId: "movie-test",
    xdm: {
        eventType: "media.sessionComplete"
    }
});
```

>[!TAB 手动会话跟踪]

```javascript
sessionPromise.then(sessionID => {
    alloy("sendMediaEvent", {
        xdm: {
            eventType: "media.sessionComplete",
            mediaCollection: {
                playhead: parseInt(document.getElementById("movie-test").currentTime, 10),
                sessionID
            }
        }
    });
});
```

>[!ENDTABS]

## 使用Web SDK标记扩展发送媒体事件

与此命令等效的Web SDK标记扩展是[**[!UICONTROL Send media event]**](/help/tags/extensions/client/web-sdk/actions/send-media-event.md)操作。

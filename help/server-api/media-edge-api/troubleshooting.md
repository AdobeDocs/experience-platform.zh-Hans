---
keywords: Experience Platform；media edge；热门主题；日期范围
solution: Experience Platform
title: Media Edge API快速入门
description: Media Edge API故障排除指南
source-git-commit: f723114eebc9eb6bfa2512b927c5055daf97188b
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---


# Media Edge API故障排除指南

本指南提供了用于处理错误和获取成功响应的故障排除说明。

## 使用错误响应辅助

为帮助排除不成功的响应，错误会随附包含错误对象的响应正文。 在这种情况下，响应正文包含由定义的问题详细信息 [HTTP API的RFC 7807问题详细信息](https://datatracker.ietf.org/doc/html/rfc7807). 为了改善API用户体验，问题详细信息是描述性的（数组键的详细信息使用JsonPath显示到缺失或无效的字段）。 它们也是累积的（所有无效字段都将在同一请求中报告）。


## 验证会话开始

构建会话开始请求时出现的大多数问题都会导致207多状态响应。
有效负载类似于Experience Edge Network Server API的非致命错误。 所有Media Analytics错误都具有以下类型：  `https://ns.adobe.com/aep/errors/va-edge-0XXX-XXX`. 响应中显示的编号对应于错误状态。

以下示例显示了一个会话开始请求的响应正文，该响应正文既缺少必填字段，又包含无效字段。

```
{
    "requestId": "d4be4f91-a535-41e7-80c6-bdd031d3a365",
    "handle": [
        ...
    ],
    "errors": [
        {
            "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
            "status": 400,
            "title": "Invalid request",
            "report": {
                "eventIndex": 0,
                "details": [
                    {
                        "name": "$.xdm.mediaCollection.sessionDetails.name",
                        "reason": "Missing required field"
                    },
                    {
                        "name": "$.xdm.timestamp",
                        "reason": "Field should respect ISO 8601 standard for presenting date and time with offset to UTC (e.g. 2022-05-19T19:31:02Z, 2022-05-19T21:31:02+02:00, 2022-05-19T21:31:02.234+02:00)"
                    }
                ]
            }
        }
    ]
}
```

在上例中，两个问题都由以下方面注明 `name` 和 `reason` 下 `details`：显示第一个原因 `missing required field` 第二部分描述不符合ISO 8601标准的情况。


>[!NOTE]
>
> 对于从Media Analytics上游引起的错误，Adobe建议您继续处理生成的媒体会话。

## 验证事件

大多数无效事件请求会导致400错误的请求响应。 在这些情况下，有效负载类似于Experience Edge Network Server API致命错误。

对于事件请求，媒体边缘API服务包括未在XDM模型本身中捕获的其他检查。 这包括检查路径 `eventType` 匹配请求有效负载 `eventType`.


以下示例显示了 `eventType` 与不匹配 `adBreakStart` 有效负载已发送至 `ee/va/v1/chapterStart`：

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": "The payload eventType adBreakStart was different from the path eventType chapterStart"
    }
}
```

以下示例显示了Media Edge API检查的其他结果 `chapterStart` 呼叫缺失 `chapterDetails` 信息：

```
{
    "type": "https://ns.adobe.com/aep/errors/va-edge-0400-400",
    "status": 400,
    "title": "Bad Request",
    "detail": "Invalid request. Please check your input and try again.",
    "report": {
        "details": [
            {
                "name": "$.events[0].xdm.mediaCollection.chapterDetails",
                "reason": "Missing required field"
            }
        ]
    }
}
```

## 处理400级和500级错误

下表提供了处理状态响应错误的说明：


| 错误代码 | 描述 |
| ---------- | --------- |
| 4xx错误请求 | 大多数4xx错误(例如 `400`， `403`， `404`)用户不应重试。 重试请求将不会导致成功响应。 用户在重试请求之前应解决该错误。 不会跟踪导致4xx状态代码的事件，这可能会潜在影响接收4xx响应的会话中数据的准确性。 |
| 410不存在 | 表示服务器端不再计算用于跟踪的会话。 最常见的原因是会话时长超过24小时。 收到 `410`，尝试启动新会话并跟踪该会话。 |
| 429请求太多 | 此响应代码表示服务器正在限制请求的速率。 请遵循 **重试之后** 响应标头中的说明非常仔细。 任何回流的响应都必须包含带有特定于域的错误代码的HTTP响应代码。 |
| 500内部服务器错误 | `500` 错误是一般性错误，包括所有错误。 `500` 不应重试错误，以下情况除外 `502`， `503` 和 `504`. |
| 502错误的网关 | 此错误代码表示服务器在充当网关时，从上游服务器接收到无效的响应。 由于服务器之间的网络问题，可能会发生这种情况。 临时网络问题可以自行解决，因此重试请求可以解决问题。 |
| 503服务不可用 | 此错误代码表示服务暂时不可用。 这可能发生在维护期间。 的收件人 `503` 错误可能会重试该请求，但同时也应遵循 **重试之后** 标头说明。 |


## 会话响应缓慢时对事件进行排队

启动媒体跟踪会话后，媒体播放器可能会在会话开始响应从后端返回之前（通过会话ID参数）触发。 如果发生这种情况，应用程序必须对在会话开始请求与其响应之间到达的任何跟踪事件进行排队。 当会话响应到达时，您应该首先处理所有排队的事件，然后可以开始处理实时事件。

为了获得最佳结果，请查看分发版本中的参考播放器，了解在接收会话ID之前如何处理事件的说明。

以下示例说明了一种在接收会话ID之前处理事件的方法：


```
// For event payload format, see "Request body" sections of "Session Start Request", "Event Requests" respectively.  *
 
VideoPlayer.prototype._collectEvent = function(event) {
    var sessionID = event.events[0].xdm.mediaCollection.sessionID
    var eventType = event.events[0].xdm.eventType.substring("media.".length);
    // If we don't have a Session ID yet,
    // queue the event and return...
    if (sessionId === undefined) {
        console.log("[Player] Queueing event")
        _pendingEvents.push(event)
        return;
    }
 
    // If we DO have a Session ID, process the
    // tracking event...
    apiClient.request({
        "baseUrl": `${endpoint}`,
        "path": `ee/va/v1/${eventType}`,
        "method": `POST`,
        "data": `${event}`
    }).then((response) => {
        if (eventType === "sessionStart") {
            var newSessionID = response.json().handle.filter((h) => h.type === "media-analytics:new-session")[0].payload[0].sessionId;
            _processPendingEvents(newSessionID);
        }
        […]
    }
}
 
VideoPlayer.prototype._processPendingEvents function(sessionID) {
    _pendingEvents.forEach((event) => {
        event.events[0].xdm.mediaCollection.sessionID = sessionID;
        _collectEvent(event);
    });
    _pendingEvents = [];
}
```



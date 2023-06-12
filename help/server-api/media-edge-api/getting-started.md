---
keywords: Experience Platform；media edge；热门主题；日期范围
solution: Experience Platform
title: Media Edge API快速入门
description: Media Edge API快速入门
exl-id: null
source-git-commit: 8592bcc7a6d6700ec9b689b98d07a15f0b9301b2
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 7%

---


# Media Edge API快速入门

本指南提供了与Media Edge API服务成功进行初始交互的说明。 这包括启动媒体会话，然后跟踪发送到Adobe Experience Platform (AEP)解决方案(例如Customer Journey Analytics(CJA))的事件。 使用会话开始端点启动Media Edge API服务。 会话启动后，可以跟踪以下一个或多个事件：

* play
* ping
* bitrateChange
* bufferStart
* pauseStart
* adBreakStart
* adStart
* adComplete
* adSkip
* adBreakComplete
* chapterStart
* chapterComplete
* chapterSkip
* error
* sessionEnd
* sessionComplete
* 状态更新

每个事件都有自己的端点。 所有Media Edge API端点都是POST方法，具有用于事件数据的JSON请求正文。 有关Media Edge API端点、参数和示例的更多信息，请参阅Media Edge Swagger文件。

本指南说明如何在启动会话后跟踪以下事件：

* 缓冲开始
* 播放
* 会话结束

## 实施 API

除了在称为的模型和路径方面存在的细微差异之外，媒体边缘API与媒体收集API相同。 媒体收集的实施详细信息对Media Edge API仍然有效，如以下文档中所述：

* [在播放器中设置 HTTP 请求类型](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [发送 Ping 事件](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-sed-pings.html?lang=en)
* [超时情况](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-timeout.html?lang=en)
* [控制事件的顺序](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-impl/mc-api-ctrl-order.html?lang=en)

## Authorization

目前，Media Edge API的请求中不需要授权标头。


## 启动会话

要在服务器上启动媒体会话，请使用会话开始端点。 成功的响应包括 `sessionId`，这是后续事件请求的必需参数。

在发出会话开始请求之前，您将需要满足以下条件：

* 此 `datastreamId` 是POST会话启动请求的必需参数。 检索 `datastreamId`，请参见 [配置数据流](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=zh-Hans).

* 请求有效负载的JSON对象，其中包含所需的最小数据（如下面的示例请求中所示）。

获得此信息后，请提供 `datastreamId` 在以下调用中：

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionStart?configId={datastream ID} \`

### 示例请求

以下示例显示了一个会话启动cURL请求：

```
curl -i --request POST '{uri}/ee/va/v1/sessionStart?configId={dataStreamId}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
          "sessionDetails": {
            "name": "Media Analytics API Sample",
            "playerName": "sample-html5-api-player",
            "contentType": "VOD",
            "length": 60,
            "channel": "sample-channel",
            "appVersion": "va-api-1.0.0"
          },
          "playhead": 0
        }
      }
    }
  ]
}'
```

在上面的示例请求中， `eventType` 值包含前缀 `media` 根据 [体验数据模型(XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hans) 用于指定域。

此外，数据类型映射 `eventType` 上述示例中如下所示（有效负载中不应存在仅用于报表的字段）：

| 事件类型 | 数据类型 | 仅报告字段（已忽略） |
| -------- | ------ | ---------- |
| mediaSessionStart | sessiondetails | ID、adCount、averageMinuteAudience、chapterCount、estimatedStreams、hasPauseImpactedStreams、hasProgress10、hasProgress25、hasProgress50、hasProgress75、hasProgress95、hasSegmentView、isCompleted、isDownloaded、isFederated、isPlayed、isViewed、pauseCount、pausePauseTimeTimeTimeTimeConcall、segent 、pev3、pccr |
| media.chapterStart | chapterDetails | id、isCompleted、isStarted、timePlayed |
| media.adBreakStart | advertisingPodDetails | ID |
| media.adStart | advertisingDetails | id、isCompleted、isStarted、timePlayed |
| media.error | errorDetails | - |
| media.statesUpdate | statesStart：数组[playerStateData]，状态结束：数组[playerStateData] | playerStateData.isSet、playerStateData.count、playerStateData.time |
| media.sessionStart， media.chapterStart， media.adStart | custommetadata | - |
| 所有 | qoeDataDetails | bitrateAverage、bitrateAverageBucket、bitrateChangeCount、bufferCount、bufferTime、errorCount、externalErrors、hasBitrateChangeImpactedStreams、hasBufferImpactedStreams、hasErrorImpactedStreams、hasStallImpactedStreams、isDroppedBeforeStart、mediaErrors、playsErrors、playsSdkErrors、plays、playsSdkErrors、playsReerrors、playsReerrorsSdkErrors、plays |

### 示例响应

以下示例显示了对会话启动请求的成功响应：

```
HTTP/2 200
x-request-id: 99603f5c-95cf-49ad-9afb-0ba6c5867fd7
x-rate-limit-remaining: 599
vary: Origin
date: Tue, 07 Mar 2023 14:37:58 GMT
x-konductor: 23.3.2:367bc7dc
x-adobe-edge: IRL1;6
server: jag
content-type: application/json;charset=utf-8
strict-transport-security: max-age=31536000; includeSubDomains
cache-control: no-cache, no-store, max-age=0, no-transform
x-xss-protection: 1; mode=block
x-content-type-options: nosniff

{
    "requestId": "df14bca1-ba0f-4574-ae80-a4e24a960c00",
    "handle": [
        {
            "payload": [
                {
                    "sessionId": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333"
                }
            ],
            "type": "media-analytics:new-session",
            "eventIndex": 0
        },
        {
            "payload": [
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_cluster",
                    "value": "irl1",
                    "maxAge": 1800
                },
                {
                    "key": "kndctr_6D9FE18C5536A5E90A4C98A6_AdobeOrg_identity",
                    "value": "CiY1MTkxMDM4OTc1MzkwMTY4NTQ1NjAxNDg4OTgzODU5MTAzMDcyMVIPCKKt8KnsMBgBKgRJUkwx8AGirfCp7DA=",
                    "maxAge": 34128000
                }
            ],
            "type": "state:store"
        }
    ]
}
```

在上面的示例响应中， `sessionId` 显示为 `af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333`. 您将在后续事件请求中将此ID用作必需参数。

有关会话开始端点参数和示例的更多信息，请参阅Media Edge Swagger文件。

有关XDM媒体数据参数的更多信息，请参阅 [媒体详细信息架构](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/mediadetails.schema.md#xdmplayhead).


## 缓冲开始事件请求

在媒体播放器上开始缓冲时，“缓冲开始”事件将发出信号。 缓冲恢复不是API服务中的事件；而是在缓冲启动后发送播放事件时推断出来。 要发出缓冲开始事件请求，请使用 `sessionId` 在对以下端点的调用的有效负载中：

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart \`

### 示例请求

以下示例显示了一个Buffer Start cURL请求：

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/bufferStart' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

在上述示例请求中，与 `sessionId` 上一次调用中返回的参数用作缓冲开始请求中的必需参数。

有关“缓冲开始”端点参数和示例的更多信息，请参阅Media Edge Swagger文件。

成功的响应指示状态为200，并且不包含任何内容。

## 播放事件请求

当媒体播放器将其状态从其他状态（例如“正在缓冲”、“已暂停”或“错误”）更改为“正在播放”时，将发送“播放”事件。 要提出“播放”事件请求，请使用 `sessionId` 在对以下端点的调用的有效负载中：

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/play \`

### 示例请求

以下示例显示了一个Play cURL请求：

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/play' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

成功的响应指示状态为200，并且不包含任何内容。

有关播放端点参数和示例的更多信息，请参阅Media Edge Swagger文件。

## 会话结束事件请求

当到达主内容的结尾时，将发送“会话结束”事件。 要提出“会话结束”事件请求，请使用 `sessionId` 在对以下端点的调用的有效负载中：

**POST**  `https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete \`

### 示例请求

以下示例显示了“会话结束”cURL请求：

```
curl -X 'POST' \
  'https://edge.adobedc.net/ee-pre-prd/va/v1/sessionComplete' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -d '{
  "events": [
    {
      "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
          "sessionID": "af8bb22766e458fa0eef98c48ea42c9e351c463318230e851a19946862020333",
          "playhead": 25
        },
        "timestamp": "2022-03-04T13:39:00+00:00"
      }
    }
  ]
}'
```

成功的响应指示状态为200，并且不包含任何内容。

## 响应代码

下表显示了Media Edge API请求可能产生的响应代码：

| 状态 | 描述 |
| ---------- | --------- |
| 200 | 会话已成功创建 |
| 207 | 连接到Experience Edge Network的服务之一出现问题（请参阅故障排除指南中的更多信息） |
| 400级 | 错误请求 |
| 500级 | 服务器错误 |

有关处理错误和不成功响应代码的更多信息，请参阅Media Edge故障诊断指南。



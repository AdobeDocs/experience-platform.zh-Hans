---
title: 会话详细信息报表数据类型
description: 了解会话详细信息报告Experience Data Model (XDM)数据类型。
exl-id: 8bcaa0d8-2f85-4189-b0b5-8c72ecbb0660
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '1293'
ht-degree: 4%

---

# [!UICONTROL Session Details]报告数据类型

[!UICONTROL Session Details]报表是标准的体验数据模型(XDM)数据类型，可跟踪与媒体播放会话相关的数据。
媒体报告字段由Adobe服务用于分析用户发送的媒体收集字段。 此数据以及其他特定用户量度一起进行计算和报告。 架构包含一系列属性，这些属性提供了有关用户行为和内容使用模式的洞察。 使用[!UICONTROL Session Details]报表数据类型通过记录播放事件、广告交互、进度标记、暂停和其他量度来捕获用户参与度。

+++选择以显示会话详细信息报表数据类型的图表。
![会话详细信息报告数据类型的图表。](../images/data-types/session-details-reporting.png)
+++

>[!NOTE]
>
>每个显示名称都包含一个链接，指向有关其音频和视频参数的更多信息。 链接的页面包含有关Adobe收集的视频广告数据、实施值、网络参数、报表和重要注意事项的详细信息。

| 显示名称 | 属性 | 数据类型 | 描述 |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|--------------------------------------------------------------------------------------------------|
| [[!UICONTROL 10% Progress Marker]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#ten-%25-progress-marker) | `hasProgress10` | 布尔值 | 表示播放头通过了基于流长度的10%媒体标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| [[!UICONTROL 25% Progress Marker]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#twenty-five-%25-progress-marker) | `hasProgress25` | 布尔值 | 表示播放头通过了基于流长度的25%媒体标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| [[!UICONTROL 50% Progress Marker]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#50%25-progress-marker) | `hasProgress50` | 布尔值 | 表示播放头通过了基于流长度的50%媒体标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| [[!UICONTROL 75% Progress Marker]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#seventy-five-%25-progress-marker) | `hasProgress75` | 布尔值 | 表示播放头通过了基于流长度的75%媒体标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| [[!UICONTROL 95% Progress Marker]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#ninety-five-%25-progress-marker) | `hasProgress95` | 布尔值 | 表示播放头通过了基于流长度的95%媒体标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| [[!UICONTROL Ad Count]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#ad-count) | `adCount` | 整数 | 播放期间开始的广告数。 |
| [!UICONTROL Ad Load Type] | `adLoad` | 字符串 | 由每个客户的内部呈现定义的所加载的广告类型。 |
| [[!UICONTROL Album]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#album) | `album` | 字符串 | 音乐录制或视频所属的专辑的名称。 |
| [[!UICONTROL Artist]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#artist) | `artist` | 字符串 | 执行音乐录制或视频的唱片艺术家或群体的名称。 |
| [[!UICONTROL Asset ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#asset-id) | `assetID` | 字符串 | [!UICONTROL Asset ID]是媒体资产内容的唯一标识符，例如电视剧剧集标识符、电影资产标识符或实时事件标识符。 通常，这些ID是从元数据颁发机构（如EIDR、TMS/Gracenote或Rovi）派生的。 这些标识符也可以来自其他专有或内部系统。 |
| [[!UICONTROL Author]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#author) | `author` | 字符串 | 媒体作者的姓名。 |
| [[!UICONTROL Average Minute Audience]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#average-minute-audience) | `averageMinuteAudience` | 数字描述在特定媒体项目上花费的平均内容时间，即花费的总内容时间除以所有播放会话的长度。 |  |
| [[!UICONTROL Broadcast Content Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-type) | `contentType` | 字符串 | 流投放的[!UICONTROL Broadcast Content Type]。 每个[!UICONTROL Stream Type]的可用值包括：<br>音频：“song”、“podcast”、“audiobook”和“radio”；<br>视频：“VoD”、“Live”、“Linear”、“UGC”和“DVoD”。<br>客户可以为此参数提供自定义值。 |
| [[!UICONTROL Broadcast Network]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#network) | `network` | 字符串 | 网络/渠道名称。 |
| [[!UICONTROL Chapter Count]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#chapter-count) | `chapterCount` | 整数 | 播放期间开始播放的章节的数量。 |
| [[!UICONTROL Content Channel]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-channel) | `channel` | 字符串 | [!UICONTROL Content Channel]是从中播放内容的分发渠道。 |
| [[!UICONTROL Content Completes]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-complete) | `isCompleted` | 布尔值 | [!UICONTROL Content Completes]指示定时媒体资源是否已观看完毕。 此事件并不一定意味着观看者观看了整个视频；观看者可以跳过前面。 |
| [!UICONTROL Content Delivery Network] | `cdn` | 字符串 | 已播放内容的[!UICONTROL Content Delivery Network]。 |
| [[!UICONTROL Content ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-id) | `name` | 字符串 | [!UICONTROL Content ID]是内容的唯一标识符。 它可用于链接回其他行业或CMS ID。 |
| [[!UICONTROL Content Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-name-(variable)) | `friendlyName` | 字符串 | [!UICONTROL Content Name]是内容的“友好”（人类可读）名称。 |
| [[!UICONTROL Content Player Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-player-name) | `playerName` | 字符串 | 内容播放器的名称。 |
| [[!UICONTROL Content Starts]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-starts) | `isPlayed` | 布尔值 | 使用媒体的第一帧时，[!UICONTROL Content Starts]会变为true。 如果用户在广告播放或缓冲等过程中放弃观看，则不会计为[!UICONTROL Content Starts]事件。 |
| [[!UICONTROL Content Time Spent]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-time-spent) | `timePlayed` | 整数 | [!UICONTROL Content Time Spent]计算主内容中所有“播放”类型事件的事件总时长（以秒为单位）。 |
| [[!UICONTROL Creator Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#originator) | `originator` | 字符串 | 内容创建者的名称。 |
| [[!UICONTROL Day Part]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#day-part) | `dayPart` | 字符串 | 一个属性，定义内容在一天中的哪个时间广播或播放。 客户可以视需要为此属性设置任何值 |
| [[!UICONTROL Episode Number]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#episode) | `episode` | 字符串 | 剧集的数量。 |
| [[!UICONTROL Estimated Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#estimated-streams) | `estimatedStreams` | 数值 | 每个单独内容片段的估计的视频或音频流数量。 |
| [[!UICONTROL Federated Data]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#federated-data) | `isFederated` | 布尔值 | 如果点击已联合（即，客户作为联合数据共享的一部分接收，而不是他们自己的实施），[!UICONTROL Federated Data]将设置为true。 |
| [[!UICONTROL Feed Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-feed-type) | `feed` | 字符串 | 馈送的类型，可以表示与馈送相关的实际数据（例如EAST HD或SD），也可以表示馈送的来源（例如URL）。 |
| [[!UICONTROL First Air Date]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-air-date) | `firstAirDate` | 字符串 | 内容首次在电视上播出的日期。 可接受任何日期格式，但Adobe建议使用如下格式：YYYY-MM-DD。 |
| [[!UICONTROL First Digital Date]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-digital-date) | `firstDigitalDate` | 字符串 | 内容首次在任何数字渠道或平台上播出的日期。 可接受任何日期格式，但Adobe建议使用如下格式：YYYY-MM-DD。 |
| [[!UICONTROL Genre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#genre) | `genre` | 字符串 | 内容制作者定义的内容类型或分组。 变量实施中的值应以逗号分隔。 |
| [[!UICONTROL Media Authorized]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#authorized) | `authorized` | 字符串 | 确认用户是否已通过Adobe身份验证获得授权。 |
| [[!UICONTROL Media Content Length]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-length-(variable)) | `length` | 整数     是 | [!UICONTROL Media Content Length]包含剪辑长度/运行时间 — 这是所使用内容的最大长度（或持续时间）（以秒为单位）。 |
| [[!UICONTROL Media Downloaded Flag]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-downloaded-flag) | `isDownloaded` | 布尔值 | 流下载后已在设备上本地播放。 |
| [[!UICONTROL Media Segment Views]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-segment-views) | `hasSegmentView` | 布尔值 | [!UICONTROL Media Segment Views]指示何时查看了至少一个帧（不一定是第一个帧）。 |
| [[!UICONTROL Media Session ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-session-id) | `ID` | 字符串 | [!UICONTROL Media Session ID]标识单个播放所独有的内容流实例。<br><em>注意：<em>`sessionId`针对除`sessionStart`之外的所有事件和所有下载的事件发送。 |
| [[!UICONTROL Media Session Server Timeout]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#seconds-since-last-call) | `secondsSinceLastCall` | 数字[!UICONTROL Media Session Server Timeout]表示用户最后一次已知交互和会话关闭之间经过的时间量（以秒为单位）。 |  |
| [[!UICONTROL Media Starts]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-starts) | `isViewed` | 布尔值 | 媒体的载入事件。 当查看器选择播放按钮时，会发生这种情况。 即使存在前置广告、缓冲、错误等，也会将此计为视频载入事件。 |
| [[!UICONTROL Media Time Spent]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-time-spent) | `totalTimePlayed` | 整数 | 描述用户在特定定时媒体资源上花费的总时间，其中包括观看广告所用的时间。 |
| [[!UICONTROL MVPD Identifier]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#mvpd) | `mvpd` | 字符串 | 通过Adobe身份验证提供的[!UICONTROL MVPD Identifier]。 |
| [[!UICONTROL Pause Events]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#pause-events) | `pauseCount` | 整数 | [!UICONTROL Pause Events]计算播放期间发生的暂停时段数。 |
| [[!UICONTROL Pause Impacted Streams]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#paused-impacted-streams) | `hasPauseImpactedStreams` | 布尔值指示在播放单个媒体项目期间是否发生了一次或多次暂停。 |  |
| [!UICONTROL Pccr] | `pccr` | 布尔值 | [!UICONTROL Pccr]指示已发生重定向。 |
| [!UICONTROL Pev3] | `pev3` | 字符串 | [!UICONTROL Pev3]是用于报告的媒体流类型。 |
| [[!UICONTROL Publisher]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#publisher) | `publisher` | 字符串 | 音频内容发布者的名称。 |
| [[!UICONTROL Radio Station]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#station) | `station` | 字符串 | 播放音频的电台名称。 |
| [[!UICONTROL Rating Value]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-rating) | `rating` | 字符串 | 由电视节目家长指南定义的评级。 |
| [[!UICONTROL Record Label]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#label) | `label` | 字符串 | 记录标签的名称。 |
| [[!UICONTROL Resume]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-resumes) | `hasResume` | 布尔值 | 标记在缓冲、暂停或停滞时间超过30分钟后恢复的每次播放。 |
| [[!UICONTROL Season Number]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#season) | `season` | 字符串 | 节目所属的[!UICONTROL Season Number]。 只有在节目属于某个系列节目的组成部分时，才需要指定“季系列”。 |
| [[!UICONTROL Series Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show) | `show` | 字符串 | 节目/系列名称。 只有在节目属于某个系列节目的组成部分时，才需要指定“节目名称”。 |
| [[!UICONTROL Show Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show-type) | `showType` | 字符串 | 内容类型，例如，预告片或完整剧集。 |
| [[!UICONTROL Stream Format]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-format) | `streamFormat` | 字符串 | 流的格式(HD、SD)。 |
| [[!UICONTROL Stream Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-type) | `streamType` | 字符串 | 媒体流的类型。 |
| [[!UICONTROL Total Pause Duration]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#total-pause-duration) | `pauseTime` | 整数 | [!UICONTROL Total Pause Duration]描述用户暂停播放的持续时间（以秒为单位）。 |
| [[!UICONTROL Unique Time Played]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#unique-time-played) | `uniqueTimePlayed` | 整数 | 描述用户在定时媒体资源上看到的唯一间隔的总和，即多次查看的播放间隔长度只计算一次。 |
| [[!UICONTROL Version]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#sdk-version) | `appVersion` | 字符串 | 播放器使用的SDK版本。 该参数可使用您的播放器支持的任何自定义值。 |
| [[!UICONTROL Video Segment]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-segment) | `segment` | 字符串 | 描述已查看内容部分的间隔（以分钟为单位）。 |

{style="table-layout:auto"}

<!-- Could not find details for :
Ad Load Type
Content Delivery Network
Pccr
Pev3
-->

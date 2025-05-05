---
title: 会话详细信息报表数据类型
description: 了解会话详细信息报告Experience Data Model (XDM)数据类型。
exl-id: 8bcaa0d8-2f85-4189-b0b5-8c72ecbb0660
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 13%

---

# [!UICONTROL 会话详细信息]报告数据类型

[!UICONTROL 会话详细信息]报告是标准的体验数据模型(XDM)数据类型，可跟踪与媒体播放会话相关的数据。
媒体报告字段由Adobe服务用于分析用户发送的媒体收集字段。 此数据以及其他特定用户量度一起进行计算和报告。 架构包含一系列属性，这些属性提供了有关用户行为和内容使用模式的洞察。 使用[!UICONTROL 会话详细信息]报表数据类型通过记录播放事件、广告交互、进度标记、暂停和其他量度来捕获用户参与度。

+++选择以显示会话详细信息报表数据类型的图表。
![会话详细信息报告数据类型的图表。](../images/data-types/session-details-reporting.png)
+++

>[!NOTE]
>
>每个显示名称都包含一个链接，指向有关其音频和视频参数的更多信息。 链接的页面包含有关Adobe收集的视频广告数据、实现值、网络参数、报表和重要注意事项的详细信息。

| 显示名称 | 属性 | 数据类型 | 描述 |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|--------------------------------------------------------------------------------------------------|
| [[!UICONTROL 10%进度标记]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#ten-%25-progress-marker) | `hasProgress10` | 布尔值 | 表示播放头通过了基于流长度的10%媒体标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| [[!UICONTROL 25%进度标记]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#twenty-five-%25-progress-marker) | `hasProgress25` | 布尔值 | 表示播放头通过了基于流长度的25%媒体标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| [[!UICONTROL 50%进度标记]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#50%25-progress-marker) | `hasProgress50` | 布尔值 | 表示播放头通过了基于流长度的50%媒体标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| [[!UICONTROL 75%进度标记]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#seventy-five-%25-progress-marker) | `hasProgress75` | 布尔值 | 表示播放头通过了基于流长度的75%媒体标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| [[!UICONTROL 95%进度标记]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#ninety-five-%25-progress-marker) | `hasProgress95` | 布尔值 | 表示播放头通过了基于流长度的95%媒体标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| [[!UICONTROL 广告计数]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#ad-count) | `adCount` | 整数 | 播放期间开始播放的广告的数量。 |
| [!UICONTROL 广告加载类型] | `adLoad` | 字符串 | 由每个客户的内部呈现定义的所加载的广告类型。 |
| [[!UICONTROL 相册]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#album) | `album` | 字符串 | 音乐录音或视频所属的专辑的名称。 |
| [[!UICONTROL 艺人]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#artist) | `artist` | 字符串 | 执行音乐录制或视频创作的专辑艺术家姓名或组合名称。 |
| [[!UICONTROL 资产ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#asset-id) | `assetID` | 字符串 | [!UICONTROL 资产ID]是媒体资产内容的唯一标识符，例如电视剧剧集标识符、电影资产标识符或实时事件标识符。 通常，这些ID是从元数据颁发机构（如EIDR、TMS/Gracenote或Rovi）派生的。 这些标识符也可以来自其他专有或内部系统。 |
| [[!UICONTROL 作者]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#author) | `author` | 字符串 | 媒体作者的姓名。 |
| [[!UICONTROL 平均受众访问分钟数]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#average-minute-audience) | `averageMinuteAudience` | 数字描述在特定媒体项目上花费的平均内容时间，即花费的总内容时间除以所有播放会话的长度。 |
| [[!UICONTROL 广播内容类型]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-type) | `contentType` | 字符串 | 流投放的[!UICONTROL 广播内容类型]。 每个[!UICONTROL 流类型]的可用值包括：<br>音频：“song”、“podcast”、“audiobook”和“radio”；<br>视频：“VoD”、“Live”、“Linear”、“UGC”和“DVoD”。<br>客户可以为此参数提供自定义值。 |
| [[!UICONTROL 广播网络]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#network) | `network` | 字符串 | 网络/渠道名称。 |
| [[!UICONTROL 章节计数]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#chapter-count) | `chapterCount` | 整数 | 播放期间开始播放的章节的数量。 |
| [[!UICONTROL 内容渠道]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-channel) | `channel` | 字符串 | [!UICONTROL 内容频道]是从中播放内容的分发频道。 |
| [[!UICONTROL 内容完成]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-complete) | `isCompleted` | 布尔值 | [!UICONTROL 内容完成]指示定时媒体资源是否已观看完毕。 此事件并不一定意味着观看者观看了整个视频；观看者可以跳过前面。 |
| [!UICONTROL 内容传递网络] | `cdn` | 字符串 | 已播放内容的[!UICONTROL 内容传递网络]。 |
| [[!UICONTROL 内容ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-id) | `name` | 字符串 | [!UICONTROL 内容ID]是内容的唯一标识符。 它可用于链接回其他行业或CMS ID。 |
| [[!UICONTROL 内容名称]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-name-(variable)) | `friendlyName` | 字符串 | [!UICONTROL 内容名称]是内容的“友好”（人类可读）名称。 |
| [[!UICONTROL 内容播放器名称]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-player-name) | `playerName` | 字符串 | 内容播放器的名称。 |
| [[!UICONTROL 内容开始]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-starts) | `isPlayed` | 布尔值 | 使用媒体的第一帧时，[!UICONTROL 内容开始]变为true。 如果用户在广告、缓冲等过程中放弃观看，则不会有[!UICONTROL 内容开始]事件。 |
| [[!UICONTROL 内容逗留时间]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-time-spent) | `timePlayed` | 整数 | [!UICONTROL 内容逗留时间]计算主内容中所有“播放”类型事件的事件总时长（以秒为单位）。 |
| [[!UICONTROL 创建者名称]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#originator) | `originator` | 字符串 | 内容创建者的名称。 |
| [[!UICONTROL 天部分]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#day-part) | `dayPart` | 字符串 | 一个属性，定义内容在一天中的哪个时间广播或播放。 客户可以视需要为此属性设置任何值 |
| [[!UICONTROL 剧集编号]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#episode) | `episode` | 字符串 | 剧集的数量。 |
| [[!UICONTROL 预计的流]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#estimated-streams) | `estimatedStreams` | 数值 | 每个单独内容片段的估计的视频或音频流数量。 |
| [[!UICONTROL 联合数据]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#federated-data) | `isFederated` | 布尔值 | 如果点击已联合（即，客户作为联合数据共享的一部分接收，而不是他们自己的实施），则[!UICONTROL 联合数据]设置为true。 |
| [[!UICONTROL 馈送类型]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#media-feed-type) | `feed` | 字符串 | 馈送的类型，可以表示与馈送相关的实际数据（例如EAST HD或SD），也可以表示馈送的来源（例如URL）。 |
| [[!UICONTROL 首次播放日期]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#first-air-date) | `firstAirDate` | 字符串 | 内容首次在电视上播出的日期。 可接受任何日期格式，但Adobe建议使用如下格式：YYYY-MM-DD。 |
| [[!UICONTROL 首次数字化日期]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#first-digital-date) | `firstDigitalDate` | 字符串 | 内容首次在任何数字渠道或平台上播出的日期。 可接受任何日期格式，但Adobe建议使用如下格式：YYYY-MM-DD。 |
| [[!UICONTROL 流派]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#genre) | `genre` | 字符串 | 内容制作者定义的内容类型或分组。 变量实施中的值应以逗号分隔。 |
| [[!UICONTROL 已授权的媒体]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#authorized) | `authorized` | 字符串 | 确认用户是否已通过Adobe身份验证获得授权。 |
| [[!UICONTROL 媒体内容长度]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-length-(variable)) | `length` | 整数 | 是 | [!UICONTROL 媒体内容长度]包含剪辑长度/运行时间 — 这是所使用内容的最大长度（或持续时间）（以秒为单位）。 |
| [[!UICONTROL 媒体下载标志]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#media-downloaded-flag) | `isDownloaded` | 布尔值 | 在下载后，该流在设备上本地播放。 |
| [[!UICONTROL 媒体区段视图]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-segment-views) | `hasSegmentView` | 布尔值 | [!UICONTROL 媒体区段查看]指示何时查看了至少一个帧（不一定是第一个帧）。 |
| [[!UICONTROL 媒体会话ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#media-session-id) | `ID` | 字符串 | [!UICONTROL 媒体会话ID]标识对于单个播放而言唯一的内容流实例。<br><em>注意：<em>`sessionId`针对除`sessionStart`之外的所有事件和所有下载的事件发送。 |
| [[!UICONTROL 媒体会话服务器超时]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#seconds-since-last-call) | `secondsSinceLastCall` | 数字[!UICONTROL 媒体会话服务器超时]表示用户最后一次已知交互和会话关闭之间经过的时间量（以秒为单位）。 |
| [[!UICONTROL 媒体开始]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#media-starts) | `isViewed` | 布尔值 | 媒体的载入事件。 当查看器选择播放按钮时，会发生这种情况。 即使存在前置广告、缓冲、错误等，也会将此计为视频载入事件。 |
| [[!UICONTROL 媒体逗留时间]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#media-time-spent) | `totalTimePlayed` | 整数 | 描述用户在特定定时媒体资源上花费的总时间，其中包括观看广告所用的时间。 |
| [[!UICONTROL MVPD标识符]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#mvpd) | `mvpd` | 字符串 | 通过Adobe身份验证提供的[!UICONTROL MVPD标识符]。 |
| [[!UICONTROL 暂停事件]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#pause-events) | `pauseCount` | 整数 | [!UICONTROL 暂停事件]计算播放期间发生的暂停时段数。 |
| [[!UICONTROL 暂停影响的流]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#paused-impacted-streams) | `hasPauseImpactedStreams` | 布尔值指示在播放单个媒体项目期间是否发生了一次或多次暂停。 |
| [!UICONTROL Pccr] | `pccr` | 布尔值 | [!UICONTROL Pccr]指示已发生重定向。 |
| [!UICONTROL Pev3] | `pev3` | 字符串 | [!UICONTROL Pev3]是用于报告的媒体流类型。 |
| [[!UICONTROL 发布者]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#publisher) | `publisher` | 字符串 | 音频内容发布者的名称。 |
| [[!UICONTROL 电台]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#station) | `station` | 字符串 | 播放音频的电台的名称。 |
| [[!UICONTROL 评分值]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-rating) | `rating` | 字符串 | 由电视节目家长指南定义的评级。 |
| [[!UICONTROL 记录标签]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#label) | `label` | 字符串 | 记录标签的名称。 |
| [[!UICONTROL 继续]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-resumes) | `hasResume` | 布尔值 | 标记在缓冲、暂停或停滞时间超过 30 分钟后恢复的每次播放。 |
| [[!UICONTROL 季编号]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#season) | `season` | 字符串 | 节目所属的[!UICONTROL 季编号]。 只有在节目属于某个系列节目的组成部分时，才需要指定“季系列”。 |
| [[!UICONTROL 系列名称]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#show) | `show` | 字符串 | 节目/系列名称。 只有在节目属于某个系列节目的组成部分时，才需要指定“节目名称”。 |
| [[!UICONTROL 显示类型]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#show-type) | `showType` | 字符串 | 内容类型，例如，预告片或完整剧集。 |
| [[!UICONTROL 流格式]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#stream-format) | `streamFormat` | 字符串 | 流的格式(HD、SD)。 |
| [[!UICONTROL 流类型]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#stream-type) | `streamType` | 字符串 | 媒体流的类型。 |
| [[!UICONTROL 暂停总持续时间]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#total-pause-duration) | `pauseTime` | 整数 | [!UICONTROL 暂停总持续时间]描述用户暂停播放的持续时间（以秒为单位）。 |
| [[!UICONTROL 唯一播放时间]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#unique-time-played) | `uniqueTimePlayed` | 整数 | 描述用户在定时媒体资源上看到的唯一间隔的总和，即多次查看的播放间隔长度只计算一次。 |
| [[!UICONTROL 版本]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#sdk-version) | `appVersion` | 字符串 | 播放器使用的SDK版本。 该参数可使用您的播放器支持的任何自定义值。 |
| [[!UICONTROL 视频区段]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-segment) | `segment` | 字符串 | 描述已查看内容部分的时间间隔（以分钟为单位）。 |

{style="table-layout:auto"}

<!-- Could not find details for :
Ad Load Type
Content Delivery Network
Pccr
Pev3
-->

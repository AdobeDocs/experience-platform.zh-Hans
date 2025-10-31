---
title: Adobe Analytics Source连接器的映射字段
description: 使用Adobe Analytics Source Connector将Analytics字段映射到XDM字段。
exl-id: 15dc1368-5cf1-42e1-9683-d5158f8aa2db
source-git-commit: 83a249daddbee1ec264b6e505517325c76ac9b09
workflow-type: tm+mt
source-wordcount: '3838'
ht-degree: 5%

---

# Analytics字段映射

Adobe Experience Platform允许您通过Analytics源摄取Adobe Analytics数据。 通过ADC摄取的某些数据可以直接从Analytics字段映射到体验数据模型(XDM)字段，而其他数据需要转换和特定函数才能成功映射。

![从Analytics到Experience Platform的Adobe Analytics数据历程的插图。](../images/analytics-data-experience-platform.png)

## 流媒体参数

有关流媒体参数的信息，请阅读下表。

| 数据馈送 | XDM字段路径 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| `videoname` | `mediaReporting.sessionDetails.friendlyName` | 字符串 | 视频的友好（人类可读）名称。 |
| `videoaudioauthor` | `mediaReporting.sessionDetails.author` | 字符串 | 媒体作者的姓名。 |
| `videoaudioartist` | `mediaReporting.sessionDetails.artist` | 字符串 | 执行音乐录制或视频的唱片艺术家或群体的名称。 |
| `videoaudioalbum` | `mediaReporting.sessionDetails.album` | 字符串 | 音乐录制或视频所属的专辑的名称。 |
| `videolength` | `mediaReporting.sessionDetails.length` | 整数 | 视频的长度或运行时间。 |
| `videoshowtype` | `mediaReporting.sessionDetails.showType` | 字符串 |  |
| `video` | `mediaReporting.sessionDetails.name` | 字符串 | 视频的ID。 |
| `videoshow` | `mediaReporting.sessionDetails.show` | 字符串 | 节目或系列节目的名称。 只有在节目属于某个系列节目的组成部分时，才需要提供节目/系列的名称。 |
| `videostreamtype` | mediaReporting.sessionDetails.streamType | 字符串 | 流媒体的类型，如“视频”或“音频”。 |
| `videoseason` | `mediaReporting.sessionDetails.season` | 字符串 | 节目所属的季编号。 仅当节目属于某个系列时，才需要使用此值。 |
| `videoepisode` | `mediaReporting.sessionDetails.episode` | 字符串 | 剧集的数量。 |
| `videogenre` | `mediaReporting.sessionDetails.genreList[]` | 字符串[] | 视频的流派。 |
| `videosessionid` | `mediaReporting.sessionDetails.ID` | 字符串 | 单个播放所独有的内容流实例的标识符。 |
| `videoplayername` | `mediaReporting.sessionDetails.playerName` | 字符串 | 视频播放器的名称。 |
| `videochannel` | `mediaReporting.sessionDetails.channel` | 字符串 | 播放内容的分发渠道。 |
| `videocontenttype` | `mediaReporting.sessionDetails.contentType` | 字符串 | 用于内容的流投放类型。 对于所有视频查看，此参数自动设置为“视频”。 推荐值包括：VOD、Live、Linear、UGC、DVOD、Radio、Podcast、Audiobook和Song。 |
| `videonetwork` | `mediaReporting.sessionDetails.network` | 字符串 | 网络或通道名称。 |
| `videofeedtype` | `mediaReporting.sessionDetails.feed` | 字符串 | 馈送的类型。 这可以表示与馈送相关的实际数据（例如“East HD”或“SD”），也可以表示馈送的来源（例如URL）。 |
| `videosegment` | `mediaReporting.sessionDetails.segment` | 字符串 |  |
| `videostart` | `mediaReporting.sessionDetails.isViewed` | 布尔 | 一个布尔值，指示视频是否已启动。 一旦用户选择播放按钮，即使存在前置广告、缓冲、错误等，也会发生这种情况，并计为播放次数。 |
| `videoplay` | `mediaReporting.sessionDetails.isPlayed` | 布尔 | 一个布尔值，指示媒体的第一帧是否已开始。 如果用户在任何广告或缓冲时间中断，则“内容开始”不符合条件。 |
| `videotime` | `mediaReporting.sessionDetails.timePlayed` | 整数 | 主内容上`type=PLAY`的所有事件的持续时间（以秒为单位）。 |
| `videocomplete` | `mediaReporting.sessionDetails.isCompleted` | 布尔 | 布尔值，指示定时媒体资源是否已观看完毕。 此值不一定表示查看器已观看了整个视频，因为此值并不考虑查看器可能会跳过的情况。 |
| `videototaltime` | `mediaReporting.sessionDetails.totalTimePlayed` | 整数 | 用户在特定定时媒体资源上花费的总时间，包括观看广告所用的时间。 |
| `videouniquetimeplayed` | `mediaReporting.sessionDetails.uniqueTimePlayed` | 整数 | 用户在定时媒体资源上看到的唯一间隔的总和。 换言之，多次查看的播放间隔长度只计算一次。 |
| `videoaverageminuteaudience` | `mediaReporting.sessionDetails.averageMinuteAudience` | 数字 | 特定媒体项目的平均内容逗留时间。 换言之，用内容逗留总时间除以所有播放会话的长度。 |
| `videoprogress10` | `mediaReporting.sessionDetails.hasProgress10` | 布尔 | 一个布尔值，指示给定视频的播放头是否超过总视频长度的10%标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| `videoprogress25` | `mediaReporting.sessionDetails.hasProgress25` | 布尔 | 一个布尔值，指示给定视频的播放头是否超过视频总长度的25%标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| `videoprogress50` | `mediaReporting.sessionDetails.hasProgress50` | 布尔 | 一个布尔值，指示给定视频的播放头是否超过总视频长度的50%标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| `videoprogress75` | `mediaReporting.sessionDetails.hasProgress75` | 布尔 | 一个布尔值，指示给定视频的播放头是否超过总视频长度的75%标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| `videoprogress95` | `mediaReporting.sessionDetails.hasProgress95` | 布尔 | 一个布尔值，指示给定视频的播放头是否超过总视频长度的95%标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| `videopause` | `mediaReporting.sessionDetails.hasPauseImpactedStreams` | 布尔 | 布尔值，指示在播放单个媒体项目期间是否发生了一次或多次暂停。 |
| `videopausecount` | `mediaReporting.sessionDetails.pauseCount` | 整数 | 播放期间发生的暂停时段数。 |
| `videopausetime` | `mediaReporting.sessionDetails.pauseTime` | 整数 | 用户暂停播放的总持续时间（以秒为单位）。 |
| `videomvpd` | `mediaReporting.sessionDetails.mvpd` | 字符串 | 通过MVPD身份验证提供的Adobe标识符。 |
| `videoauthorized` | `mediaReporting.sessionDetails.authorized` | 字符串 | 定义用户是否已通过Adobe身份验证获得授权。 |
| `videodaypart` | `mediaReporting.sessionDetails.dayPart` | 定义一天中广播或播放内容的时间。 |  |
| `videoresume` | `mediaReporting.sessionDetails.hasResume` | 布尔 | 一个布尔值，标记在超过30分钟的缓冲、暂停或停滞时段后恢复的每次播放。 |
| `videosegmentviews` | `mediaReporting.sessionDetails.hasSegmentView` | 布尔 | 布尔值，指示至少已查看了一个帧。 此帧不必是第一帧。 |
| `videoaudiolabel` | `mediaReporting.sessionDetails.label` | 字符串 | 记录标签的名称。 |
| `videoaudiostation` | `mediaReporting.sessionDetails.station` | 字符串 | 播放音频的电台或名称。 |
| `videoaudiopublisher` | `mediaReporting.sessionDetails.publisher` | 字符串 | 音频内容发布者的名称。 |
| `videosecondssincelastcall` | `mediaReporting.sessionDetails.secondsSinceLastCall` | 数字 | 指示用户最后一次已知交互和会话关闭之间经过的时间（以秒为单位）。 |
| `videoadload` | `mediaReporting.sessionDetails.adLoad` | 字符串 | 由您自己的内部表示定义的所加载的广告类型。 |

{style="table-layout:auto"}

## Advertising参数

有关广告参数的信息，请阅读下表。

| 数据馈送 | XDM字段路径 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| `videoad` | `mediaReporting.advertisingDetails.name` | 字符串 | 广告的名称。 在报表中，“广告名称”是分类，“广告名称（变量）”是eVar。 |
| `videoadinpod` | `mediaReporting.advertisingDetails.podPosition` | 整数 | 父广告开始内部的广告索引。 例如，第一个广告的索引为0，第二个广告的索引为1。 |
| `videoadlength` | `mediaReporting.advertisingDetails.length` | 整数 | 视频广告的长度，以秒为单位。 |
| `videoadplayername` | `mediaReporting.advertisingDetails.playerName` | 字符串 | 用于呈现广告的播放器的名称。 |
| `videoadpod` | `mediaReporting.advertisingPodDetails.ID` | 字符串 | 广告时间的ID。 |
| `videoadname` | `mediaReporting.advertisingDetails.friendlyName` | 字符串 | 广告时间的友好（人类可读）名称。 |
| `videoadadvertiser` | `mediaReporting.advertisingDetails.advertiser` | 字符串 | 广告中展现的产品所属的公司或品牌。 |
| `videoadcampaign` | `mediaReporting.advertisingDetails.campaignID` | 字符串 | 广告营销活动的ID。 |
| `videoadstart` | `mediaReporting.advertisingDetails.isStarted` | 布尔 | 一个布尔值，指示广告是否已启动。 |
| `videoadcomplete` | `mediaReporting.advertisingDetails.isCompleted` | 布尔 | 一个布尔值，指示是否已完成。 |
| `videoadtime` | `mediaReporting.advertisingDetails.timePlayed` | 整数 | 观看广告所花费的总时间，以秒为单位。 |

{style="table-layout:auto"}

## 章节参数

有关章节参数的信息，请阅读下表。

| 数据馈送 | XDM字段路径 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| `videochapter` | `mediaReporting.chapterDetails.ID` | 字符串 | 自动生成的章节ID。 |
| `videochapterstart` | `mediaReporting.chapterDetails.isStarted` | 布尔 | 一个布尔值，指示章节是否已启动。 |
| `videochaptercomplete` | `mediaReporting.chapterDetails.isCompleted` | 布尔 | 一个布尔值，指示章节是否已完成。 |
| `videochaptertime` | `mediaReporting.chapterDetails.timePlayed` | 整数 | 在章节花费的时间，以秒为单位。 |

{style="table-layout:auto"}

## 播放器状态参数

有关播放器状态参数的信息，请阅读下表。

| 数据馈送 | XDM字段路径 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| `videostatefullscreen` | `mediaReporting.states[].isSet` | 布尔 | 一个布尔值，指示视频状态是否设置为全屏。 |
| `videostatefullscreencount` | `mediaReporting.states[].count` | 整数 | 将视频状态设置为全屏的次数。 |
| `videostatefullscreentime` | `mediaReporting.states[].time` | 整数 | 视频状态设置为全屏时的总持续时间。 |
| `videostateclosedcaptioning` | `mediaReporting.states[].isSet` | 布尔 | 一个布尔值，指示是否启用隐藏式字幕。 |
| `videostateclosedcaptioningcount` | `mediaReporting.states[].count` | 整数 | 启用隐藏式字幕的次数。 |
| `videostateclosedcaptioningtime` | `mediaReporting.states[].time` | 整数 | 启用隐藏式字幕的总时间。 |
| `videostatemute` | `mediaReporting.states[].isSet` | 布尔 | 一个布尔值，指示视频状态是否设置为静音。 |
| `videostatemutecount` | `mediaReporting.states[].count` | 整数 | 视频静音的次数。 |
| `videostatemutetime` | `mediaReporting.states[].time` | 整数 | 静音视频的总时长。 |
| `videostatepictureinpicture` | `mediaReporting.states[].isSet` | 布尔 | 一个布尔值，指示是否启用画中画模式。 |
| `videostatepictureinpicturecount` | `mediaReporting.states[].count` | 整数 | 启用画中画模式的次数。 |
| `videostatepictureinpicturetime` | `mediaReporting.states[].time` | 整数 | 启用画中画模式的总持续时间。 |
| `videostateinfocus` | `mediaReporting.states[].isSet` | 布尔 | 一个布尔值，指示是否启用聚焦模式 |
| `videostateinfocuscount` | `mediaReporting.states[].count` | 整数 | 启用画中画模式的次数。 |
| `videostateinfocustime` | `mediaReporting.states[].time` | 整数 | 启用聚焦模式的总持续时间。 |

{style="table-layout:auto"}

## 质量参数

有关质量参数的信息，请阅读下表。

| 数据馈送 | XDM字段路径 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| `videoqoebitrateaverage` | `mediaReporting.qoeDataDetails.bitrateAverage` | 数字 | 平均比特率（以kbps为单位，整数）。 此量度计算为在播放会话期间发生的播放持续时间的所有相关比特率值的加权平均值。 |
| `videoqoebitratechange` | `mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams` | 布尔 | 一个布尔值，指示发生比特率更改的流数量。 只有在播放会话期间发生至少一次比特率更改事件时，此量度才设置为true。 |
| `videoqoebitratechangecountevar` | `mediaReporting.qoeDataDetails.bitrateChangeCount` | 整数 |  |
| `videoqoebitrateaverageevar` | `mediaReporting.qoeDataDetails.bitrateAverageBucket` | 字符串 | 比特率更改的次数。 此值计算为在播放会话期间发生的所有比特率更改事件的总和。 |
| `videoqoetimetostartevar` | `mediaReporting.qoeDataDetails.timeToStart` | 整数 | 视频加载和视频开始之间经过的持续时间（以秒为单位）。 |
| `videoqoedroppedframes` | `mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams` | 布尔 | 一个布尔值，指示丢帧的流数量。 只有在播放会话期间至少丢失了一个帧时，此量度才设置为true。 |
| `videoqoedroppedframecountevar` | `mediaReporting.qoeDataDetails.droppedFrames` | 整数 | 主内容播放期间丢帧的数量。 |
| `videoqoebuffercountevar` | `mediaReporting.qoeDataDetails.bufferCount` | 整数 | 缓冲事件的次数。 此量度计算为在播放会话期间发生不同缓冲状态的次数。 此量度计算播放器从其他状态（例如播放或暂停）进入缓冲状态的次数。 |
| `videoqoebuffertimeevar` | `mediaReporting.qoeDataDetails.bufferTime` | 整数 | 缓冲所花费的总时间，以秒为单位。 此值计算为在播放会话期间发生的所有缓冲事件持续时间的总和。 |
| `videoqoebuffer` | `mediaReporting.qoeDataDetails.hasBufferImpactedStreams` | 布尔 | 布尔值，指示受缓冲影响的流数量。 只有在播放会话期间发生至少一次缓冲事件时，此量度才设置为true。 |
| `videoqoeerror` | `mediaReporting.qoeDataDetails.hasErrorImpactedStreams` | 布尔 | 一个布尔值，指示发生错误事件的流数量。 例如，如果在播放会话期间调用trackError，并生成了type=error心率调用。 只有在播放期间发生至少一次错误时，此量度才设置为true。 |
| `videoerrorcountevar` | `mediaReporting.qoeDataDetails.errorCount` | 整数 | 发生的错误数。 此值计算为在播放会话期间发生的所有错误事件的总和。 |
| `videoqoeplayersdkerrors` | `mediaReporting.qoeDataDetails.playerSdkErrors` | 字符串数组 | 播放器SDK生成的唯一错误ID。 您必须在实施时通过提供的错误API来提供错误代码或ID。 |
| `videoqoeextneralerrors` | `mediaReporting.qoeDataDetails.externalErrors` | 字符串数组 | 来自任何外部源（如CDN错误）的唯一错误ID。 您必须在实施时通过提供的错误API来提供错误代码或ID。 |
| `videoqoedropbeforestart` | `mediaReporting.qoeDataDetails.isDroppedBeforeStart` | 布尔 | Media SDK在播放期间生成的唯一错误ID。 |

{style="table-layout:auto"}

## 已弃用的字段

有关已弃用的Analytics映射字段的信息，请阅读此部分。

### 直接映射字段

+++选择可查看已弃用的直接映射字段的表

| 数据馈送 | XDM字段 | XDM类型 | 描述 |
| --- | --- | --- | --- |
| `m_evar1`<br/>`[...]`<br/>`m_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | 字符串 | 自定义Analytics eVar。 每个组织可以以不同的方式使用eVar。 |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | 字符串 | 自定义Analytics prop。 每个组织可以有不同的方式使用prop。 |
| `m_browser` | `_experience.analytics.environment.`<br/>`browserID` | 整数 | 浏览器的编号ID。 |
| `m_browser_height` | `environment.browserDetails.viewportHeight` | 整数 | 浏览器的高度（像素）。 |
| `m_browser_width` | `environment.browserDetails.viewportWidth` | 整数 | 浏览器的宽度（像素）。 |
| `m_campaign` | `marketing.trackingCode` | 字符串 | 在跟踪代码维度中使用的变量。 |
| `m_channel` | `web.webPageDetails.siteSection` | 字符串 | 在“网站区域”维度中使用的变量。 |
| `m_domain` | `environment.domain` | 字符串 | 在域维度中使用的变量。 它基于用户的互联网服务提供商(ISP)。 |
| `m_geo_city` | `placeContext.geo.city` | 字符串 | 点击所在城市的名称。 这是基于点击的IP地址。 |
| `m_geo_dma` | `placeContext.geo.dmaID` | 整数 | 点击人口统计区的数值ID。 这是基于点击的IP地址。 |
| `m_geo_region` | `placeContext.geo.stateProvince` | 字符串 | 点击所在州或地区的名称。 这是基于点击的IP地址。 |
| `m_geo_zip` | `placeContext.geo.postalCode` | 字符串 | 点击的邮政编码。 这是基于点击的IP地址。 |
| `m_keywords` | `search.keywords` | 字符串 | 在“关键字”维度中使用的变量。 |
| `m_os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | 整数 | 表示访客的操作系统的数值ID。 这是基于user_agent列的。 |
| `m_page_url` | `web.webPageDetails.URL` | 字符串 | 页面点击的URL。 |
| `m_pagename` | `web.webPageDetails.pageViews.value` | 字符串 | 具有页面名称的点击上等于1。 这类似于Adobe Analytics页面查看次数量度。 |
| `m_referrer` | `web.webReferrer.URL` | 字符串 | 上一页的页面URL。 |
| `m_search_page_num` | `search.pageDepth` | 整数 | 供所有搜索页面排名维度使用。 指示用户在点击进入您的网站之前您的网站出现在搜索结果的哪个页面。 |
| `m_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | 字符串 | 状态变量。 |
| `m_user_server` | `web.webPageDetails.server` | 字符串 | 在服务器维度中使用的变量。 |
| `m_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | 字符串 | 用于填充邮政编码维度的变量。 |
| `accept_language` | `environment.browserDetails.acceptLanguage` | 字符串 | 列出所有接受的语言，如Accept-Language HTTP标头所示。 |
| `homepage` | `web.webPageDetails.isHomePage` | 布尔 | 已不再使用。 指示当前URL是否为浏览器的主页。 |
| `ipv6` | `environment.ipV6` | 字符串 |  |
| `j_jscript` | `environment.browserDetails.javaScriptVersion` | 字符串 | 浏览器支持的JavaScript版本。 |
| `user_agent` | `environment.browserDetails.userAgent` | 字符串 | HTTP标头中发送的用户代理字符串。 |
| `mobileappid` | `application.name` | 字符串 | 移动设备应用程序ID，以下列格式存储： `[AppName][BundleVersion]`。 |
| `mobiledevice` | `device.model` | 字符串 | 移动设备的名称。 在iOS上，它存储为逗号分隔的2位字符串。 第一个数字代表第几代设备，第二个数字代表设备系列。 |
| `pointofinterest` | `placeContext.POIinteraction.POIDetail.`<br/>`name` | 字符串 | 由Mobile Services使用。 表示目标点。 |
| `pointofinterestdistance` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.distanceToCenter` | 数字 | 由Mobile Services使用。 表示兴趣点距离。 |
| `mobileplaceaccuracy` | `placeContext.POIinteraction.POIDetail.`<br/>`geoInteractionDetails.deviceGeoAccuracy` | 数字 | 从上下文数据变量a.loc.acc收集。 指示GPS在收集时的精度（以米为单位）。 |
| `mobileplacecategory` | `placeContext.POIinteraction.POIDetail.`<br/>`category` | 字符串 | 从上下文数据变量a.loc.category收集。 描述特定位置的类别。 |
| `mobileplaceid` | `placeContext.POIinteraction.POIDetail.`<br/>`POIID` | 字符串 | 从上下文数据变量a.loc.id收集。 给定目标点的标识符。 |
| `videoadpod` | `advertising.adAssetViewDetails.adBreak._id` | 字符串 | |
| `mobilebeaconmajor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMajor` | 数字 | Mobile Services信标主要。 |
| `mobilebeaconminor` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.beaconMinor` | 数字 | Mobile Services信标次要。 |
| `mobilebeaconuuid` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximityUUID` | 字符串 | 移动服务信标UUID。 |
| `mobileinstalls` | `application.firstLaunches` | 对象 | 在安装或重新安装后`{id (string), value (number)}`首次运行时会触发此事件 |
| `mobileupgrades` | `application.upgrades` | 对象 | 报告应用程序升级次数。 升级后或版本号更改后首次运行时触发。`{id (string), value (number)}` |
| `mobilelaunches` | `application.launches` | 对象 | 应用程序已启动的次数。 `{id (string), value (number)}` |
| `mobilecrashes` | `application.crashes` | 对象 | `{id (string), value (number)}` |
| `mobilemessageclicks` | `directMarketing.clicks` | 对象 | `{id (string), value (number)}` |
| `mobileplaceentry` | `placeContext.POIinteraction.poiEntries` | 对象 | `{id (string), value (number)}` |
| `mobileplaceexit` | `placeContext.POIinteraction.poiExits` | 对象 | `{id (string), value (number)}` |
| `videoqoetimetostart` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.timeToStart` | 对象 | 视频品质：开始时间。`{id (string), value (number)}` |
| `videoqoedropbeforestart` | `media.mediaTimed.dropBeforeStarts` | 对象 | `{id (string), value (number)}` |
| `videoqoebuffercount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.buffers` | 对象 | 视频品质：缓冲区计数`{id (string), value (number)}` |
| `videoqoebuffertime` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bufferTime` | 对象 | 视频品质：缓冲时间`{id (string), value (number)}` |
| `videoqoebitratechangecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateChanges` | 对象 | 视频质量更改计数`{id (string), value (number)}` |
| `videoqoebitrateaverage` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.bitrateAverage` | 对象 | 视频品质：平均比特率`{id (string), value (number)}` |
| `videoqoeerrorcount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.errors` | 对象 | 视频品质：错误计数`{id (string), value (number)}` |
| `videoqoedroppedframecount` | `media.mediaTimed.primaryAssetViewDetails.`<br/>`qoe.droppedFrames` | 对象 | `{id (string), value (number)}` |

{style="table-layout:auto"}

+++

## 生成的映射字段

必须转换来自ADC的选择字段，这要求在XDM中生成来自Adobe Analytics的直接副本以外的逻辑。

+++选择可查看已弃用生成的映射字段的表

| 数据馈送 | XDM字段 | XDM类型 | 描述 |
| --- | --- | --- | --- |
| `m_prop1`<br/>`[...]`<br/>`m_prop75` | `_experience.analytics.customDimensions`<br/>`.listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | 对象 | 自定义Analytics属性，配置为列表属性。 它包含分隔的值列表。`{}` |
| `m_hier1`<br/>`[...]`<br/>`m_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | 对象 | 由层次结构变量使用。 它包含分隔的值列表。`{values (array), delimiter (string)}` |
| `m_mvvar1`<br/>`[...]`<br/>`m_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | 数组 | 自定义Analytics列表变量。 包含分隔的值列表。 `{value (string), key (string)}` |
| `m_color` | `device.colorDepth` | 整数 | 颜色深度ID，它基于c_color列的值。 |
| `m_cookies` | `environment.browserDetails.cookiesEnabled` | 布尔 | 在“Cookie支持”维度中使用的变量。 |
| `m_event_list` | `commerce.purchases`，<br/>`commerce.productViews`，<br/>`commerce.productListOpens`，<br/>`commerce.checkouts`，<br/>`commerce.productListAdds`，<br/>`commerce.productListRemovals`，<br/>`commerce.productListViews` | 对象 | 点击时触发的标准商务事件。`{id (string), value (number)}` |
| `m_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | 对象 | 点击时触发的自定义事件。`{id (Object), value (Object)}` |
| `m_geo_country` | `placeContext.geo.countryCode` | 字符串 | 点击来源国家/地区的缩写，基于IP地址。 |
| `m_geo_latitude` | `placeContext.geo._schema.latitude` | 数字 | |
| `m_geo_longitude` | `placeContext.geo._schema.longitude` | 数字 | |
| `m_java_enabled` | `environment.browserDetails.javaEnabled` | 布尔 | 指示Java™是否已启用的标记。 |
| `m_latitude` | `placeContext.geo._schema.latitude` | 数字 | |
| `m_longitude` | `placeContext.geo._schema.longitude` | 数字 | |
| `m_page_event_var1` | `web.webInteraction.URL` | 字符串 | 仅在链接跟踪图像请求中使用的变量。 此变量包含下载链接、退出链接或单击的自定义链接的URL。 |
| `m_page_event_var2` | `web.webInteraction.name` | 字符串 | 仅在链接跟踪图像请求中使用的变量。 这会列出链接的自定义名称（如果已指定）。 |
| `m_page_type` | `web.webPageDetails.isErrorPage` | 布尔 | 用于填充页面未找到维度的变量。 此变量应为空或包含“ErrorPage”。 |
| `m_pagename_no_url` | `web.webPageDetails.name` | 数字 | 页面的名称（如果已设置）。 如果未指定页面，此值将留空。 |
| `m_paid_search` | `search.isPaid` | 布尔 | 如果点击与付费搜索检测相匹配，则设置此标记。 |
| `m_product_list` | `productListItems[].items` | 数组 | 产品列表，通过products变量传入。 | {SKU （字符串）、数量（整数）、价格总计（数字）} |
| `m_ref_type` | `web.webReferrer.type` | 字符串 | 表示点击的反向链接类型的数值ID。<br/>`1`：网站内<br/>`2`：其他网站<br/>`3`：搜索引擎<br/>`4`：硬盘<br/>`5`：未发送<br/>`6`：已输入/添加书签（无反向链接）<br/>`7`：电子邮件<br/>`8`：无JavaScript<br/>`9`：社交网络 |
| `m_search_engine` | `search.searchEngine` | 字符串 | 表示将访客引荐至您的网站的搜索引擎的数值ID。 |
| `post_currency` | `commerce.order.currencyCode` | 字符串 | 交易期间使用的货币代码。 |
| `post_cust_hit_time_gmt` | `timestamp` | 字符串 | 这仅在启用了时间戳的数据集中使用。 这是随点击发送的时间戳，基于UNIX®时间。 |
| `post_cust_visid` | `identityMap` | 对象 | 客户访客ID。 |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.primary` | 布尔 | 客户访客ID。 |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.namespace.code` | 字符串 | 客户访客ID。 |
| `post_visid_high` + `visid_low` | `identityMap` | 对象 | 访问的唯一标识符。 |
| `post_visid_high` + `visid_low` | `endUserIDs._experience.aaid.id` | 字符串 | 访问的唯一标识符。 |
| `post_visid_high` | `endUserIDs._experience.aaid.primary` | 布尔 | 与`visid_low`一起使用以唯一标识访问。 |
| `post_visid_high` | `endUserIDs._experience.aaid.namespace.code` | 字符串 | 与`visid_low`一起使用以唯一标识访问。 |
| `post_visid_low` | `identityMap` | 对象 | 与visid_high结合使用，用来唯一标识访问。 |
| `hit_time_gmt` | `receivedTimestamp` | 字符串 | 点击的时间戳，基于UNIX®时间。 |
| `hitid_high` + `hitid_low` | `_id` | 字符串 | 用于标识点击的唯一标识符。 |
| `hitid_low` | `_id` | 字符串 | 与hitid_high一起使用，唯一标识点击。 |
| `ip` | `environment.ipV4` | 字符串 | IP地址，基于图像请求的HTTP标头。 |
| `j_jscript` | `environment.browserDetails.javaScriptEnabled` | 布尔 | 使用的JavaScript版本。 |
| `mcvisid_high` + `mcvisid_low` | identityMap | 对象 | Experience Cloud访客ID。 |
| `mcvisid_high` + `mcvisid_low` | endUserIDs._experience.mcid.id | 字符串 | Experience Cloud ID (ECID)也称为MCID，有时用于命名空间。 |
| `mcvisid_high` | `endUserIDs._experience.mcid.primary` | 布尔 | Experience Cloud ID (ECID)也称为MCID，有时用于命名空间。 |
| `mcvisid_high` | `endUserIDs._experience.mcid.namespace.code` | 字符串 | Experience Cloud ID (ECID)也称为MCID，有时用于命名空间。 |
| `mcvisid_low` | `identityMap` | 对象 | Experience Cloud访客ID。 |
| `sdid_high` + `sdid_low` | `_experience.target.supplementalDataID` | 字符串 | 点击拼接ID。 分析字段sdid_high和sdid_low是用于拼合两个（或更多）传入点击的补充数据ID。 |
| `mobilebeaconproximity` | `placeContext.POIinteraction.POIDetail.`<br/>`beaconInteractionDetails.proximity` | 字符串 | Mobile Services信标邻近性。 |

{style="table-layout:auto"}

+++

## 拆分映射字段

这些字段具有单个源，但映射到&#x200B;**多个** XDM位置。

+++选择可查看已弃用的拆分映射字段的表

| 数据馈送 | XDM字段 | XDM类型 | 描述 |
| --- | --- | --- | --- |
| `s_resolution` | `device.screenWidth`，<br/>`device.screenHeight` | 整数 | 表示显示器分辨率的数值ID。 |
| `mobileosversion` | `environment.operatingSystem`，<br/>`environment.operatingSystemVersion` | 字符串 | 移动设备操作系统版本。 |

{style="table-layout:auto"}

+++

## 高级映射字段

在Adobe使用处理规则、VISTA规则和查找表调整其值后，选择字段（称为“post values”）将包含数据。 大多数post值具有预处理的对应项。

Analytics Source Connector将预处理的数据发送到Experience Platform的数据集中。 您可以使用转换将此数据转换为经过后处理的对应数据。 要了解有关使用查询服务执行这些转换的更多信息，请参阅查询服务用户指南中的[Adobe定义的函数](/help/query-service/sql/adobe-defined-functions.md)。

要了解有关使用查询服务执行这些转换的更多信息，请参阅查询服务用户指南中的[Adobe定义的函数](/help/query-service/sql/adobe-defined-functions.md)。

+++选择可查看已弃用的高级映射字段的表

| 数据馈送 | XDM字段 | XDM类型 | 描述 |
| — | — | — | — ||
| `post_evar1`<br/>`[...]`<br/>`post_evar250` | `_experience.analytics.customDimensions.`<br/>`eVars.eVar1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`eVars.eVar250` | 字符串 | 自定义Analytics eVar。 每个组织可以以不同的方式使用eVar。 |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`props.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`props.prop75` | 字符串 | 自定义Analytics prop。 每个组织可以有不同的方式使用prop。 |
| `post_browser_height` | `environment.browserDetails.viewportHeight` | 整数 | 浏览器的高度（像素）。 |
| `post_browser_width` | `environment.browserDetails.viewportWidth` | 整数 | 浏览器的宽度（像素）。 |
| `post_campaign` | `marketing.trackingCode` | 字符串 | 在跟踪代码维度中使用的变量。 |
| `post_channel` | `web.webPageDetails.siteSection` | 字符串 | 在“网站区域”维度中使用的变量。 |
| `post_cust_visid` | `endUserIDs._experience.aacustomid.id` | 字符串 | 自定义访客ID（如果已设置）。 |
| `post_first_hit_page_url` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.URL` | 字符串 | 访客访问到的第一个页面的URL。 |
| `post_first_hit_pagename` | `_experience.analytics.endUser.`<br/>`firstWeb.webPageDetails.name` | 字符串 | 在原始登入页面维度中使用的变量。 访客的登录页面的页面名称。 |
| `post_keywords` | `search.keywords` | 字符串 | 为点击收集的关键字。 |
| `post_page_url` | `web.webPageDetails.URL` | 字符串 | 页面点击的URL。 |
| `post_pagename` | `web.webPageDetails.pageViews.value` | 字符串 | 具有页面名称的点击上等于1。 这类似于Adobe Analytics页面查看次数量度。 |
| `post_purchaseid` | `commerce.order.purchaseID` | 字符串 | 用于唯一标识购买的变量。 |
| `post_referrer` | `web.webReferrer.URL` | 字符串 | 上一页的URL。 |
| `post_state` | `_experience.analytics.customDimensions.`<br/>`stateProvince` | 字符串 |  状态变量。 |
| `post_user_server` | `web.webPageDetails.server` | 字符串 | 在服务器维度中使用的变量。 |
| `post_zip` | `_experience.analytics.customDimensions.`<br/>`postalCode` | 字符串 | 用于填充邮政编码维度的变量。 |
| `browser` | `_experience.analytics.environment.`<br/>`browserID` | 整数 | 浏览器的数值ID。 |
| `domain` | `environment.domain` | 字符串 | 在域维度中使用的变量。 它基于用户的互联网服务提供商(ISP)。 |
| `first_hit_referrer` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.URL` | 字符串 | 访客的第一个反向链接URL。 |
| `geo_city` | `placeContext.geo.city` | 字符串 | 点击所在城市的名称。 这是基于点击的IP地址。 |
| `geo_dma` | `placeContext.geo.dmaID` | 整数 | 点击人口统计区的数值ID。 这是基于点击的IP地址。 |
| `geo_region` | `placeContext.geo.stateProvince` | 字符串 | 点击所在州或地区的名称。 这是基于点击的IP地址。 |
| `geo_zip` | `placeContext.geo.postalCode` | 字符串 | 点击的邮政编码。 这是基于点击的IP地址。 |
| `os` | `_experience.analytics.environment.`<br/>`operatingSystemID` | 整数 | 表示访客的操作系统的数值ID。 这是基于user_agent列的。 |
| `search_page_num` | `search.pageDepth` | 整数 | 此变量由所有搜索页面排名维度使用，它指示您网站的搜索结果页面 | 在用户点击进入您的网站之前出现在。 |
| `visit_keywords` | `_experience.analytics.session.`<br/>`search.keywords` | 字符串 | 在搜索关键字维度中使用的变量。 |
| `visit_num` | `_experience.analytics.session.`<br/>`num` | 整数 | 在访问数量维度中使用的变量。 此值从1开始，每当新访问开始（每个用户）时，该值就会递增。 |
| `visit_page_num` | `_experience.analytics.session.`<br/>`depth` | 整数 | 在点击深度维度中使用的变量。 对于用户生成的每次点击，此值增加1，并在每次访问后重置。 |
| `visit_referrer` | `_experience.analytics.session.`<br/>`web.webReferrer.URL` | 字符串 | 访问的第一个反向链接。 |
| `visit_search_page_num` | `_experience.analytics.session.`<br/>`search.pageDepth` | 整数 | 访问的第一个页面名称。 |
| `post_prop1`<br/>`[...]`<br/>`post_prop75` | `_experience.analytics.customDimensions.`<br/>`listprops.prop1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`listprops.prop75` | 对象 | 自定义Analytics属性，配置为列表属性。 它包含分隔的值列表。 |
| `post_hier1`<br/>`[...]`<br/>`post_hier5` | `_experience.analytics.customDimensions.`<br/>`hierarchies.hier1`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`hierarchies.hier5` | 对象 | 由层次结构变量使用并包含分隔的值列表。 | {values (array)， delimiter (string)} |
| `post_mvvar1`<br/>`[...]`<br/>`post_mvvar3` | `_experience.analytics.customDimensions.`<br/>`lists.list1.list[]`<br/>`[...]`<br/>`_experience.analytics.customDimensions.`<br/>`lists.list3.list[]` | 数组 | 变量值的列表。 包含分隔的自定义值列表，具体取决于实施。 | {值（字符串），键（字符串）} |
| `post_cookies` | `environment.browserDetails.cookiesEnabled` | 布尔型 | 在“Cookie支持”维度中使用的变量。 |
| `post_event_list` | `commerce.purchases`，<br/>`commerce.productViews`，<br/>`commerce.productListOpens`，<br/>`commerce.checkouts`，<br/>`commerce.productListAdds`，<br/>`commerce.productListRemovals`，<br/>`commerce.productListViews` | 对象 | 点击时触发的标准商务事件。 | {id （字符串），值（数字）} |
| `post_event_list` | `_experience.analytics.event1to100.event1`<br/>`[...]`<br/>`_experience.analytics.event901to1000.event1000` | 对象 | 点击时触发的自定义事件。| {id（对象），值（对象）} |
| `post_java_enabled` | `environment.browserDetails.javaEnabled` | 布尔型 | 指示Java™是否已启用的标记。 |
| `post_latitude` | `placeContext.geo._schema.latitude` | 数字 |   |
| `post_longitude` | `placeContext.geo._schema.longitude` | 数字 |   |
| `post_page_event` | `web.webInteraction.type` | 字符串 | 在图像请求中发送的点击类型（标准点击、下载链接、退出链接或单击的自定义链接）。 |
| `post_page_event` | `web.webInteraction.linkClicks.value` | 数字 | 如果点击是链接点击，则等于1。 这类似于Adobe Analytics中的“页面事件”量度。 |
| `post_page_event_var1` | `web.webInteraction.URL` | 字符串 | 此变量仅在链接跟踪图像请求中使用。 它是已单击下载链接、退出链接或自定义链接的URL。 |
| `post_page_event_var2` | `web.webInteraction.name` | 字符串 | 此变量仅在链接跟踪图像请求中使用。 它是链接的自定义名称。 |
| `post_page_type` | `web.webPageDetails.isErrorPage` | 布尔型 | 用于填充未找到页面维度。 此变量应为空或包含“ErrorPage” |
| `post_pagename_no_url` | `web.webPageDetails.name` | 数字 | 页面的名称（如果已设置）。 如果未指定页面，此值将留空。 |
| `post_product_list` | `productListItems[].items` | 数组 | 产品列表，通过products变量传入。 | {SKU （字符串）、数量（整数）、价格总计（数字）} |
| `post_search_engine` | `search.searchEngine` | 字符串 | 表示将访客引荐至您的网站的搜索引擎的数值ID。 |
| `mvvar1_instances` | `.list.items[]` | 对象 | 变量值列表。 包含分隔的自定义值列表，具体取决于实施。 |
| `mvvar2_instances` | `.list.items[]` | 对象 | 变量值列表。 包含分隔的自定义值列表，具体取决于实施。 |
| `mvvar3_instances` | `.list.items[]` | 对象 | 变量值列表。 包含分隔的自定义值列表，具体取决于实施。 |
| `color` | `device.colorDepth` | 整数 | 颜色深度ID，基于c_color列的值。 |
| `first_hit_ref_type` | `_experience.analytics.endUser.`<br/>`firstWeb.webReferrer.type` | 字符串 | 数值ID，表示访客的第一个反向链接的反向链接类型。 |
| `first_hit_time_gmt` | `_experience.analytics.endUser.`<br/>`firstTimestamp` | 整数 | 访客第一次点击的时间戳(以UNIX®时间表示)。 |
| `geo_country` | `placeContext.geo.countryCode` | 字符串 | 点击来源国家/地区的缩写，基于IP地址。 |
| `geo_latitude` | `placeContext.geo._schema.latitude` | 数字 |  |
| `geo_longitude` | `placeContext.geo._schema.longitude` | 数字 |  |
| `paid_search` | `search.isPaid` | 布尔型 | 如果点击与付费搜索检测相匹配，则设置此标记。 |
| `ref_type` | `web.webReferrer.type` | 字符串 | 表示点击的反向链接类型的数值ID。 |
| `visit_paid_search` | `_experience.analytics.session.`<br/>`search.isPaid` | 布尔型 | 指示访问的第一次点击是否来自付费搜索点击的标志（1=付费，0=未付费）。 |
| `visit_ref_type` | `_experience.analytics.session.`<br/>`web.webReferrer.type` | 字符串 | 表示访问的第一个反向链接的反向链接类型的数值ID。 |
| `visit_search_engine` | `_experience.analytics.session.`<br/>`search.searchEngine` | 字符串 | 访问的第一个搜索引擎的数值ID。 |
| `visit_start_time_gmt` | `_experience.analytics.session.`<br/>`timestamp` | 整数 | 访问首次点击的时间戳(以UNIX®时间表示)。 |

+++

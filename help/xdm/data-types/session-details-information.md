---
title: 会话详细信息数据类型
description: 了解会话详细信息体验数据模型(XDM)数据类型。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 8%

---

# [!UICONTROL 会话详细信息] 数据类型

[!UICONTROL 会话详细信息] 是一个标准的体验数据模型(XDM)数据类型，可跟踪与媒体播放会话相关的数据。 架构包含一系列属性，这些属性提供了有关如何使用媒体内容的见解。 使用 [!UICONTROL 会话详细信息] 用于通过记录播放事件、广告交互、进度标记、暂停和其他量度来捕获用户参与的数据类型。 这提供了有关用户行为和内容使用模式的宝贵见解。

+++选择以显示“会话详细信息”数据类型的图表。
![会话详细信息数据类型的图表。](../images/data-types/session-details-information.png)
+++

| 显示名称 | 属性 | 数据类型 | 描述 |
| --- | --- | --- | --- |
| [!UICONTROL 媒体会话ID] | `ID` | 字符串 | 此 [!UICONTROL 媒体会话ID] 标识对于单次播放而言具有唯一性的内容流实例。 |
| [!UICONTROL 内容Id] | `name` | 字符串 | **必填** 此 [!UICONTROL 内容Id] 是内容的唯一标识符。 它可用于链接回其他行业或CMS ID。 |
| [!UICONTROL 内容名称] | `friendlyName` | 字符串 | 此 [!UICONTROL 内容名称] 是内容的“友好”（人类可读）名称。 |
| [!UICONTROL 媒体内容长度] | `length` | 整数 | **必填** 此 [!UICONTROL 媒体内容长度] 包含剪辑长度/运行时间 — 此值是所使用内容的最大长度（或时长），以秒为单位。 |
| [!UICONTROL 广播内容类型] | `contentType` | 字符串 | **必填** 此 [!UICONTROL 广播内容类型] 流投放的ID。 可用的值，按 [!UICONTROL 流类型] 包括：<br>音频： “song”、“podcast”、“audiobook”和“radio”；<br>视频： “VoD”、“实时”、“线性”、“UGC”和“DVoD”。<br>客户可以为此参数提供自定义值。 |
| [!UICONTROL 内容播放器名称] | `playerName` | 字符串 | **必填** 内容播放器的名称。 |
| [!UICONTROL 内容渠道] | `channel` | 字符串 | **必填** 此 [!UICONTROL 内容渠道] 是播放内容的分发渠道。 |
| [!UICONTROL 版本] | `appVersion` | 字符串 | 播放器使用的SDK版本。 该参数可使用您的播放器支持的任何自定义值。 |
| [!UICONTROL 系列名称] | `show` | 字符串 | 节目/系列名称。 只有在节目属于某个系列节目的组成部分时，才需要指定“节目名称”。 |
| [!UICONTROL 季编号] | `season` | 字符串 | 此 [!UICONTROL 季编号] 该节目所属的。 只有在节目属于某个系列节目的组成部分时，才需要指定“季系列”。 |
| [!UICONTROL 集数] | `episode` | 字符串 | 剧集的数量。 |
| [!UICONTROL 资产ID] | `assetID` | 字符串 | 此 [!UICONTROL 资产ID] 是媒体资产内容的唯一标识符，例如电视剧剧集标识符、电影资产标识符或实时事件标识符。 通常，这些 ID 是从元数据颁发机构（如 EIDR、TMS/Gracenote 或 Rovi）派生的。这些标识符也可以来自其他专有或内部系统。 |
| [!UICONTROL 流派] | `genre` | 字符串 | 内容制作者定义的内容类型或分组。 变量实施中的值应以逗号分隔。 |
| [!UICONTROL 首次播放日期] | `firstAirDate` | 字符串 | 内容首次在电视上播出的日期。 可接受任何日期格式，但Adobe建议使用如下格式：YYYY-MM-DD。 |
| [!UICONTROL 首次数字化日期] | `firstDigitalDate` | 字符串 | 内容首次在任何数字渠道或平台上播出的日期。 可接受任何日期格式，但Adobe建议使用如下格式：YYYY-MM-DD。 |
| [!UICONTROL 评级值] | `rating` | 字符串 | 由电视节目家长指南定义的评级。 |
| [!UICONTROL  创建者名称] | `originator` | 字符串 | 内容创建者的名称。 |
| [!UICONTROL 广播网络] | `network` | 字符串 | 网络/渠道名称。 |
| [!UICONTROL 节目类型] | `showType` | 字符串 | 内容类型，例如，预告片或完整剧集。 |
| [!UICONTROL 广告加载类型] | `adLoad` | 字符串 | 由每个客户的内部呈现定义的所加载的广告类型。 |
| [!UICONTROL MVPD标识符] | `mvpd` | 字符串 | 此 [!UICONTROL MVPD标识符] 通过Adobe身份验证提供的。 |
| [!UICONTROL 媒体已授权] | `authorized` | 字符串 | 确认用户是否已通过Adobe身份验证获得授权。 |
| [!UICONTROL 时段] | `dayPart` | 字符串 | 一个属性，定义内容在一天中的哪个时间广播或播放。 客户可以视需要为此属性设置任何值 |
| [!UICONTROL 信息源类型] | `feed` | 字符串 | 馈送的类型，可以表示与馈送相关的实际数据（例如EAST HD或SD），也可以表示馈送的来源（例如URL）。 |
| [!UICONTROL 流格式] | `streamFormat` | 字符串 | 流的格式(HD、SD)。 |
| [!UICONTROL 继续] | `hasResume` | 布尔值 | 标记在缓冲、暂停或停滞时间超过30分钟后恢复的每次播放。 |
| [!UICONTROL 流类型] | `streamType` | 字符串 | 媒体流的类型。 |
| [!UICONTROL 艺人] | `artist` | 字符串 | 执行音乐录制或视频的唱片艺术家或群体的名称。 |
| [!UICONTROL 相册] | `album` | 字符串 | 音乐录制或视频所属的专辑的名称。 |
| [!UICONTROL 记录标签] | `label` | 字符串 | 记录标签的名称。 |
| [!UICONTROL 作者] | `author` | 字符串 | 媒体作者的姓名。 |
| [!UICONTROL 广播电台] | `station` | 字符串 | 播放音频的电台名称。 |
| [!UICONTROL 发布者] | `publisher` | 字符串 | 音频内容发布者的名称。 |
| [!UICONTROL 视频区段] | `segment` | 字符串 | 描述已查看内容部分的间隔（以分钟为单位）。 |
| [!UICONTROL 媒体下载标志] | `isDownloaded` | 布尔值 | 流下载后已在设备上本地播放。 |
| [!UICONTROL 联合数据] | `isFederated` | 布尔值 | [!UICONTROL 联合数据] 如果点击已联合（即，客户作为联合数据共享的一部分接收，而不是他们自己的实施），则设置为true。 |
| [!UICONTROL 媒体开始] | `isViewed` | 布尔值 | 媒体的载入事件。 当查看器选择播放按钮时，会发生这种情况。 即使存在前置广告、缓冲、错误等，也会将此计为视频载入事件。 |
| [!UICONTROL 内容开始] | `isPlayed` | 布尔值 | [!UICONTROL 内容开始] 当第一帧媒体被观看时，为true。 如果用户在广告播放或缓冲等过程中放弃观看，则不会 [!UICONTROL 内容开始] 事件。 |
| [!UICONTROL 内容结束] | `isCompleted` | 布尔值 | [!UICONTROL 内容结束] 指示定时媒体资源是否已观看完毕。 此事件并不一定意味着观看者观看了整个视频；观看者可以跳过前面。 |
| [!UICONTROL 内容逗留时间] | `timePlayed` | 整数 | [!UICONTROL 内容逗留时间] 计算主内容中所有“播放”类型事件的事件总时长（以秒为单位）。 |
| [!UICONTROL 媒体逗留时间] | `totalTimePlayed` | 整数 | 描述用户在特定定时媒体资源上花费的总时间，其中包括观看广告所用的时间。 |
| [!UICONTROL 独特播放时间] | `uniqueTimePlayed` | 整数 | 描述用户在定时媒体资源上看到的唯一间隔的总和，即多次查看的播放间隔长度只计算一次。 |
| [!UICONTROL 平均受众访问分钟数] | `averageMinuteAudience` | 数值 | 描述在特定媒体项目上花费的平均内容时间，即花费的总内容时间除以所有播放会话的长度。 |
| [!UICONTROL 广告计数] | `adCount` | 整数 | 播放期间开始的广告数。 |
| [!UICONTROL 章节计数] | `chapterCount` | 整数 | 播放期间开始播放的章节的数量。 |
| [!UICONTROL 10%进度标记] | `hasProgress10` | 布尔值 | 表示播放头通过了基于流长度的10%媒体标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| [!UICONTROL 25%进度标记] | `hasProgress25` | 布尔值 | 表示播放头通过了基于流长度的25%媒体标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| [!UICONTROL 50%进度标记] | `hasProgress50` | 布尔值 | 表示播放头通过了基于流长度的50%媒体标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| [!UICONTROL 75%进度标记] | `hasProgress75` | 布尔值 | 表示播放头通过了基于流长度的75%媒体标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| [!UICONTROL 95%进度标记] | `hasProgress95` | 布尔值 | 表示播放头通过了基于流长度的95%媒体标记。 即使向后搜索，标记也只会计数一次。 如果向前搜索，则不计数跳过的标记。 |
| [!UICONTROL 预计的流] | `estimatedStreams` | 数值 | 每个单独内容片段的估计的视频或音频流数量。 |
| [!UICONTROL 受暂停影响的流] | `hasPauseImpactedStreams` | 布尔值 | 指示在播放单个媒体项目期间是否发生了一次或多次暂停。 |
| [!UICONTROL 暂停事件] | `pauseCount` | 整数 | [!UICONTROL 暂停事件] 计算播放期间发生暂停时段的次数。 |
| [!UICONTROL 暂停总持续时间] | `pauseTime` | 整数 | [!UICONTROL 暂停总持续时间] 描述用户暂停播放的持续时间（秒）。 |
| [!UICONTROL 媒体区段查看次数] | `hasSegmentView` | 布尔值 | [!UICONTROL 媒体区段查看次数] 指示何时查看了至少一个帧（不一定是第一个帧）。 |
| [!UICONTROL 媒体会话服务器超时] | `secondsSinceLastCall` | 数值 | 此 [!UICONTROL 媒体会话服务器超时] 指示用户最后一次已知交互和会话关闭之间经过的时间（以秒为单位）。 |
| [!UICONTROL 内容交付网络] | `cdn` | 字符串 | 此 [!UICONTROL 内容交付网络] 播放的内容的URL编号。 |
| [!UICONTROL Pev3] | `pev3` | 字符串 | [!UICONTROL Pev3] 是用于报表的媒体流的类型。 |
| [!UICONTROL Pccr] | `pccr` | 布尔值 | [!UICONTROL Pccr] 指示已发生重定向。 |

{style="table-layout:auto"}

有关字段组的更多详细信息，请参阅 [公共XDM存储库](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json)

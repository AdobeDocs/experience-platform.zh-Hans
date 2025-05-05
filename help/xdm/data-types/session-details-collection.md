---
title: 会话详细信息收集数据类型
description: 了解会话详细信息收集Experience Data Model (XDM)数据类型。
exl-id: ffe6bcf7-61e1-4f7a-ba95-7fcb78683cc9
source-git-commit: 9350cfc299c20bd63a2a559c177b3af02739e5b9
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 16%

---

# [!UICONTROL 会话详细信息]集合数据类型

[!UICONTROL 会话详细信息]集合是标准的体验数据模型(XDM)数据类型，用于跟踪与媒体播放会话相关的数据。 媒体收集字段用于捕获发送到其他Adobe服务以供进一步处理的数据。 此架构包含大量属性，可用于深入分析用户行为和内容使用模式。 使用[!UICONTROL 会话详细信息]收藏集数据类型通过记录播放事件、广告交互、进度标记、暂停和其他量度来捕获用户参与度。

+++选择以显示会话详细信息收集数据类型的图表。
![会话详细信息集合数据类型的图表。](../images/data-types/session-details-collection.png)
+++

>[!NOTE]
>
>每个显示名称都包含一个链接，指向有关其音频和视频参数的更多信息。 链接的页面包含有关Adobe收集的视频广告数据、实现值、网络参数、报表和重要注意事项的详细信息。

| 显示名称 | 属性 | 数据类型 | 必需 | 描述 |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|----------|---------------------------------------------------------------------------------------|
| [!UICONTROL 广告加载类型] | `adLoad` | 字符串 | 否 | 由每个客户的内部呈现定义的所加载的广告类型。 |
| [[!UICONTROL 相册]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#album) | `album` | 字符串 | 否 | 音乐录音或视频所属的专辑的名称。 |
| [[!UICONTROL 艺人]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#artist) | `artist` | 字符串 | 否 | 执行音乐录制或视频创作的专辑艺术家姓名或组合名称。 |
| [[!UICONTROL 资产ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#asset-id) | `assetID` | 字符串 | 否 | [!UICONTROL 资产ID]是媒体资产内容的唯一标识符，例如电视剧剧集标识符、电影资产标识符或实时事件标识符。 通常，这些ID是从元数据颁发机构（如EIDR、TMS/Gracenote或Rovi）派生的。 这些标识符也可以来自其他专有或内部系统。 |
| [[!UICONTROL 作者]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#author) | `author` | 字符串 | 否 | 媒体作者的姓名。 |
| [[!UICONTROL 广播内容类型]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-type) | `contentType` | 字符串 | 是 | 流投放的[!UICONTROL 广播内容类型]。 每个[!UICONTROL 流类型]的可用值包括：<br>音频：“song”、“podcast”、“audiobook”和“radio”；<br>视频：“VoD”、“Live”、“Linear”、“UGC”和“DVoD”。<br>客户可以为此参数提供自定义值。 |
| [[!UICONTROL 广播网络]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#network) | `network` | 字符串 | 否 | 网络/渠道名称。 |
| [[!UICONTROL 内容渠道]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-channel) | `channel` | 字符串 | 是 | [!UICONTROL 内容频道]是从中播放内容的分发频道。 |
| [!UICONTROL 内容传递网络] | `cdn` | 字符串 | 否 | 已播放内容的[!UICONTROL 内容传递网络]。 |
| [[!UICONTROL 内容ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-id) | `name` | 字符串 | 是 | [!UICONTROL 内容ID]是内容的唯一标识符。 它可用于链接回其他行业或CMS ID。 |
| [[!UICONTROL 内容名称]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-name-(variable)) | `friendlyName` | 字符串 | 否 | [!UICONTROL 内容名称]是内容的“友好”（人类可读）名称。 |
| [[!UICONTROL 内容播放器名称]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-player-name) | `playerName` | 字符串 | 是 | 内容播放器的名称。 |
| [[!UICONTROL 创建者名称]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#originator) | `originator` | 字符串 | 否 | 内容创建者的名称。 |
| [[!UICONTROL 天部分]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#day-part) | `dayPart` | 字符串 | 否 | 一个属性，定义内容在一天中的哪个时间广播或播放。 客户可以视需要为此属性设置任何值 |
| [[!UICONTROL 剧集编号]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#episode) | `episode` | 字符串 | 否 | 剧集的数量。 |
| [[!UICONTROL 馈送类型]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#media-feed-type) | `feed` | 字符串 | 否 | 馈送的类型，可以表示与馈送相关的实际数据（例如EAST HD或SD），也可以表示馈送的来源（例如URL）。 |
| [[!UICONTROL 首次播放日期]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#first-air-date) | `firstAirDate` | 字符串 | 否 | 内容首次在电视上播出的日期。 可接受任何日期格式，但Adobe建议使用如下格式：YYYY-MM-DD。 |
| [[!UICONTROL 首次数字化日期]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#first-digital-date) | `firstDigitalDate` | 字符串 | 否 | 内容首次在任何数字渠道或平台上播出的日期。 可接受任何日期格式，但Adobe建议使用如下格式：YYYY-MM-DD。 |
| [[!UICONTROL 流派]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#genre) | `genre` | 字符串 | 否 | 内容制作者定义的内容类型或分组。 变量实施中的值应以逗号分隔。 |
| [[!UICONTROL 已授权的媒体]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#authorized) | `authorized` | 字符串 | 否 | 确认用户是否已通过Adobe身份验证获得授权。 |
| [[!UICONTROL 媒体内容长度]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-length-(variable)) | `length` | 整数 | 是 | [!UICONTROL 媒体内容长度]包含剪辑长度/运行时间 — 这是所使用内容的最大长度（或持续时间）（以秒为单位）。 |
| [[!UICONTROL MVPD标识符]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#mvpd) | `mvpd` | 字符串 | 否 | 通过Adobe身份验证提供的多通道视频节目分发服务器(MVPD)标识符。 |
| [[!UICONTROL 发布者]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#publisher) | `publisher` | 字符串 | 否 | 音频内容发布者的名称。 |
| [[!UICONTROL 电台]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#station) | `station` | 字符串 | 否 | 播放音频的电台的名称。 |
| [[!UICONTROL 评分值]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-rating) | `rating` | 字符串 | 否 | 由电视节目家长指南定义的评级。 |
| [[!UICONTROL 记录标签]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#label) | `label` | 字符串 | 否 | 记录标签的名称。 |
| [[!UICONTROL 继续]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#content-resumes) | `hasResume` | 布尔值 | 否 | 标记在缓冲、暂停或停滞时间超过 30 分钟后恢复的每次播放。 |
| [[!UICONTROL 季编号]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#season) | `season` | 字符串 | 否 | 节目所属的[!UICONTROL 季编号]。 只有在节目属于某个系列节目的组成部分时，才需要指定“季系列”。 |
| [[!UICONTROL 系列名称]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#show) | `show` | 字符串 | 否 | 节目/系列名称。 只有在节目属于某个系列节目的组成部分时，才需要指定“节目名称”。 |
| [[!UICONTROL 显示类型]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#show-type) | `showType` | 字符串 | 否 | 内容的类型。 例如，预告片或完整剧集。 内容的类型以0到3之间的整数表示。 例如，“0”=全集；“1”=预览/预告片；“2”=剪辑；“3”=其他。 |
| [[!UICONTROL 流格式]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#stream-format) | `streamFormat` | 字符串 | 否 | 流的格式(HD、SD)。 |
| [[!UICONTROL 流类型]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#stream-type) | `streamType` | 字符串 | 否 | 媒体流的类型。 |
| [[!UICONTROL 版本]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html?lang=zh-Hans#sdk-version) | `appVersion` | 字符串 | 否 | 播放器使用的SDK版本。 该参数可使用您的播放器支持的任何自定义值。 |

{style="table-layout:auto"}

---
title: 发送媒体事件
description: 将媒体数据发送到Adobe Experience Platform Edge Network。
source-git-commit: 639d3d3d8bfb51e6c97066aee61271d0b00ec455
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# 发送媒体事件

**[!UICONTROL Send media event]**&#x200B;操作将媒体事件发送到数据流，然后应用程序和服务(如Adobe Experience Platform或Adobe Analytics)可以使用该数据流。 在资产上跟踪流媒体内容时，此操作很有用。

![Experience Platform UI图像显示“发送媒体”事件屏幕。](../assets/send-media-event.png)

可用选项取决于您选择的&#x200B;**[!UICONTROL Media event type]**。 所有媒体事件类型都需要一个&#x200B;**[!UICONTROL Player ID]**，它是内容播放器名称。

某些事件类型提供配置其他字段的功能。 如果此处未列出媒体事件类型，则唯一可用的字段为[!UICONTROL Player ID]。 以下媒体事件类型包含其他字段：

## [!UICONTROL Ad break start]

允许您配置广告面板详细信息。

* **[!UICONTROL Ad break name]**：广告时间的友好名称。
* **[!UICONTROL Ad break offset (seconds)]**：广告时间在内容中的偏移，以秒为单位。
* **[!UICONTROL Ad break index]**：广告时间在内容中的索引，从1开始。

## [!UICONTROL Ad start]

允许您配置广告详细信息。

* **[!UICONTROL Ad name]**：广告的友好名称。
* **[!UICONTROL Ad ID]**：广告的ID。 支持任何字母数字值。
* **[!UICONTROL Ad length (seconds)]**：视频广告的长度，以秒为单位。
* **[!UICONTROL Advertiser]**：广告中展现的产品所属的公司或品牌。
* **[!UICONTROL Campaign ID]**：广告营销活动的ID。
* **[!UICONTROL Creative ID]**：广告创意的ID。
* **[!UICONTROL Creative URL]**：广告创意的URL。
* **[!UICONTROL Placement ID]**：广告的版面ID。
* **[!UICONTROL Site ID]**：广告网站的ID。
* **[!UICONTROL Pod position]**：父广告时间内的广告索引，从0开始。

此事件类型还支持将自定义元数据作为媒体事件有效负载的一部分提供的功能。

## [!UICONTROL Bitrate change]

* **[!UICONTROL Quality of experience data]**： [体验质量](/help/xdm/data-types/qoe-data-details-collection.md)对象，它指定比特率、丢帧、每秒帧数和开始时间。

## [!UICONTROL Chapter start]

用于配置章节详细信息。

* **[!UICONTROL Chapter name]**：章节或区段的名称。
* **[!UICONTROL Chapter length]**：章节的长度，以秒为单位。
* **[!UICONTROL Chapter index]**：章节在内容中的位置。
* **[!UICONTROL Chapter offset]**：章节从内容开始的偏移，以秒为单位。

此事件类型还支持将自定义元数据作为媒体事件有效负载的一部分提供的功能。

## [!UICONTROL Error]

允许您配置错误详细信息。

* **[!UICONTROL Error name]**：错误名称。
* **[!UICONTROL Source]**：错误的来源。

## [!UICONTROL Session start]

用于配置媒体会话详细信息。

* **[!UICONTROL Handle media session automatically]**：允许Web SDK自动发送必要Ping的复选框。 如果要自己手动发送ping，可以取消选中此框。
* **[!UICONTROL Playhead]**：播放头，以秒为单位。
* **[!UICONTROL Content type]**：内容类型。 支持任何字符串值；Adobe还提供了以下预设：
   * [!UICONTROL Audiobook]
   * [!UICONTROL Downloaded video-on-demand]
   * [!UICONTROL Linear playback of the media asset]
   * [!UICONTROL Live streaming]
   * [!UICONTROL Podcast]
   * [!UICONTROL Radio show]
   * [!UICONTROL Song]
   * [!UICONTROL User-generated content]
   * [!UICONTROL Video-on-demand]
* **[!UICONTROL Clip length/runtime (seconds)]**：正在使用的内容的最长持续时间（以秒为单位）。 对于持续时间未知的实时媒体，默认值为`86400`值。
* **[!UICONTROL Content ID]**：内容的内容ID。
* **[!UICONTROL Ad load type]**：加载的广告类型。 支持以下两个值：
   * [!UICONTROL Ads same as TV]
   * [!UICONTROL Other (custom/dynamic ads)]
* **[!UICONTROL Album]**：歌曲所属的专辑。
* **[!UICONTROL Artist]**：歌曲的歌手。
* **[!UICONTROL Asset ID]**：媒体资源内容的唯一标识符。 这些ID通常派生自元数据颁发机构，如EIDR、TMS/Gracenote或Rovi。 这些标识符也可以来自其他专有或内部系统。
* **[!UICONTROL Author]**：有声读物的作者姓名。
* **[!UICONTROL Authorized]**：确定用户是否通过Adobe身份验证登录的标志。
* **[!UICONTROL Day part]**：一天中广播或播放内容的时间。 支持任何字符串值。
* **[!UICONTROL Episode]**：剧集编号。
* **[!UICONTROL Feed type]**：馈送的类型。
* **[!UICONTROL First air date]**：内容首次在电视上播出的日期。 支持任何字符串值；但是，Adobe建议使用格式`YYYY-MM-DD`。
* **[!UICONTROL First digital date]**：内容首次在任何数字渠道或平台上播出的日期。 支持任何字符串值；但是，Adobe建议使用格式`YYYY-MM-DD`。
* **[!UICONTROL Content name]**：内容的友好名称。
* **[!UICONTROL Genre]**：内容制作者定义的内容类型或分组。 此字段支持多个值，并以逗号分隔。
* **[!UICONTROL Label]**：记录标签的名称。
* **[!UICONTROL Rating]**：由电视节目家长指南定义的评级。
* **[!UICONTROL MVPD]**：由Adobe身份验证提供的MVPD。
* **[!UICONTROL Network]**：网络或通道名称。
* **[!UICONTROL Originator]**：内容的创建者。
* **[!UICONTROL Publisher]**：音频内容发布者。
* **[!UICONTROL Season]**：如果该节目属于某个系列，则为节目的季编号。
* **[!UICONTROL Show]**：如果该节目属于某个系列，则为系列名称。
* **[!UICONTROL Show type]**：节目类型。 支持任何字符串值；Adobe还提供了以下预设：
   * [!UICONTROL Clip]
   * [!UICONTROL Full episode]
   * [!UICONTROL Other]
   * [!UICONTROL Preview/trailer]
* **[!UICONTROL Stream type]**：流类型。
* **[!UICONTROL Stream format]**：流的格式，如HD或SD。
* **[!UICONTROL Station]**：广播电台名称或ID。

此事件类型还支持将自定义元数据作为媒体事件有效负载的一部分提供的功能。 它还允许数据流配置覆盖，从而让您能够控制哪些应用程序和服务接收此数据。 当在单个命令和标记扩展配置设置中设置数据流配置覆盖时，单个命令优先。 有关详细信息，请参阅[数据流配置覆盖](../configure/configuration-overrides.md)。

## [!UICONTROL States update]

允许您配置状态更新详细信息。 您可以开始或结束以下状态：

* [!UICONTROL Closed captioning]
* [!UICONTROL Full screen]
* [!UICONTROL In focus]
* [!UICONTROL Mute]
* [!UICONTROL Picture in picture]

以下字段可用：

* **[!UICONTROL States started]**：下拉菜单，用于指示状态已开始。 选择&#x200B;**[!UICONTROL Add another state that started]**&#x200B;按钮允许您在同一操作中启动多个状态。
* **[!UICONTROL States ended]**：一个下拉菜单，可让您指示状态已结束。 选择&#x200B;**[!UICONTROL Add another state that ended]**&#x200B;按钮允许您在同一操作中结束多个状态。

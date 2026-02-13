---
title: 流媒体配置设置
description: 自定义Web SDK标记扩展收集流媒体数据的方式。
exl-id: f486d729-b7ad-4720-8399-71495cb9c57e
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 3%

---

# 流媒体配置设置 {#streaming-media}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_streamingmedia"
>title="流媒体"
>abstract="确定在媒体播放会话期间如何收集流媒体数据。"

媒体收集功能可帮助您收集与媒体会话相关的数据，例如媒体回放、暂停、结束和其他相关事件。 收集之后，您可以将此数据发送到Adobe Experience Platform或Adobe Analytics以生成报表。 此功能为跟踪和了解您网站上的媒体消费行为提供了全面的解决方案。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL Extensions]**，然后在&#x200B;**[!UICONTROL Configure]**&#x200B;信息卡上选择[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下滚动到&#x200B;**[!UICONTROL Streaming media]**&#x200B;部分。

![在标记UI中显示Web SDK标记扩展的媒体收集设置的图像](../assets/media-collection.png)

## 先决条件

要使用Web SDK的流媒体组件，您必须满足以下先决条件：

* 确保您有权访问Adobe Experience Platform或Adobe Analytics。
* 为您正在使用的数据流启用&#x200B;**[[!UICONTROL Media Analytics]](/help/datastreams/configure.md#advanced-options)**&#x200B;选项。
* 确保数据流使用的架构包括媒体收集架构字段。
* 在Web SDK标记扩展中配置流媒体功能，如本页所示。

## [!UICONTROL Channel]

发生媒体收集的渠道的名称。 例如：`Video channel`。任何字符串值都有效。

## [!UICONTROL Player Name]

资产用于媒体播放的媒体播放器的名称。

## [!UICONTROL Application Version]

您的资产用于媒体播放的媒体播放器应用程序的版本。

## [!UICONTROL Main ping interval]

主内容Ping的频率（以秒为单位）。 默认值为 `10`。值可以介于`10`到`50`秒之间。 如果未指定值，则在使用[自动跟踪的会话](/help/collection/js/commands/createmediasession.md#automatic)时使用默认值。

## [!UICONTROL Ad ping interval]

广告内容的Ping频率（以秒为单位）。 默认值为 `10`。值可以介于`1`到`10`秒之间。 如果未指定值，则在使用[自动跟踪的会话](/help/collection/js/commands/createmediasession.md#automatic)时使用默认值。

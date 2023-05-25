---
title: Assurance中的适用于流媒体的 Adobe Analytics视图
description: 本指南介绍如何将适用于流媒体的 Adobe Analytics与Adobe Experience Platform Assurance结合使用。
exl-id: 9a9c2c64-e9ed-4d58-b936-d802f1c3b7d3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 2%

---

# Assurance中的适用于流媒体的 Adobe Analytics视图

通过适用于流媒体的 Adobe Analytics与Adobe Experience Platform Assurance之间的集成，您现在可以在移动设备应用程序中验证Media Analytics实施。 Media Analytics视图会显示媒体会话中跟踪的内容，例如：

- 会话开始事件，包含所有内容核心、标准元数据和自定义元数据属性以及会话结束和会话结束事件。
- 附加了所有广告属性的广告时间开始和广告开始事件，以及两者的跳过和完成事件。
- 章节开始并附加所有属性，以及章节跳过和章节结束事件。
- 所有播放更改事件（播放、暂停、缓冲、错误、比特率更改）。
- 所有播放器状态更改跟踪事件（开始、结束）。

在Analytics中处理数据后，后处理状态和数据（如媒体逗留时间和总暂停持续时间）也可在事件详细信息视图中找到。

## 快速入门

在继续之前，请确保您拥有以下服务：

- 此 [Adobe Experience Platform数据收集UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

要了解如何在应用程序中安装Assurance，请阅读 [实施Assurance指南](../tutorials/implement-assurance.md).

## 在适用于流媒体的 Adobe Analytics中使用Assurance

在为Adobe Analytics连接并设置应用程序后，便可以为Streaming Media Analytics配置应用程序。 在左侧面板底部，选择 **[!UICONTROL 配置]** 添加Media Analytics事件视图和 **保存** 它。

![配置](./images/adobe-analytics-streaming-media/configure.png)

添加后，选择 **[!UICONTROL Media Analytics事件]** 在中查看 **[!UICONTROL Adobe Analytics]** 部分，以验证会话跟踪。

![选择](./images/adobe-analytics-streaming-media/select.png)

在 **[!UICONTROL Media Analytics事件]** 您可以按会话ID (VSID)进行搜索和过滤，以查看特定的媒体会话。 要查看其他事件详细信息，请选择特定事件。

![媒体事件](./images/adobe-analytics-streaming-media/media-events.png)

为了更简洁地查看API调用，您还可以通过选择 **[!UICONTROL 隐藏播放头更新事件]** 筛选条件。

![隐藏播放头](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>查看后处理的媒体分析数据需要使用SDK版本：Android Media 2.1.2和iOS AEPMedia 3.0.1（或更高版本）

要查看处理后的数据，请找到会话开始事件，并在状态列中验证会话已完成。 如果完成，请单击事件以在事件详细信息视图中查看媒体会话摘要。 有关更多详细信息，请向下滚动以查找处理后的详细信息。

![后处理视图](./images/adobe-analytics-streaming-media/post-processed-view.png)

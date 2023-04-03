---
title: 适用于流媒体的 Adobe Analytics在保证中的视图
description: 本指南介绍如何将适用于流媒体的 Adobe Analytics与Adobe Experience Platform Assurance结合使用。
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 1%

---


# 适用于流媒体的 Adobe Analytics保障视图

通过适用于流媒体的 Adobe Analytics与Adobe Experience Platform保证之间的集成，您现在可以在移动设备应用程序中验证Media Analytics实施。 Media Analytics视图显示媒体会话中跟踪的内容，例如：

- 会话开始事件，其中包含所有内容核心、标准元数据和自定义元数据属性，以及会话结束事件和会话结束事件。
- 附加了所有广告属性的广告时间开始事件和广告开始事件，以及两者的跳过和结束事件。
- 章节开始，其中包含所有属性，以及章节跳过和章节结束事件。
- 所有播放更改事件（播放、暂停、缓冲、错误、比特率更改）。
- 所有播放器状态更改跟踪事件（开始、结束）。

在Analytics中处理数据后，后处理状态和数据（如媒体逗留时间和暂停总持续时间）也会在事件详细信息视图中可用。

## 快速入门

在继续操作之前，请确保您具有以下服务：

- 的 [Adobe Experience Platform数据收集UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform保障](https://experience.adobe.com/assurance)

要了解如何在应用程序中安装保障，请阅读 [实施保证指南](../tutorials/implement-assurance.md).

## 对适用于流媒体的 Adobe Analytics使用保证

连接并设置Adobe Analytics应用程序后，便可以为流媒体分析配置它。 在左侧面板的底部，选择 **[!UICONTROL 配置]** 添加Media Analytics“事件”视图和 **保存** 它。

![配置](./images/adobe-analytics-streaming-media/configure.png)

添加后，选择 **[!UICONTROL Media Analytics事件]** 视图 **[!UICONTROL Adobe Analytics]** 部分以验证会话跟踪。

![选择](./images/adobe-analytics-streaming-media/select.png)

在 **[!UICONTROL Media Analytics事件]** 查看时，您可以按会话ID(VSID)搜索和过滤，以查看特定的媒体会话。 要查看其他事件详细信息，请选择一个特定事件。

![媒体事件](./images/adobe-analytics-streaming-media/media-events.png)

对于API调用的更简洁视图，您还可以通过选择 **[!UICONTROL 隐藏播放头更新事件]** 过滤器。

![隐藏播放头](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>查看处理后的媒体分析数据需要使用SDK版本：Android Media 2.1.2和iOS AEPMedia 3.0.1（或更高版本）

要查看后处理的数据，请查找会话开始事件并在状态列中验证会话是否已完成。 如果完成，请单击事件以在事件详细信息视图中查看媒体会话摘要。 有关更多详细信息，请向下滚动以查找后处理的详细信息。

![后处理视图](./images/adobe-analytics-streaming-media/post-processed-view.png)

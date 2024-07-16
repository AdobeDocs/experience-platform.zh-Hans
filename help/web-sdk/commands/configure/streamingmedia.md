---
title: 流媒体
description: 配置Web SDK以收集与您Web资产上的媒体使用情况相关的数据。
exl-id: f7733619-d35e-43eb-ac90-052717310c39
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 6%

---

# `streamingMedia`

`streamingMedia`组件可帮助您收集与网站上的媒体会话相关的数据。

收集的数据可以包括有关媒体回放、暂停、完成和其他相关事件的信息。 收集之后，您可以将此数据发送到Adobe Experience Platform和/或Adobe Analytics以生成报表。 此功能为跟踪和了解您网站上的媒体消费行为提供了全面的解决方案。

## 先决条件 {#prerequisites}

要使用Web SDK的`streamingMedia`组件，您必须满足以下先决条件：

* 确保您有权访问Adobe Experience Platform和/或Adobe Analytics。
* 您必须使用Web SDK版本2.20.0或更高版本。 请参阅[Web SDK安装概述](../../install/overview.md)，了解如何安装最新版本。
* 为您正在使用的数据流启用&#x200B;**[[!UICONTROL Media Analytics]](../../../datastreams/configure.md#advanced-options)**&#x200B;选项。
* 确保数据流使用的架构包括媒体收集架构字段。
* 通过[标记扩展](#tag-extension)或通过[JavaScript库](#library)在Web SDK配置中配置流媒体功能，如本页所示。

## 使用Web SDK标记扩展配置流媒体 {#tag-extension}

要在Web SDK标记扩展中配置流媒体，请执行以下步骤。

1. 使用您的Adobe ID凭据登录[experience.adobe.com](https://experience.adobe.com)。
1. 导航到&#x200B;**[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**。
1. 选择所需的标记属性。
1. 导航到&#x200B;**[!UICONTROL 扩展]**，然后单击[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 配置]**。
1. 按照[Web SDK标记扩展配置页面](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection)中的说明配置&#x200B;**[!UICONTROL 流媒体]**&#x200B;设置。

## 使用Web SDK JavaScript库配置流媒体 {#library}

要在Web SDK中配置流媒体，请使用下面描述的属性。

调用`configure`命令时，添加`streamingMedia`对象。

```js
alloy("configure", {
    streamingMedia: {
        channel: "video channel",
        playerName: "test player",
        appVersion: "Media Analytics with Web SDK 2.20.0",
        mainPingInterval: 10,
        adPingInterval: 10
    }
});
```

| 属性 | 类型 | 必需 | 描述 |
|---------|----------|---------|---------|
| `channel` | 字符串 | 是 | 发生流媒体收集的渠道的名称。 示例：`Video channel`。 |
| `playerName` | 字符串 | 是 | 媒体播放器的名称。 |
| `appVersion` | 字符串 | 否 | 媒体播放器应用程序的版本。 |
| `mainPingInterval` | 整数 | 否 | 主内容Ping的频率（以秒为单位）。 默认值为 `10`。值可以介于`10`到`50`秒之间。  如果未指定值，则在使用[自动跟踪的会话](../createmediasession.md#automatic)时使用默认值。 |
| `adPingInterval` | 整数 | 否 | 广告内容的Ping频率（以秒为单位）。 默认值为 `10`。值可以介于`1`到`10`秒之间。 如果未指定值，则在使用[自动跟踪的会话](../createmediasession.md#automatic)时使用默认值。 |

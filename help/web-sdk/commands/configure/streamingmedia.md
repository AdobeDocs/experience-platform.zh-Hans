---
title: media收藏集
description: 配置Web SDK以收集与您Web资产上的媒体使用情况相关的数据。
source-git-commit: 1d1bb754769defd122faaa2160e06671bf02c974
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 6%

---


# `streamingMedia`

此 `streamingMedia` 组件可帮助您收集与网站上的媒体会话相关的数据。

收集的数据可以包括有关媒体回放、暂停、完成和其他相关事件的信息。 收集之后，您可以将此数据发送到Adobe Experience Platform和/或Adobe Analytics以生成报表。 此功能为跟踪和了解您网站上的媒体消费行为提供了全面的解决方案。

## 先决条件 {#prerequisites}

要使用 `streamingMedia` 组件，您必须满足以下先决条件：

* 确保您有权访问Adobe Experience Platform和/或Adobe Analytics。
* 您必须使用Web SDK版本2.20.0或更高版本。 请参阅 [Web SDK安装概述](../../install/overview.md) 了解如何安装最新版本。
* 启用 **[[!UICONTROL 媒体分析]](../../../datastreams/configure.md#advanced-options)** 选项。
* 确保数据流使用的架构包括媒体收集架构字段。
* 在Web SDK配置中配置流媒体功能，如本页所示，通过 [标记扩展](#tag-extension) 或通过 [JavaScript库](#library).

## 使用Web SDK标记扩展配置流媒体 {#tag-extension}

要在Web SDK标记扩展中配置流媒体，请执行以下步骤。

1. 登录 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID凭据。
1. 导航到 **[!UICONTROL 数据收集]** > **[!UICONTROL 标记]**.
1. 选择所需的标记属性。
1. 导航到 **[!UICONTROL 扩展]**，然后单击 **[!UICONTROL 配置]** 在 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 配置 **[!UICONTROL 流媒体]** 设置，如 [Web SDK标记扩展配置页面](../../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#media-collection).

## 使用Web SDK JavaScript库配置流媒体 {#library}

要在Web SDK中配置流媒体，请使用下面描述的属性。

调用时 `configure` 命令，添加 `streamingMedia` 对象。

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
| `mainPingInterval` | 整数 | 否 | 主内容Ping的频率（以秒为单位）。 默认值为 `10`。值可以介于 `10` 到 `50` 秒。  如果未指定值，则在使用 [自动跟踪的会话](../createmediasession.md#automatic). |
| `adPingInterval` | 整数 | 否 | 广告内容的Ping频率（以秒为单位）。 默认值为 `10`。值可以介于 `1` 到 `10` 秒。 如果未指定值，则在使用 [自动跟踪的会话](../createmediasession.md#automatic). |

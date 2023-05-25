---
title: Assurance中的Adobe Analytics视图
description: 本指南介绍如何将Adobe Analytics与Adobe Experience Platform Assurance结合使用。
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 3%

---

# Assurance中的Adobe Analytics视图

Adobe Experience Platform保障与Adobe Analytics的集成为用户调试和验证其Adobe Analytics实施提供了更丰富的SDK事件视图。 Adobe Analytics该视图现在显示生命周期和操作/状态事件，这些事件是从 [ADOBE EXPERIENCE PLATFORM SDK](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/). 该视图还具有“响应”详细信息，其中提供了在应用每个报表包的处理规则后如何处理事件的信息。

![](./images/adobe-analytics/overview.png)

## 快速入门

在继续之前，请确保您拥有以下服务：

- 此 [Adobe Experience Platform数据收集UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

要了解如何在应用程序中安装Assurance，请阅读 [实施Assurance指南](../tutorials/implement-assurance.md).

## 后处理状态

在SDK通过Adobe Analytics发出网络请求后，状态将告知您Assurance是否能够检索Adobe Analytics请求的后处理信息。

请注意，为了检索后处理信息，登录用户必须有权访问相应的报表包。

| 状态 | 描述 |
| :----- | :---------- |
| `Queued` | 网络请求正在获取后处理信息。 |
| `Processed` | 网络请求成功，并接收后处理信息。 |
| `Delayed` | 已超过重试获取后处理信息的最大请求数。 |
| `Error` | 错误导致网络请求失败。 有关错误的更多详细信息将显示在事件详细信息视图中。 |
| `Unauthorized` | 用户无权访问Adobe Analytics报表包。 |
| `Unavailable` | Adobe Analytics请求没有相应的 `AnalyticsResponse` 事件。 |
| `No Debug Flag` | 当前的Adobe Analytics或Assurance SDK版本可能不支持Analytics调试功能。 欲知更多信息，请阅读 [疑难解答指南](../troubleshooting.md). |
| `Expired` | 此 `AnalyticsTrack` 或 `LifecycleStart` 事件早于24小时。 |

## 事件详细信息视图

对于Analytics跟踪事件，详细视图包含以下重要部分：

- 发起的SDK Analytics请求事件。
- 来自请求的OOTB元和上下文数据，例如报表包ID、SDK扩展版本、OOTB上下文数据等。
- 有关Analytics事件的后处理信息，包含revar、evar、prop等的映射。

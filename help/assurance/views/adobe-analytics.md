---
title: Assurance 中的 Adobe Analytics 视图
description: 本指南介绍如何将 Adobe Analytics 与 Adobe Experience Platform Assurance 配合使用。
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 100%

---

# Assurance 中的 Adobe Analytics 视图

Adobe Experience Platform Assurance 与 Adobe Analytics 集成为调试和验证其 Adobe Analytics 实施的用户提供一个内容更丰富的 SDK 事件视图。该视图现在显示从 [Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/) 发送到 Adobe Analytics 的生命周期和操作/状态事件。该视图还列举“响应”详细信息，其中提供在应用每个报表包的处理规则后如何处理事件的信息。

![](./images/adobe-analytics/overview.png)

## 快速入门

在继续之前，请确保您拥有以下服务：

- [Adobe Experience Platform 数据收藏集 UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

要了解如何在您的应用程序中安装 Assurance，请阅读[实施 Assurance 指南](../tutorials/implement-assurance.md)。

## 后处理状态

当 SDK 向 Adobe Analytics 提出网络请求后，该状态将告知 Assurance 是否曾经能够检索该 Adobe Analytics 请求的后处理信息。

请注意，若要检索后处理信息，已登录的用户必须有权访问相应的报表包。

| 状态 | 描述 |
| :----- | :---------- |
| `Queued` | 网络请求正在获取后处理信息。 |
| `Processed` | 该网络请求取得成功，并收到后处理信息。 |
| `Delayed` | 已超出获取后处理信息的最大请求重试次数。 |
| `Error` | 某个错误导致该网络请求失败。在事件详细信息视图中显示关于该错误的更多详细信息。 |
| `Unauthorized` | 用户无权访问该 Adobe Analytics 报表包。 |
| `Unavailable` | Adobe Analytics 请求没有相应的 `AnalyticsResponse` 事件。 |
| `No Debug Flag` | 当前的 Adobe Analytics 或 Assurance SDK 版本可能不支持 Analytics 调试功能。有关详细信息，请阅读[故障排除指南](../troubleshooting.md)。 |
| `Expired` | `AnalyticsTrack` 或 `LifecycleStart` 事件发生时间超过 24 小时。 |

## 事件详细信息视图

对于 Analytics 跟踪事件，详细视图包含以下几个有用的部分：

- 原始 SDK Analytics 请求事件。
- 来自该请求的 OOTB 元和上下文数据，例如报表包 ID、SDK 扩展版本、OOTB 上下文数据等。
- 有关 Analytics 事件的后处理信息，其中包含 revar、evar、prop 等的映射。

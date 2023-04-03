---
title: Adobe Analytics在保证中的视图
description: 本指南介绍如何将Adobe Analytics与Adobe Experience Platform Assurance结合使用。
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 2%

---


# Adobe Analytics保障视图

与Adobe Analytics的Adobe Experience Platform保障集成为用户调试和验证其Adobe Analytics实施提供了更丰富的SDK事件视图。 该视图现在显示从 [Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/). 该视图还提供了“响应”详细信息，以提供有关在应用每个报表包的处理规则之后如何处理事件的信息。

![](./images/adobe-analytics/overview.png)

## 快速入门

在继续操作之前，请确保您具有以下服务：

- 的 [Adobe Experience Platform数据收集UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform保障](https://experience.adobe.com/assurance)

要了解如何在应用程序中安装保障，请阅读 [实施保证指南](../tutorials/implement-assurance.md).

## 后处理状态

在SDK通过Adobe Analytics发出网络请求后，状态将告知您保证是否可以检索Adobe Analytics请求的后处理信息。

请注意，为了检索后处理信息，登录用户必须有权访问相应的报表包。

| 状态 | 描述 |
| :----- | :---------- |
| `Queued` | 网络请求正在获取后处理信息。 |
| `Processed` | 网络请求成功，并收到后处理信息。 |
| `Delayed` | 已超出获取后处理信息的请求重试的最大次数。 |
| `Error` | 错误导致网络请求失败。 有关该错误的更多详细信息显示在事件详细信息视图中。 |
| `Unauthorized` | 用户无权访问Adobe Analytics报表包。 |
| `Unavailable` | Adobe Analytics请求没有对应的 `AnalyticsResponse` 事件。 |
| `No Debug Flag` | 当前的Adobe Analytics或保证SDK版本可能不支持Analytics调试功能。 欲知更多信息，请阅读 [疑难解答指南](../troubleshooting.md). |
| `Expired` | 的 `AnalyticsTrack` 或 `LifecycleStart` 事件超过24小时。 |

## 事件详细信息视图

对于Analytics跟踪事件，详细视图包含以下有用部分：

- 原始SDK Analytics请求事件。
- 来自请求的OOTB元和上下文数据，如报表包ID、SDK扩展版本、OOTB上下文数据，等等。
- 有关Analytics事件的后处理信息，该事件包含revar、evar、prop等的映射。

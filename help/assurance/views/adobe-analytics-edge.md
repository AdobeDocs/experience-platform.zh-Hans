---
title: Analytics Events 2.0 in Assurance
description: 本指南介绍如何将Adobe Analytics和Analytics Edge视图与Adobe Experience Platform Assurance结合使用。
badgeBeta: label="Beta 版" type="Informative"
exl-id: faaa2c1d-3471-4d86-9a25-03265b996e31
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 19%

---

# Analytics Events 2.0 in Assurance

Analytics Events 2.0为用户调试和验证其Adobe Analytics实施提供了更丰富的SDK事件视图。 该视图显示从[Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/solution/adobe-analytics/)以及[Adobe Experience PlatformEdge NetworkSDK](https://developer.adobe.com/client-sdks/edge/edge-network/)发送到Adobe Analytics的事件。 该视图还具有一个详细信息面板，该面板提供了客户端SDK处理事件的方式，以及在事件离开设备后上游服务处理该事件的方式。

## 快速入门

要使用此视图，请完成以下步骤：

1. [设置Adobe Experience Platform保证](../tutorials/implement-assurance.md)。
2. [创建并连接到保证会话](../tutorials/using-assurance.md)。
3. 在左侧导航&#x200B;**主页**&#x200B;视图菜单中的Assurance UI中，选择&#x200B;**Analytics Events 2.0 (Beta)**。 如果未看到此选项，请选择窗口左下角的&#x200B;**配置**，添加&#x200B;**Analytics Events 2.0 (Beta)**，然后选择&#x200B;**保存**。

## Analytics事件视图

如果您使用的是&#x200B;**Adobe Analytics**&#x200B;移动扩展，请使用Analytics事件视图。 此视图允许您轻松查看从连接的客户端发送的Analytics事件，包括跟踪操作、跟踪状态和生命周期事件。 通过选择表中的Analytics事件之一，可以在右侧面板上查看有关如何处理该事件的详细信息。

![展示Analytics事件视图中不同组件的图像。](./images/adobe-analytics-edge/analytics-events.png)

### 后处理状态

在SDK通过Adobe Analytics发出网络请求后，状态将告知您保障是否能够检索Adobe Analytics请求的后处理信息。 在触发请求后，当后处理状态为操作状态时，Analytics事件视图必须保持活动状态。

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

### 事件详细信息视图

对于Analytics跟踪事件，详细视图包含以下部分：

- 原始 SDK Analytics 请求事件。
- 请求中的元和上下文数据，例如报表包ID、SDK扩展版本和上下文数据。
- Post处理的有关Analytics事件的信息，其中包含常量、evar和prop的映射。

### Analytics视图验证

验证视图可让您轻松查看与Analytics相关的验证脚本的结果。 验证器显示的错误可能包含指向应修复错误的链接或显示处于错误状态的事件。

![显示Analytics视图中的“验证器”选项卡的图像。](./images/adobe-analytics-edge/analytics-validation-view.png)

## Analytics Edge视图

如果您使用的是&#x200B;**Edge Network**&#x200B;或&#x200B;**Edge Bridge**&#x200B;移动扩展，请使用Analytics Edge视图。 要启用此视图，请选择右上角的“Analytics Edge (Beta)”切换开关，以查看在当前会话中通过Edge网络发送的Analytics事件。 这包括生命周期扩展触发的所有事件、Edge请求和/或Edge Bridge事件（基于跟踪操作和跟踪状态）。

![显示用于在Analytics视图和Analytics Edge视图之间进行切换的切换的图像。](./images/adobe-analytics-edge/analytics-view-toggle.png)

Analytics Edge视图包含有关客户端调度的与Analytics相关的Edge请求和生命周期方法的信息。 通过在列表中选择一个事件，右侧面板会显示客户端SDK以及上游服务在离开设备后处理的事件，以便您轻松查看由调用产生的事件链。

![展示Analytics Edge视图中各个组件的图像。](./images/adobe-analytics-edge/edge-analytics-events.png)

### Analytics Edge验证

通过Analytics Edge验证视图，您可以轻松查看与Analytics Edge相关的验证脚本的结果。 验证器显示的错误可能包含指向应修复错误的链接或显示处于错误状态的事件。

![在Analytics Edge视图中显示“验证器”选项卡的图像。](./images/adobe-analytics-edge/edge-analytics-validation-view.png)

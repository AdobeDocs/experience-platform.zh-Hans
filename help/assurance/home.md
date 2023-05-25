---
title: Adobe Experience Platform保障概述
description: Adobe Experience Platform Assurance 可帮助您检查、证明、模拟和验证您在移动应用程序中收集数据或提供体验的方式。
exl-id: e887f5f6-3db0-4521-be2d-20ef3d08e7d0
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 4%

---

# Adobe Experience Platform Assurance

Adobe Experience Platform Assurance是以下产品之一 [Adobe Experience Cloud](https://www.adobe.com/cn/experience-cloud.html) 帮助您检查、验证、模拟和验证在移动应用程序中收集数据或提供体验的方式。

>[!IMPORTANT]
>
> Project Griffon现在称为 **Assurance**！
>
> Griffon项目现在通常可用于 **所有** Adobe Experience Cloud客户作为保证。 要了解有关此过渡的更多信息，请阅读 [用户访问指南](./user-access.md).

>[!INFO]
>
>Assurance Public API可用！
>
>[保证API](https://developer.adobe.com/adobe-assurance-public-apis/) 是一组API，这些API使用户能够在安装Adobe保障Mobile SDK后测试和调试其Web和移动设备应用程序。

## 正式发布

从2022年10月15日开始，Assurance已正式向所有Adobe Experience Cloud提供。

### 哪些方面发生了变化？

10月15日 — 对Assurance的访问将通过Admin Console进行管理。 请阅读 [用户访问指南](./user-access.md) 以确保您能够继续不间断地访问。

预计现有Assurance集成、会话和事件不会发生其他更改或中断。 可以继续通过以下方式访问保证 [https://griffon.adobe.com](https://griffon.adobe.com) **或** 您可以使用（和书签） [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance).

## Assurance可以为您做什么？

### 快速设置

使用几行代码快速入门。 对于移动应用程序，Assurance可与Adobe Experience Platform Mobile SDK配合使用，帮助您检查、模拟和验证应用程序事件、位置信号、配置参数、SDK日志、设备信息等。

### 轻松连接

使用Assurance，将您的应用程序与Platform连接起来既简单又可靠。 您不需要使用网络代理， [MiTM](https://en.wikipedia.org/wiki/Man-in-the-middle_attack))，以及其他网络体操 — 将您的应用程序连接到Assurance就像扫描二维码或点击按钮一样简单。

![](./images/index/no-hassle-connection.png)

### 实时检查、模拟和验证

连接到Assurance后，您可以检查实时流式传输的应用程序事件和活动，并进行过滤和搜索以消除噪音。 事件包含有关验证、调试和疑难解答您的移动应用程序实施的详细信息。 Assurance还可让您实时获取屏幕快照、模拟位置信号等。

![](./images/index/real-time-insepction.png)

### 与Adobe Experience Cloud集成

用户如何在以营销人员为中心的用户界面中设置报告规则、活动和营销活动，从而为客户端数据和体验提供上下文。 为了帮助您连接这两者之间的点，我们与Adobe Experience Cloud解决方案(如Adobe Experience Platform、Adobe Analytics、Adobe Target、Places Service等)集成。

![](./images/index/integration.png)

## 功能

### Adobe Experience Platform Mobile SDK事件、日志等

Assurance可帮助您检查Adobe Experience Platform Mobile SDK生成的原始SDK事件。 SDK收集的所有事件均可供检查。 SDK事件会加载到列表视图中，并按时间排序。 每个事件都有一个详细视图，其中提供了更多详细信息。 还提供了用于浏览SDK配置、数据元素、共享状态和SDK扩展版本的其他视图。

### Adobe Analytics

Adobe Analytics > Analytics事件视图是一个重点视图，其中显示与Adobe Analytics移动实施相关的事件。 列表视图以特别格式化的视图显示生命周期或操作/状态事件、后处理的“状态”以及所需的事件详细信息。 “后处理”状态显示Adobe Analytics在对该事件应用处理规则后如何处理该事件。

### 适用于流媒体的 Adobe Analytics

“Adobe Analytics”>“Media Analytics事件”视图可显示音频和视频分析实施的事件。 事件详细信息视图显示为每个播放会话跟踪的标准元数据和自定义元数据。 此外，您还可以查看后处理的状态和后处理的媒体分析数据，如媒体逗留时间或缓冲总持续时间。

### 地点（位置服务）

Location Services视图是一个设备上视图，该视图显示用户位置进入和退出事件以方便验证。 此方便易用的视图提供了一个便利的界面，用于在客户端上查看位置特定的数据点以进行上下文调试。

## Assurance是否安全？

保证已采取以下安全措施：

* Assurance和Assurance Web UI都有一个基于PIN的安全握手用于连接。 用户必须明确创建握手，以防止最终用户创建“意外”保证连接。
* 仅支持属于同一Adobe Experience Cloud组织ID的Assurance和Assurance Web UI之间的连接。
* Adobe Experience Platform Mobile SDK事件通过HTTPS进行传输。
* Assurance和Adobe Experience Platform Mobile SDK使用TLS 1.2
* 保障会话将在30天后删除。
* 按照存储最佳实践，确保会话数据在静态状态下加密。

## 快速入门

要设置Assurance，您需要先在应用程序中安装Assurance扩展。 要了解如何执行此操作，请阅读的教程 [实施Assurance扩展](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

将Assurance添加到应用程序后，您可以创建一个可连接到设备的保证会话。 要了解如何使用Assurance，请阅读 [使用Assurance指南](./tutorials/using-assurance.md).

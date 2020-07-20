---
title: Adobe Experience PlatformWeb SDK帮助
seo-title: Adobe Experience PlatformWeb SDK帮助
description: 了解什么是Adobe Experience PlatformWeb SDK以及如何使用它。
seo-description: 允许Adobe Experience Cloud客户与Experience Cloud中的各种服务进行交互。
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---


# 什么是Adobe Experience PlatformWeb SDK

Adobe Experience PlatformWeb SDK是客户端JavaScript库，允许Adobe Experience Cloud客户通过Adobe与中的各种服 [!DNL Experience Cloud] 务交互 [!DNL Experience Platform Edge Network]。

以下视频概述了Adobe Experience Platform [!DNL Web SDK] 和 [!DNL Edge Network]。

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK被Adobe Experience PlatformWeb SDK所取代

Adobe Experience PlatformWeb SDK替换以下SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

这不仅仅是现有库的包装。 这完全是重写。 其目的是通过以下方式结束挑战：以正确的顺序触发标记、与库版本控制挑战不一致以及更好地进行依赖管理。 它是一种新的实现方式， [!DNL Experience Cloud] 是开放源 [码的实现](https://github.com/adobe/alloy)。

除了新的库，还有一个新的端点，可简化对Adobe解决方案的HTTP请求。 以前，访客.js向访客ID服务发送阻止调用，然后AT.js向Adobe Target发送呼叫，DIL.js向Adobe Audience Manager发送呼叫，最后，AppMeasurement.js向AdobeAnalytics发送呼叫。 此新库和端点可以检索ID、获取体 [!DNL Target] 验、向Adobe Experience Platform发 [!DNL Audience Manager]送数据，并通过一次调用将数据传递给。

以下视频演示了Adobe Experience Platform [!DNL Web SDK] 和 [!DNL Edge Network] 实际操作情况。 该视频示例使用对Adobe的单个调用，该调用将数 [!DNL Experience Platform]据发 [!DNL Analytics]送到 [!DNL Audience Manager]、和 [!DNL Target]。

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)


## 入门指南

我们强烈建议您 [查看我们的入门指南](getting-started/quick-start-with-launch.md) ，以快速学习如何开始使用Adobe Launch。

本产品不断发展和增长，以支持越来越多的用例。 为了跟上最新的步伐，请查看我们支持 [的使用案例展示板](https://github.com/adobe/alloy/projects/5)。 我们会根据我们目前支持的使用案例以及我们正在努力帮助您做出最佳决策的案例，不断更新这些案例。

* __尚未支持的用例__ -这些用例是我们今后将支持的路线图中的用例。
* __使用案例进行中__ -这些是团队当前正在完成以释放的使用案例。
* __支持的用例__ -这些用例是现在支持和可用的。
* __我们不支持的使用案例__ -这些是我们决定不支持的使用案例。

---
title: Adobe Experience Platform Web SDK帮助
seo-title: Adobe Experience Platform Web SDK帮助
description: 了解Adobe Experience Platform Web SDK是什么以及如何使用它。
seo-description: 允许Adobe Experience Cloud客户与Experience Cloud中的各种服务交互
translation-type: tm+mt
source-git-commit: 6ad09df6f6867ebe057d0043dea4bc97de2b66b3

---


# （测试版）什么是Adobe Experience Platform Web SDK

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生变化。

Adobe Experience Platform Web SDK是客户端JavaScript库，它允许Adobe Experience Cloud的客户通过Adobe Experience Platform Edge Network与Experience Cloud中的各种服务交互。

## SDK由Adobe Experience Platform Web SDK取代

Adobe Experience Platform Web SDK取代了以下SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

这不仅仅是现有库的包装器。 这完全是重写。 其目的是通过以正确的顺序触发标签、与库版本管理挑战不一致以及更好地进行依赖关系管理来结束挑战。 这是实施Experience Cloud的新方式。

除了新的库外，还有一个新的端点，可简化对Adobe解决方案的HTTP请求。 以前，访客.js向访客ID服务发送阻止调用，然后AT.js向Adobe目标发送调用，DIL.js向Adobe受众管理器发送调用，最后，AppMeasurement.js向Adobe Analytics发送调用。 此新库和端点可以检索ID、获取目标体验、将数据发送到受众管理器，并通过一次调用将数据传递到Adobe Experience Platform。
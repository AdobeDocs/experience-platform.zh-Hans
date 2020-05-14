---
title: Adobe Experience Platform Web SDK帮助
seo-title: Adobe Experience Platform Web SDK帮助
description: 了解Adobe Experience Platform Web SDK是什么以及如何使用它。
seo-description: 允许Adobe Experience Cloud客户与Experience Cloud中的各种服务进行交互。
translation-type: tm+mt
source-git-commit: f06c90d6248071894bd9929fbe1150e30c8e7385
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# 什么是Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK是客户端JavaScript库，允许Adobe Experience Cloud客户通过Adobe Experience Platform Edge Network与Experience Cloud中的各种服务交互。

## SDK已由Adobe Experience Platform Web SDK取代

Adobe Experience Platform Web SDK取代了以下SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

这不仅仅是现有库的包装。 这完全是重写。 其目的是通过以正确的顺序启用标记、与库版本控制挑战不一致以及更好的依赖性管理来结束挑战。 它是实施Experience Cloud的一种新方式，是开 [放源](https://github.com/adobe/alloy)

除了新的库，还有一个新的端点，可简化对Adobe解决方案的HTTP请求。 之前，访客.js向访客ID服务发送阻止调用，然后AT.js向Adobe目标发送调用，DIL.js向Adobe受众管理器发送调用，最后，AppMeasurement.js向Adobe Analytics发送调用。 此新库和端点可以检索ID、获取目标体验、将数据发送到受众管理器，并通过一次调用将数据传递到Adobe Experience Platform。

## 入门指南

我们强烈建议您结 [帐我们的入门指南](getting-started/quick-start-with-launch.md) ，以快速学习如何开始使用启动项。

本产品不断发展和增长，以支持越来越多的用例。 为了跟上最新的步伐，我们结帐了我们 [支持的使用案例展示板](https://github.com/adobe/alloy/projects/5)。 我们会根据我们目前支持的使用案例以及我们正在努力帮助您做出最佳决策的案例，不断更新这些案例。

* __Use Cases Not Desupported__ - are use cases that is are are in the readmap to de.
* __使用案例进行中__ -这些是团队当前正在完成以释放的使用案例。
* __支持的用例__ -这些用例是现在支持和可用的。
* __我们不支持的使用案例__ -这些是我们决定不支持的使用案例。

---
title: Adobe Experience PlatformWeb SDK帮助
seo-title: Adobe Experience PlatformWeb SDK帮助
description: 了解Adobe Experience PlatformWeb SDK是什么以及如何使用它。
seo-description: 了解如何允许Adobe Experience Cloud的客户与该Experience Cloud的各种服务进行交互。
keywords: Adobe Experience PlatformWeb SDK；平台Web SDK;Web SDK;edge;访客.js;AppMeasurement.js;AT.js;DIL.js;web sdk;SDK;Web SDK；启动；
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 1%

---


# 什么是Adobe Experience PlatformWeb SDK

Adobe Experience PlatformWeb SDK是客户端JavaScript库，它允许Adobe Experience Cloud客户通过Adobe Experience Platform边缘网络与[!DNL Experience Cloud]中的各种服务进行交互。 除JavaScript库外，还有[Experience Platform Launch扩展](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)，可帮助您配置Web SDK。

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] 是组成Experience Edge的集合的一部分。Experience Edge包含三种技术：

* **[!DNL Adobe Experience Platform Web SDK]：可** 大幅简化部 [!DNL Experience Platform Launch] 署技术的JavaScript SDK和扩 [!DNL Adobe] 展
* **Adobe Experience Platform移动** SDK:v5移动SDK的扩展，允许客户使用新的部署方法
* **[!DNL Adobe Experience Platform Edge Network]：一** 个全球分布式服务器网络，支持一种部署产品的新方 [!DNL Adobe] 法

[!DNL Adobe Experience Edge]是用于在所有可寻址渠道中进行低延迟数据收集、可插拔计算和快速数据激活的新框架。

[!DNL Adobe Experience Edge] 为每个渠道（JavaScript、移动、服务器端）提供一个统一的SDK，它将数据发送到通用Adobe域(`adobedc.net`)，并为数据和体验投放接收单个负载返回。

在服务器端，统一的边缘网关和通用平台服务框架使得在这个实时计算环境中插入和部署新功能变得很容易。  此架构：

* 缩短客户价值转化时间
* 结束对“点”集成的需求
* 与旧库相比，性能得到提高
* 降低成本
* 提高创新速度
* 为Adobe客户创造持续的竞争优势

通过单一整合的边缘系统，客户可以作为集成体验管理所有渠道的广告、营销或个性化活动。  它允许[!DNL Adobe]以更低的客户总体拥有成本提供服务。  它还通过使实时边缘可插拔，允许[!DNL Adobe]及其客户更快地向该实时系统添加新功能和客户定义的逻辑，从而帮助提高产品创新的速度。

## 视频概述

以下视频概述了Adobe Experience Platform[!DNL Web SDK]和Adobe Experience Platform[!DNL Edge Network]。

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK被Adobe Experience PlatformWeb SDK所取代

Adobe Experience PlatformWeb SDK取代了以下SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

这不仅仅是现有库的包装。 这完全是重写。 其目的是通过以下方式结束挑战：以正确的顺序触发标记、与库版本控制挑战不一致以及更好地进行依赖管理。 它是实现[!DNL Experience Cloud]的一种新方法，它是[开放源](https://github.com/adobe/alloy)。

除了新的库外，还有一个新的端点，可简化对Adobe解决方案的HTTP请求。 以前，访客ID服务会收到阻止呼叫，然后AT.js向Adobe Target发出呼叫，DILID向Adobe Audience Manager发出呼叫，最后，AppMeasurement.js向Adobe Analytics发出呼叫。 此新库和端点可以检索ID、获取[!DNL Target]体验、将数据发送到[!DNL Audience Manager]，并通过一次调用将数据传递到Adobe Experience Platform。

以下视频演示了Adobe Experience Platform[!DNL Web SDK]和Adobe Experience Platform[!DNL Edge Network]的实际操作。 该视频示例使用对Adobe的单个调用，该调用将数据发送到[!DNL Experience Platform]、[!DNL Analytics]、[!DNL Audience Manager]和[!DNL Target]。

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

本产品不断发展和增长，以支持越来越多的用例。 为了跟上最新的步伐，请查看我们的[受支持的用例板](https://github.com/adobe/alloy/projects/5)。 我们会根据我们目前支持的使用案例以及我们正在努力帮助您做出最佳决策的案例，不断更新这些案例。

* **尚未支持的用** 例：我们今后将支持这些用例。
* **正在进行的用例：** 这些是团队当前正在完成的待发布的用例。
* **支持的用例：** 这些用例是现在支持和可用的。
* **我们不支持的使用案例：** 这些是我们决定不支持的使用案例。

---
title: Adobe Experience Platform Web SDK概述
description: 了解如何使用Adobe Experience Platform Web SDK将平台功能集成到您的网站中。
keywords: Adobe Experience Platform Web SDK；平台Web SDK;Web SDK；边缘；访客.js;AppMeasurement.js;AT.js;DIL.js;web sdk;SDK;Web SDK；启动；启动
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 2%

---


# Adobe Experience Platform Web SDK概述

Adobe Experience Platform Web SDK是客户端JavaScript库，它允许Adobe Experience Cloud客户通过Adobe Experience Platform Edge Network与[!DNL Experience Cloud]中的各种服务交互。 除JavaScript库外，还有一个[Experience Platform Launch扩展](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)，用于帮助您配置Web SDK。

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] 是组成Experience Edge的集合的一部分。Experience Edge包含三种技术：

* **[!DNL Adobe Experience Platform Web SDK]:** JavaScript SDK和扩展可 [!DNL Experience Platform Launch] 以显着简化部署技 [!DNL Adobe] 术
* **Adobe Experience Platform Mobile SDK:** v5 Mobile SDK的扩展，允许客户使用新的部署方法
* **[!DNL Adobe Experience Platform Edge Network]：一** 个全球分布式服务器网络，支持部署产品的新方 [!DNL Adobe] 法

[!DNL Adobe Experience Edge]是用于在所有可寻址渠道中进行低延迟数据收集、可插拔计算和快速数据激活的新框架。

[!DNL Adobe Experience Edge] 为每个渠道(JavaScript、Mobile、Server-side)提供一个统一的SDK，该将数据发送到公用Adobe域()，并为和体验投放接收单个负载`adobedc.net`返回。

在服务器端，统一的边缘网关和通用平台服务框架使得在此实时计算环境中插入和部署新功能变得很容易。  此架构：

* 缩短客户实现价值的时间
* 结束了对“点”集成的需求
* 与旧库相比，性能有所提高
* 降低成本
* 提高创新速度
* 为Adobe客户创造持续的竞争优势

通过单一整合的边缘系统，客户可以将其所有渠道的广告、营销或个性化活动作为集成体验进行管理。  它允许[!DNL Adobe]以更低的总拥有成本为客户提供服务。  它还通过使实时边缘可插拔和允许[!DNL Adobe]及其客户更快速地向该实时系统添加新功能和客户定义的逻辑，帮助提高产品创新的速度。

## 视频概述

以下视频概述了Adobe Experience Platform [!DNL Web SDK]和Adobe Experience Platform [!DNL Edge Network]。

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK由Adobe Experience Platform Web SDK替换

Adobe Experience Platform Web SDK取代了以下SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

这不仅仅是现有库的包装。 这是彻底的重写。 其目的是通过以正确的顺序触发标签、库版本管理挑战不一致以及更好的依赖关系管理来结束挑战。 它是实现[!DNL Experience Cloud]的一种新方法，它是[开放源](https://github.com/adobe/alloy)。

除了新的库外，还有一个新的端点，可简化对Adobe解决方案的HTTP请求。 之前，访客.js向访客 ID服务发送了阻止调用，然后AT.js向Adobe Target发送了调用，DIL.js向Adobe Audience Manager发送了调用，最后，AppMeasurement.js向Adobe Analytics发送了调用。 此新库和端点可以检索ID、获取[!DNL Target]体验、将数据发送到[!DNL Audience Manager]，并通过一次调用将数据传递到Adobe Experience Platform。

以下视频演示了Adobe Experience Platform [!DNL Web SDK]和Adobe Experience Platform [!DNL Edge Network]的实际操作情况。 该视频示例使用对Adobe的单个调用，该调用将数据发送到[!DNL Experience Platform]、[!DNL Analytics]、[!DNL Audience Manager]和[!DNL Target]。

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

此产品在不断发展和增长，以支持越来越多的使用案例。 为了跟上最新的步伐，请查看我们的[受支持的用例板](https://github.com/adobe/alloy/projects/5)。 我们会根据我们目前支持的使用案例以及我们正在努力帮助您做出最佳决策的案例，不断更新此版本。

* **尚未支持的使用案** 例：这些是将来支持我们路线图中的使用案例。
* **使用案例：** 团队当前正在完成发行的使用案例。
* **支持的用例：** 这些用例是目前支持和可用的用例。
* **我们不支持的使用案例：** 这些是我们决定不支持的使用案例。

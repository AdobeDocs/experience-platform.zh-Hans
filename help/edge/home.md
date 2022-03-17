---
title: Adobe Experience Platform Web SDK概述
description: 了解如何使用Adobe Experience Platform Web SDK将平台功能集成到您的网站中。
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;Edge;Visitor.js;AppMeasurement.js;AT.js;Web.js;Web SDK;Web SDK;Launch；启动
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 71857ffc5e671f4d9a0502fb95d89d30fdec1f15
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 1%

---

# Adobe Experience Platform Web SDK概述

Adobe Experience Platform Web SDK是一个客户端JavaScript库，它允许Adobe Experience Cloud客户与 [!DNL Experience Cloud] 通过Adobe Experience Platform边缘网络。 除了JavaScript库之外，还有 [标记扩展](./extension/web-sdk-extension-configuration.md) 以帮助您配置Web SDK。

**有关设置Web SDK以及将数据发送到解决方案的分步指南，请参阅我们的 [使用Web SDK实施Adobe Experience Cloud教程](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en)**

## Experience Edge

[!DNL Adobe Experience Platform Web SDK] 是构成Experience Edge的集合的一部分。 Experience Edge包含三种技术：

* **[!DNL Adobe Experience Platform Web SDK]:** 可显着简化部署的JavaScript SDK和标记扩展 [!DNL Adobe] 技术
* **Adobe Experience Platform Mobile SDK:** v5 Mobile SDK的扩展，允许客户使用新的部署方法
* **[!DNL Adobe Experience Platform Edge Network]:** 全球分布式服务器网络，支持新的部署方法 [!DNL Adobe] 产品

的 [!DNL Adobe Experience Edge] 是用于在所有可寻址渠道中进行低延迟数据收集、可插拔计算和快速数据激活的新框架。

[!DNL Adobe Experience Edge] 为每个渠道（JavaScript、Mobile、服务器端）提供单个整合的SDK，该渠道会将数据发送到通用的Adobe域(`adobedc.net`)并接收返回的单个有效负载以交付数据和体验。

在服务器端，统一的边缘网关和通用的平台服务框架使插件和部署新功能成为这一实时计算环境的方便之选。  此架构：

* 缩短客户实现价值的时间
* 结束了对“点”集成的需求
* 与旧库相比，提高了性能
* 降低成本
* 提高创新速度
* 为Adobe客户创造持续的竞争优势

通过单个整合的边缘系统，客户可以作为集成体验来管理所有渠道中的广告、营销或个性化活动。  它允许 [!DNL Adobe] 为客户提供总拥有成本更低的服务。  它还通过使实时边缘可插拔和允许 [!DNL Adobe] 以及其客户，以更快地向该实时系统添加新功能和客户定义逻辑。

## 视频概述

以下视频概述了Adobe Experience Platform [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK已由Adobe Experience Platform Web SDK替代

Adobe Experience Platform Web SDK取代了以下SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

这不仅仅是现有库的包装器。 这是彻头彻尾的重写。 其目的在于终止标签必须按正确顺序触发的挑战、与库版本控制挑战不一致以及更好的依赖关系管理。 这是实施 [!DNL Experience Cloud] 而是 [开源](https://github.com/adobe/alloy).

除了新库之外，还有一个新端点，可简化对Adobe解决方案的HTTP请求。 之前，Visitor.js向访客ID服务发送了一个阻止调用，然后AT.js向Adobe Target发送一个调用，DIL.js向Adobe Audience Manager发送一个调用，最后，AppMeasurement.js向Adobe Analytics发送了一个调用。 此新库和端点可以检索ID，获取 [!DNL Target] 体验，将数据发送到 [!DNL Audience Manager]，并在一次调用中将数据传递到Adobe Experience Platform。

以下视频演示了Adobe Experience Platform [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network] 中。 视频示例使用对Adobe的单个调用，该调用将数据发送到 [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]和 [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

此产品不断发展壮大，以支持越来越多的用例。 要跟上最新版本并了解我们当前支持的功能，请参阅 [“支持用例”页](https://github.com/orgs/adobe/projects/18/views/1).

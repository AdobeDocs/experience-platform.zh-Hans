---
title: JavaScript概述
description: 使用JavaScript将数据发送到Adobe Experience Platform Edge Network。
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 09799847c61d82ed5b7cd372d92aa436697d54f3
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# JavaScript概述

**Adobe Experience Platform Web SDK**&#x200B;是客户端JavaScript库，它允许您将数据发送到Adobe Experience Platform Edge Network。

Web SDK以与解决方案无关的方式(XDM)将数据发送到Experience Platform Edge Network，会将数据映射到解决方案特定的格式和目标，并实时发送。

您可以通过两种方式实施Web SDK：

* 使用[JavaScript库](install/library.md)手动实施（此文档）
* [Web SDK标记扩展](/help/tags/extensions/client/web-sdk/overview.md)

本指南包含有关使用Web Experience Cloud JavaScript库与SDK解决方案交互的说明。

## Experience Platform Edge Network {#edge-network}

Adobe Experience Platform Edge Network提供了低延迟数据收集、可插拔计算和快速数据激活功能，涵盖所有可寻址渠道。 它为Web、移动和服务器端渠道提供单个整合的SDK，将数据发送到公共Adobe域(`adobedc.net`)，并接收数据和体验交付的单个有效负载。

在服务器端，统一的边缘网关和通用平台服务框架简化了新功能的部署，同时提供了以下优势：

* 减少客户实现价值的时间；
* 结束对“点”集成的需求；
* 与旧库相比提高了性能；
* 降低运营成本；
* 加快创新速度；
* 为Adobe客户创造持续的竞争优势。

通过整合的边缘系统，您可以跨所有渠道管理广告、营销和个性化营销活动。 它降低了总拥有成本并支持各种数据类型，使您能够映射数据模型以用于多个Experience Cloud产品。

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## 由Web SDK替换的库 {#sdks}

Web SDK是从头开始构建的开放源库，用于集成现有库的功能。 它解决了标记触发顺序、版本不一致和依赖关系管理等问题，提供了一种实施许多Experience Cloud产品的方法。 Web SDK取代了为以下服务收集数据：

* Adobe Experience Platform访客ID服务(`Visitor.js`)
* Adobe Analytics (`AppMeasurement.js`)
* Adobe Target (`AT.js`)
* Adobe Audience Manager (`DIL.js`)
* Adobe Media Analytics
* Adobe Advertising

它还引入了一个新端点，该端点可简化对Adobe解决方案的HTTP请求。 以前，每个数据收集库需要多次调用。 现在，单次调用便可以检索ID、提取[!DNL Target]体验、将数据发送到[!DNL Audience Manager]以及将数据传递到Adobe Experience Platform。

## 从现有库迁移到Web SDK {#migrating-to-web-sdk}

Adobe提供了简化的升级路径，以简化从任何现有库到Web SDK的迁移。 您可以单独迁移网站的每个页面，而无需一次迁移整个网站。 您可以在部分页面上使用Web SDK，而在其他页面上使用现有库，从而实现逐步过渡。

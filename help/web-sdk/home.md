---
title: Adobe Experience Platform Web Software Development Kit (SDK)概述
description: 了解如何使用Adobe Experience Platform Web SDK将Experience Platform功能集成到您的网站。
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 1%

---

# Adobe Experience Platform Web SDK {#overview}

Adobe Experience Platform Web SDK是一个客户端JavaScript库，它允许Adobe Experience Cloud客户通过Adobe Experience Platform Edge Network与其服务进行交互。

您可以通过两种方式实施Web SDK：

* [Web SDK标记扩展](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)。 有关详细信息，请参阅关于如何[使用Web SDK实施Adobe Experience Cloud](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hans)的教程。
* 使用[Web SDK JavaScript库](install/library.md)手动实施。

本指南包含有关同时使用Web Experience Cloud JavaScript库和标记扩展与SDK解决方案交互的说明。

## Experience Platform Edge Network {#edge-network}



Experience Platform Web SDK是Adobe Experience Platform Edge Network的一部分，它包括：

* **[Experience Platform Web SDK](#overview)**：用于简化Adobe技术部署的JavaScript库和标记扩展。
* **[Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/)**：新部署方法的v5移动SDK扩展。
* **[Edge Network API](../server-api/overview.md)**：用于数据收集、个性化、广告和营销用例的服务器端API。 您可以在服务器、IoT设备、机顶盒和其他设备上使用它。

Edge Network提供了低延迟的数据收集、可插拔计算和快速数据激活（涵盖所有可寻址渠道）。 它为Web、移动和服务器端渠道提供单个整合的SDK，将数据发送到公共Adobe域(`adobedc.net`)，并接收数据和体验交付的单个有效负载。

在服务器端，统一的边缘网关和通用平台服务框架简化了新功能的部署，同时提供了以下优势：

* 减少客户实现价值的时间；
* 结束对“点”集成的需求；
* 与旧库相比提高了性能；
* 降低运营成本；
* 加快创新速度；
* 为Adobe客户创造持续的竞争优势。

通过整合的边缘系统，您可以跨所有渠道管理广告、营销和个性化营销活动。 它降低了总拥有成本并支持各种数据类型，使您能够映射数据模型以用于多个Experience Cloud产品。

## 视频概述 {#video}

观看以下视频，了解Adobe Experience Platform [!DNL Web SDK]和[!DNL Edge Network]的概述。

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## 由Web SDK替换的库 {#sdks}

Web SDK是新的开源库，从头开始构建，用于集成现有库的功能。 它解决了标记触发顺序、版本不一致和依赖关系管理的问题，提供了一种新的[开源](https://github.com/adobe/alloy)方法来实施[!DNL Experience Cloud]。

Web SDK取代了：

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

它还引入了一个新端点，该端点可简化对Adobe解决方案的HTTP请求。 以前，`Visitor.js`、`AT.js`、`DIL.js`和`AppMeasurement.js`需要多次调用。 现在，单次调用便可以检索ID、提取[!DNL Target]体验、将数据发送到[!DNL Audience Manager]以及将数据传递到Adobe Experience Platform。

观看以下视频以了解Adobe Experience Platform [!DNL Web SDK]和[!DNL Edge Network]的实际操作情况，只需一次调用即可将数据发送到[!DNL Experience Platform]、[!DNL Analytics]、[!DNL Audience Manager]和[!DNL Target]。

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## 从现有库迁移到Web SDK {#migrating-to-web-sdk}

Adobe提供了简化的升级路径，以简化从任何[现有库](#sdks)到Web SDK的迁移。 您可以单独迁移网站的每个页面，而无需一次迁移整个网站。 您可以在部分页面上使用Web SDK，而在其他页面上使用现有库，从而实现逐步过渡。

### 将`AT.js`迁移到Web SDK注意事项 {#considerations}

在使用`AT.js`将页面迁移到Web SDK之前，请启用以下Web SDK配置选项，以确保在页面之间导航时保持访客资料。

* [&#39;idMigrationEnabled&#39;](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [&#39;targetMigrationEnabled&#39;](/help/web-sdk/commands/configure/targetmigrationenabled.md)

>[!IMPORTANT]
>
>从`at.js`迁移到Web SDK时不支持以下Target功能：
>
>* [重定向选件](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html)
>* [CNAME和跨域支持](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

从`AT.js`迁移到Web SDK后，从配置中删除`targetMigrationEnabled`选项。

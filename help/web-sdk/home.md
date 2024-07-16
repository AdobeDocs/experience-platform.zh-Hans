---
title: Adobe Experience Platform Web软件开发工具包(SDK)概述
description: 了解如何使用Adobe Experience Platform Web SDK将Platform功能集成到您的网站。
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 1%

---


# Adobe Experience Platform Web SDK {#overview}

>[!IMPORTANT]
>
>2024年4月底，Adobe Experience Platform Web SDK将停止对所有版本的Internet Explorer提供支持。

Adobe Experience Platform Web软件开发工具包(SDK)是一个客户端JavaScript库，它允许Adobe Experience Cloud的客户通过Adobe Experience PlatformEdge Network与其服务进行交互。

Adobe提供了两种实施Web SDK的方法：

* [Web SDK标记扩展](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)。 有关详细信息，请参阅关于如何[使用Web SDK实施Adobe Experience Cloud](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hans)的教程。
* 使用Web SDK JavaScript库进行手动实施。

本用户指南包含有关通过Web SDK JavaScript库和Experience Cloud扩展（如果适用）与标记解决方案交互的说明。

## Experience PlatformEdge Network {#edge-network}

Experience PlatformWeb SDK是构成Adobe Experience PlatformEdge Network的工具集的一部分。

Edge Network包含以下组件：

* **[Experience PlatformWeb SDK](#overview)：**&#x200B;可帮助您简化Adobe技术部署的JavaScript库和标记扩展。
* **[Experience PlatformMobile SDK](https://developer.adobe.com/client-sdks/home/)：** v5 Mobile SDK的扩展，允许您使用新的部署方法。
* **[Edge Network服务器API](../server-api/overview.md)：**&#x200B;可用于各种数据收集、个性化、广告和营销用例的服务器端API。 服务器API可用于服务器、IoT设备、机顶盒和其他各种设备。

该Edge Network是一个跨所有可寻址信道进行低延迟数据收集、可插拔计算和快速数据激活的框架。 它为每个渠道（Web、移动设备、服务器端）提供单个整合的SDK，后者将数据发送到公共Adobe域(`adobedc.net`)，并接收返回的单个有效负载以交付数据和体验。

在服务器端，统一的边缘网关和通用平台服务框架有助于将新功能轻松部署到此实时计算环境中。 此架构：

* 减少客户实现价值的时间
* 结束对“点”集成的需求
* 与旧库相比提高了性能
* 降低成本
* 提高创新速度
* 为Adobe客户创造持续的竞争优势

通过单个整合的边缘系统，您可以将所有渠道中的广告、营销或个性化营销活动作为集成体验进行管理。 它还允许Adobe以更低的总体拥有成本为客户提供服务。 Edge System旨在容纳大多数类型的数据，允许您映射自己的数据模型以供多个Experience Cloud产品摄取。

## 视频概述 {#video}

观看以下视频，了解Adobe Experience Platform [!DNL Web SDK]和[!DNL Edge Network]的概述。

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## 由Web SDK替换的库 {#sdks}

Web SDK不仅仅是现有库的包装器。 它是一个新的图书馆，从头开始编写，以合并现有图书馆的功能。 其目的在于结束标记必须按正确顺序触发的挑战、与库版本化挑战不一致以及更好地管理依赖关系。 这是一种实现[!DNL Experience Cloud]的新方法，它是[开源](https://github.com/adobe/alloy)。

Web SDK替换以下SDK：

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

除了新库之外，还有一个新端点，它简化了Adobe解决方案的HTTP请求。 之前，`Visitor.js`向访客ID服务发送阻止调用，然后`AT.js`向Adobe Target发送调用，`DIL.js`向Adobe Audience Manager发送调用，最后`AppMeasurement.js`向Adobe Analytics发送调用。 此新库和端点可以在一次调用中检索ID、获取[!DNL Target]体验、将数据发送到[!DNL Audience Manager]以及将数据传递到Adobe Experience Platform。

以下视频演示了Adobe Experience Platform [!DNL Web SDK]和Adobe Experience Platform [!DNL Edge Network]的实际操作情况。 视频示例使用单个调用来Adobe，该调用将数据发送到[!DNL Experience Platform]、[!DNL Analytics]、[!DNL Audience Manager]和[!DNL Target]。

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## 从现有库迁移到Web SDK {#migrating-to-web-sdk}

为了简化从任何[现有库](#sdks)到Web SDK的迁移，Adobe提供了简化的升级途径。 通过此路径，您可以将网站的每个页面迁移到Web SDK，而无需一次迁移整个网站。 您可以在给定页面上使用Web SDK，而现有库驻留在其他页面上。 准备就绪后，您还可以迁移这些其他页面。

### 将`AT.js`迁移到Web SDK注意事项 {#considerations}

在将使用`AT.js`的页面迁移到Web SDK之前，请确保启用以下Web SDK配置选项。 这些选项可确保使用Web SDK从具有`AT.js`的页面导航到页面时，保持访客配置文件。

* [&#39;idMigrationEnabled&#39;](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [&#39;targetMigrationEnabled&#39;](/help/web-sdk/commands/configure/targetmigrationenabled.md)


>[!IMPORTANT]
>
>从at.js迁移到Web SDK时不支持以下Target功能：
>
>* [重定向选件](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html)
>* [CNAME和跨域支持](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

从`AT.js`迁移到Web SDK后，从配置中删除`targetMigrationEnabled`选项。

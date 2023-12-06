---
title: Adobe Experience Platform Web软件开发工具包(SDK)概述
description: 了解如何使用Adobe Experience Platform Web SDK将Platform功能集成到您的网站。
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 1%

---


# Adobe Experience Platform Web SDK {#overview}

Adobe Experience Platform Web软件开发工具包(SDK)是一个客户端JavaScript库，它允许Adobe Experience Cloud的客户通过Adobe Experience Platform Edge Network与其服务进行交互。 Adobe提供了两种实施Web SDK的方法：

* 使用进行手动实施 `alloy.js` JavaScript库 本用户指南提供了关于此实施方法的文档。
* 此 [Web SDK标记扩展](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). 请参阅 [使用Web SDK实施Adobe Experience Cloud教程](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hans) 以了解更多信息。

## Experience Platform边缘网络 {#edge-network}

Experience PlatformWeb SDK是组成Adobe Experience Platform Edge Network的一系列工具的一部分。 Edge Network包含以下组件：

* **[Experience PlatformWeb SDK](#overview)：** JavaScript SDK和标记扩展可显着简化Adobe技术的部署。
* **[Experience Platform移动SDK](https://developer.adobe.com/client-sdks/home/)：** v5 Mobile SDK的扩展，允许客户使用新的部署方法
* **[Experience Platform边缘网络服务器API](../server-api/overview.md)：** 可用于各种数据收集、个性化、广告和营销用例的API。 服务器API可用于服务器、IoT设备、机顶盒和其他各种设备。

Edge Network是一个框架，用于在所有可寻址通道中进行低延迟数据收集、可插拔计算和快速数据激活。 它为每个渠道（JavaScript、移动设备、服务器端）提供单个整合SDK，将数据发送到公共Adobe域(`adobedc.net`)，接收返回的单个有效负载以进行数据和体验交付。

在服务器端，统一的边缘网关和通用平台服务框架有助于将新功能轻松部署到此实时计算环境中。 此架构：

* 减少客户实现价值的时间
* 结束对“点”集成的需求
* 与旧库相比提高了性能
* 降低成本
* 提高创新速度
* 为Adobe客户创造持续的竞争优势

通过单个整合的边缘系统，客户可将其跨所有渠道的广告、营销或个性化营销活动作为集成体验进行管理。 它还允许Adobe以更低的总体拥有成本为客户提供服务。 Edge System旨在容纳大多数类型的数据，允许您映射自己的数据模型以供多个Experience Cloud产品摄取。

## 视频概述 {#video}

以下视频概述了Adobe Experience Platform [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## 由Web SDK替换的库 {#sdks}

Web SDK不仅仅是现有库的包装器。 它是一个新的图书馆，从头开始编写，以合并现有图书馆的功能。 其目的在于结束标记必须按正确顺序触发的挑战、与库版本化挑战不一致以及更好地管理依赖关系。 这是一种实施 [!DNL Experience Cloud] 确实如此 [开放源代码](https://github.com/adobe/alloy).

Web SDK替换以下SDK：

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

除了新库之外，还有一个新端点，它简化了Adobe解决方案的HTTP请求。 之前， `Visitor.js` 向访客ID服务发送阻止调用，然后 `AT.js` 向Adobe Target发送了调用， `DIL.js` 向Adobe Audience Manager发送了调用，最后 `AppMeasurement.js` 已向Adobe Analytics发送调用。 此新库和端点可以检索ID，获取 [!DNL Target] 体验，将数据发送到 [!DNL Audience Manager]，并在单个调用中将数据传递到Adobe Experience Platform。

以下视频演示了Adobe Experience Platform [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network] 实际操作中。 视频示例使用单个调用以将数据传输到的Adobe [!DNL Experience Platform]， [!DNL Analytics]， [!DNL Audience Manager]、和 [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## 从现有库迁移到Web SDK {#migrating-to-web-sdk}

简化从任一 [现有库](#sdks) 对于Web SDK，Adobe提供了简化的升级途径。 通过此路径，您可以将网站的每个页面迁移到Web SDK，而无需一次迁移整个网站。 您可以在给定页面上使用Web SDK，而现有库驻留在其他页面上。 准备就绪后，您还可以迁移这些其他页面。

### 迁移 `AT.js` 更改为Web SDK注意事项 {#considerations}

在迁移使用的页面之前 `AT.js` 对于Web SDK，请确保启用以下Web SDK配置选项。 这些选项确保在使用的页面中导航时保留访客配置文件 `AT.js` 到使用Web SDK的页面。

* [&#39;idMigrationEnabled&#39;](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [&#39;targetMigrationEnabled&#39;](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>从at.js迁移到Web SDK时不支持以下Target功能：
>
>* [重定向选件](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html)
>* [CNAME和跨域支持](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

从迁移后 `AT.js` 到Web SDK，删除 `targetMigrationEnabled` 选项。

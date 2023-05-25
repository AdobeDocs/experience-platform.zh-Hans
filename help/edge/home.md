---
title: Adobe Experience Platform Web SDK概述
description: 了解如何使用Adobe Experience Platform Web SDK将Platform功能集成到您的网站。
keywords: Adobe Experience Platform Web SDK；Platform Web SDK；Web SDK；Edge；Visitor.js；AppMeasurement.js；AT.js；DIL.js；Web SDK；SDK；Web SDK；Launch；Launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 00801465435133fce29002c8bd0f2256745ba2c2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 1%

---

# Adobe Experience Platform Web SDK概述 {#overview}

Adobe Experience Platform Web SDK是一个客户端JavaScript库，它允许Adobe Experience Cloud的客户与 [!DNL Experience Cloud] 通过Adobe Experience Platform Edge Network。 除了JavaScript库之外， [标记扩展](./extension/web-sdk-extension-configuration.md) 以帮助配置Web SDK。

有关使用标记设置Web SDK并将数据发送到解决方案的分步指南，请参阅我们的 [使用Web SDK实施Adobe Experience Cloud教程](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en).

>[!IMPORTANT]
>
>此产品在不断演变和增长，以支持越来越多的用例。 要了解最新信息并查看我们当前支持的内容，请参阅 [受支持的用例页面](https://github.com/orgs/adobe/projects/18/views/1).

## Adobe Experience Edge

[!DNL Adobe Experience Platform Web SDK] 是构成 [!DNL Adobe Experience Edge]. [!DNL Experience Edge] 由以下技术组成：

* **[[!DNL Adobe Experience Platform Web SDK]](#overview)：** JavaScript SDK和标记扩展可显着简化部署 [!DNL Adobe] 技术。
* **[[!DNL Adobe Experience Platform Mobile SDK]](https://aep-sdks.gitbook.io/docs/getting-started/overview)：** v5 mobile SDK的扩展，允许客户使用新的部署方法
* **[[!DNL Adobe Experience Platform Edge Network]](../server-api/overview.md)：** 全球分布式服务器网络，支持新的部署方法 [!DNL Adobe] 产品

此 [!DNL Adobe Experience Edge] 是用于所有可寻址通道上的低延迟数据收集、可插拔计算和快速数据激活的新框架。

[!DNL Adobe Experience Edge] 为每个渠道（JavaScript、移动设备、服务器端）提供单个整合SDK，将数据发送到公共Adobe域(`adobedc.net`)并接收单个有效负荷返回，以进行数据和体验交付。

在服务器端，统一的边缘网关和通用平台服务框架使插入新功能并部署到该实时计算环境中变得很容易。  此架构：

* 缩短客户实现价值的时间
* 结束对“点”集成的需求
* 与旧库相比提高了性能
* 降低成本
* 提高创新速度
* 为Adobe客户创造持续的竞争优势

通过单个整合的边缘系统，客户可以将跨所有渠道的广告、营销或个性化营销活动作为集成体验进行管理。 它允许 [!DNL Adobe] 以更低的总体拥有成本为客户提供服务。  此外，它还可以通过使实时边缘可插拔并允许 [!DNL Adobe] 及其客户以更快地向实时系统添加新功能和客户定义的逻辑。

## 视频概述 {#video}

以下视频概述了Adobe Experience Platform [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## 由Web SDK替换的库 {#sdks}

Web SDK不仅仅是一个围绕现有库的包装器。 它是一个全新的图书馆，从头开始编写，以纳入现有图书馆的功能。 其目的在于结束标记必须按正确顺序触发的挑战、与库版本控制挑战的不一致以及更好的依赖关系管理。 这是一种实施 [!DNL Experience Cloud] 它是 [开放源代码](https://github.com/adobe/alloy).

Web SDK替换以下SDK：

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

除了新库之外，还有一个新端点，它简化了Adobe解决方案的HTTP请求。 之前，Visitor.js向访客ID服务发送阻止调用，然后AT.js向Adobe Target发送调用，DIL.js向Adobe Audience Manager发送调用，最后AppMeasurement.js向Adobe Analytics发送调用。 此新库和端点可以检索ID，获取 [!DNL Target] 体验，将数据发送到 [!DNL Audience Manager]，并在单个调用中将数据传递到Adobe Experience Platform。

以下视频演示了Adobe Experience Platform [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network] 实际操作中。 视频示例使用单个调用以将数据传输到的Adobe [!DNL Experience Platform]， [!DNL Analytics]， [!DNL Audience Manager]、和 [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## 从现有库迁移到Web SDK {#migrating-to-web-sdk}

简化从任意 [现有库](#sdks) 对于Web SDK，Adobe提供了简化的升级途径，允许您将网站的每个单独页面迁移到Web SDK，而无需一次迁移整个网站。

这意味着您可以在页面上使用Web SDK，并将现有库保留在其他页面上，直到您也可以迁移这些库为止。

### 从at.js迁移到Web SDK的注意事项 {#considerations}

在迁移使用的页面之前 [!DNL at.js] 对于Web SDK，请确保启用以下Web SDK配置选项。 这可以确保在从页面导航时保留访客资料 [!DNL at.js ] 到使用Web SDK的页面。

* [&#39;idMigrationEnabled&#39;](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [&#39;targetMigrationEnabled&#39;](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>从at.js迁移到Web SDK时，不支持以下Target功能：
> * [重定向选件](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en)
> * [CNAME和跨域支持](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/?lang=en)


从at.js迁移到Web SDK后，您应删除 `targetMigrationEnabled` 选项。




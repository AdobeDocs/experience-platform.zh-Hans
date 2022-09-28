---
title: Adobe Experience Platform Web SDK概述
description: 了解如何使用Adobe Experience Platform Web SDK将平台功能集成到您的网站中。
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;Edge;Visitor.js;AppMeasurement.js;AT.js;Web.js;Web SDK;Web SDK;Launch；启动
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 00801465435133fce29002c8bd0f2256745ba2c2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 1%

---

# Adobe Experience Platform Web SDK概述 {#overview}

Adobe Experience Platform Web SDK是一个客户端JavaScript库，它允许Adobe Experience Cloud客户与 [!DNL Experience Cloud] 通过Adobe Experience Platform边缘网络。 除了JavaScript库之外，还有 [标记扩展](./extension/web-sdk-extension-configuration.md) 以帮助您配置Web SDK。

有关设置Web SDK以及将数据发送到解决方案的分步指南，请参阅我们的 [使用Web SDK实施Adobe Experience Cloud教程](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en).

>[!IMPORTANT]
>
>此产品不断发展壮大，以支持越来越多的用例。 要跟上最新版本并了解我们当前支持的功能，请参阅 [“支持用例”页](https://github.com/orgs/adobe/projects/18/views/1).

## Adobe Experience Edge

[!DNL Adobe Experience Platform Web SDK] 是构成 [!DNL Adobe Experience Edge]. [!DNL Experience Edge] 包括以下技术：

* **[[!DNL Adobe Experience Platform Web SDK]](#overview):** 可显着简化部署的JavaScript SDK和标记扩展 [!DNL Adobe] 技术。
* **[[!DNL Adobe Experience Platform Mobile SDK]](https://aep-sdks.gitbook.io/docs/getting-started/overview):** v5 Mobile SDK的扩展，允许客户使用新的部署方法
* **[[!DNL Adobe Experience Platform Edge Network]](../server-api/overview.md):** 全球分布式服务器网络，支持新的部署方法 [!DNL Adobe] 产品

的 [!DNL Adobe Experience Edge] 是用于在所有可寻址渠道中进行低延迟数据收集、可插拔计算和快速数据激活的新框架。

[!DNL Adobe Experience Edge] 为每个渠道（JavaScript、Mobile、服务器端）提供单个整合的SDK，该渠道会将数据发送到通用的Adobe域(`adobedc.net`)并接收返回的单个有效负载以交付数据和体验。

在服务器端，统一的边缘网关和通用的平台服务框架使插件和部署新功能成为这一实时计算环境的方便之选。  此架构：

* 缩短客户实现价值的时间
* 结束了对“点”集成的需求
* 与旧库相比，提高了性能
* 降低成本
* 提高创新速度
* 为Adobe客户创造持续的竞争优势

通过单个整合的边缘系统，客户可以作为集成体验来管理所有渠道中的广告、营销或个性化活动。 它允许 [!DNL Adobe] 为客户提供总拥有成本更低的服务。  它还通过使实时边缘可插拔和允许 [!DNL Adobe] 以及其客户，以更快地向该实时系统添加新功能和客户定义逻辑。

## 视频概述 {#video}

以下视频概述了Adobe Experience Platform [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## 由Web SDK替换的库 {#sdks}

Web SDK不仅是现有库的包装器。 它是一个全新的库，从头开始编写，以融入现有库的功能。 其目的在于终止标签必须按正确顺序触发的挑战、与库版本控制挑战不一致以及更好的依赖关系管理。 这是实施 [!DNL Experience Cloud] 而是 [开源](https://github.com/adobe/alloy).

Web SDK取代了以下SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

除了新库之外，还有一个新端点，可简化对Adobe解决方案的HTTP请求。 之前，Visitor.js向访客ID服务发送了一个阻止调用，然后AT.js向Adobe Target发送一个调用，DIL.js向Adobe Audience Manager发送一个调用，最后，AppMeasurement.js向Adobe Analytics发送了一个调用。 此新库和端点可以检索ID，获取 [!DNL Target] 体验，将数据发送到 [!DNL Audience Manager]，并在一次调用中将数据传递到Adobe Experience Platform。

以下视频演示了Adobe Experience Platform [!DNL Web SDK] 和Adobe Experience Platform [!DNL Edge Network] 中。 视频示例使用对Adobe的单个调用，该调用将数据发送到 [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]和 [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## 从现有库迁移到Web SDK {#migrating-to-web-sdk}

简化从 [现有库](#sdks) 到Web SDK， Adobe提供了一个简化的升级路径，允许您将网站的每个单独页面迁移到Web SDK，而无需同时迁移整个网站。

这意味着您可以在页面上使用Web SDK，并将现有库保留在其他页面上，直到您也可以迁移它们为止。

### at.js到Web SDK的迁移注意事项 {#considerations}

在迁移使用 [!DNL at.js] 对于Web SDK，请确保启用以下Web SDK配置选项。 这可确保在从具有 [!DNL at.js ] 到使用Web SDK的页面。

* [“idMigrationEnabled”](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [“targetMigrationEnabled”](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>从at.js迁移到Web SDK时，不支持以下Target功能：
> * [重定向选件](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en)
> * [CNAME和跨域支持](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/?lang=en)


从at.js迁移到Web SDK后，您应该删除 `targetMigrationEnabled` 选项。




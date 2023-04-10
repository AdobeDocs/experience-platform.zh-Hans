---
title: Adobe Experience Platform Web SDK常见问题解答
description: 获取有关Adobe Experience Platform Web SDK的常见问题解答。
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: a8f6bb8c3e35f4c17812ef944440210b7fe3f87b
workflow-type: tm+mt
source-wordcount: '2104'
ht-degree: 2%

---

# 常见问题解答

本指南提供了有关Adobe Experience Platform Web SDK的常见问题解答。

## 什么是Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK是一个客户端JavaScript库，它允许Adobe Experience Cloud客户与Experience Cloud中的各种服务进行交互。

它以与解决方案无关的方式(XDM)将数据发送到Adobe Experience Platform边缘网络，然后该网络将数据映射到特定于解决方案的格式和目标，并实时发送数据。

**更多信息**
[Adobe Summit演示](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Adobe Experience Platform Web SDK与以前的解决方案有何不同？

### 在Adobe Experience Platform SDK之前

目前，您必须根据每个解决方案部署不同的JavaScript库。

* 每个解决方案都有其自己的JavaScript库、架构和域。
* 这些库都不是为了彼此协同工作而构建的。
* 跨解决方案和Adobe Experience Platform用例要求这些不同的库相互依赖，从而导致部署摩擦。

尽管Platform中的标记使部署和管理这些库尽可能简单，但仍存在以下问题：

* 库大小(页面上的Adobe代码过多)
* 性能（站点加载时间过长）
* 针对单个用例的多个调用
* 在个性化调用之前等待ECID返回（导致延迟）
* 断开的数据收集（什么是evar？）
* 解决方案(A4T)之间的架构混淆
* 很多其他不太理想的事

此外，当前还没有可直接将数据发送到Adobe Experience Platform的JavaScript库。

### 使用Adobe Experience Platform Web SDK

新的Web SDK将以下解决方案的数据发送到单个目标(Adobe Experience Platform边缘网络)，并针对上述最常见的解决方案用例进行了解决。

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* 访客 ID
* Adobe Experience Platform

今年晚些时候，其他解决方案将陆续推出。

Adobe Experience Platform Web SDK还可以将数据直接发送到Adobe Experience Platform。 此数据位于XDM中，且已映射到服务器端解决方案架构。

## 此新Web SDK的价值是什么？

**性能：** Web SDK比使用所有当前Adobe库都小，并且提供了显着更快的页面加载速度。

**简单：** XDM、Web SDK、标记、Experience Edge、Adobe Experience Cloud解决方案和Adobe Experience Platform的组合，创建了一个简单易懂且易于跟踪的数据收集故事。

* **XDM:** 您用于将数据发送到Adobe的与解决方案无关的架构。 不再为evar或mbox添加标记。
* **Adobe Experience Platform Web SDK:** 可轻松地向Adobe Experience Platform边缘网络发送和接收数据。
* **标记：** 简化网站上Web SDK（和任何其他JavaScript标记）的部署和配置。
* **Experience Edge:** 轻松将数据路由到Adobe Experience Platform和解决方案，其格式为所需。
* **Adobe Experience Platform和Adobe解决方案：** 启用他们的价值主张。

**控制：** 由于所有数据都使用一个连接的数据流，因此您可以在逻辑上跟踪和控制数据在应用程序访问和访问过程中每毫秒的显示情况。

**现代化、面向未来：** Web SDK及其与Experience Edge Network的连接使Adobe能够显着地现代化Adobe处理数据收集、个性化、同意和第三方Cookie未来的方式。 (它启用由Adobe管理的第一方域。)

**价值实现时间：** Adobe一直在努力（并将继续），以尽可能轻松地通过标记部署Web SDK，并将客户端数据映射到XDM。 完成该工作后，所有其他Adobe解决方案和Adobe Experience Platform服务都可以在服务器端打开或关闭。 例如，如果您要将此代码用于Adobe Analytics，并且希望打开Target或Experience Platform，则只需翻转数据流配置上的切换开关，并点亮这些用例。

## 什么是Alloy?

Alloy是Adobe Experience Platform Web SDK的代码名称。 它在SDK的源代码和文件名中使用，但Adobe Experience Platform Web SDK是官方名称。

## 客户是否需要购买Adobe Experience Platform才能使用 [!DNL Web SDK]?

不会。任何AdobeDigital Experience客户都可以免费使用Adobe Experience Platform Web SDK。 希望使用 [!DNL Web SDK] 将需要在数据收集UI或Experience PlatformUI中配置正确的权限，以创建架构、数据集、身份命名空间和数据流。

有关配置这些权限的更多信息，请参阅 [数据收集权限管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).

## 谁应使用Web SDK?

Adobe Experience Platform Web SDK是为以下人员开发的：

* Adobe Experience Platform用户
   * 如果您需要将数据直接从设备发送到Adobe Experience Platform，则官方建议使用这种方式。
   * Adobe知道，如果客户已经拥有Adobe Analytics，则使用Adobe Analytics连接器会更快，但这不是数据收集的长期策略。

* Adobe Experience Cloud解决方案客户
   * 新的Adobe Analytics、Adobe Audience Manager和Adobe Target客户应该从新的Web SDK开始，而不是使用旧版库。
   * 如果现有客户希望尽可能获得最优化的实施，则应使用新的Web SDK。


## 如何获取开始使用Adobe Experience Platform Web SDK的访问权限？

Web SDK当前可供一般公众使用，并可用于将数据发送到Adobe Experience Cloud产品。 将数据发送到第三方解决方案的功能即将推出。 SDK不收取任何费用，并且由Adobe免费托管。 如果需要，您可以免费下载它并将其托管在自己的服务器上。 Platform Web SDK需要访问数据流配置和Adobe Experience Platform XDM架构生成器，以便Adobe的服务器能够正确处理来自SDK的入站数据。 如果您希望获得访问权限，请联系您的Adobe帐户团队以开始请求流程。

## Web SDK当前支持哪些用例？

Web SDK正在快速发展。 正在处理更多用例。 您可以在 [此处当前支持的用例列表。](https://github.com/adobe/alloy/projects/5)

## 当前客户是否必须重新标记其网站？

这依具体情况而定。Adobe Experience Platform Web SDK可以部署为两种不同的样式。 将来的迁移文档将提供更多详细信息。

* **只是另一个标记：** 如果网站已针对解决方案进行标记，且您无法重新标记，但是您希望将数据发送到Adobe Experience Platform Edge Network以供Experience Platform用例或即将推出的事件转发功能（请参阅下文），则可以添加 `alloy.js` 标记到网站，其中它只作为“其他标记”使用。

* **唯一的标记：** 如果您要将Web SDK用于Experience Cloud解决方案，则必须将其用于 _全部_ 的解决方案。 例如，如果您的网站已经为Adobe Analytics标记，并且您希望将其用于Target，则您需要将其同时用于Target，以及将来的任何其他网站。

换言之，如果您决定将Adobe Experience Platform Web SDK用于非解决方案用例，则可以使用标记网站 `alloy.js` 就象新的解决方案一样。 如果要将其用于Adobe Analytics、Target或Audience Manager，或用于应用程序用例，则可能必须删除页面上的任何旧版代码。

## 我能否在开始使用Alloy时迁移ECID，以便我的网站访客不会开始显示为新访客？

是，Adobe Experience Platform Web SDK提供了身份迁移功能。 按照 [平台Web SDK身份文档](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) 以了解更多详细信息。

## Web SDK与标记有何不同？

* **Experience Platform中的标记** 管理设备代码。 使用它们可更轻松地部署代码。 他们自由而强大。

* **Adobe Experience Platform Web SDK** 是新代码的官方名称，新代码将由标记部署以用于Adobe用例。 它也是自由和强大的。

* **`alloy.js`** 是Adobe Experience Platform Web SDK代码的文件名。

## 我是否必须使用标记来部署Web SDK?

不会。您可以下载 `alloy.js` 自己归档。

但是:

* Adobe Experience Platform Web SDK需要称为数据流ID的内容，以便边缘网络能够识别该流并确定如何处理数据。 此ID是在Experience Platform中创建的。 这并不意味着您必须使用UI创建属性或部署JavaScript代码，但是您确实需要使用标记来创建配置ID。

* 标记不仅是最佳的可用标记和SDK管理器，而且易于部署 `alloy.js` 并将数据映射到XDM模式。 如果决定不使用标记，则必须管理部署 `alloy.js`，以及在发送数据之前将其映射到XDM。 这是 _多_ 比使用标记更加困难的过程。

* 建议您使用标记进行部署 `alloy.js`，即使它是您唯一使用的标记。

## 什么是事件转发？

如果您使用我们的SDK并将XDM发送到Experience Edge，则这些新增功能事件转发允许您安装新的服务器端扩展，并将该数据映射到任何内容（并从我们的边缘网络发送到任何位置）。 可将其视为“数据收集为服务”。 此服务将可收取费用，并作为Adobe Experience Platform的一部分捆绑提供。

## 什么是CNAME或第一方域，为什么它很重要？

有关CNAME的更多信息，请参阅 [Adobe文档](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## Adobe Experience Platform Web SDK是否使用Cookie? 如果是，它会使用哪些Cookie?

是，目前Web SDK使用的Cookie介于1到7个之间的任意位置，具体取决于您的实施。 以下是您可能在Web SDK中看到的Cookie列表及其使用方式：

| **名称** | **maxAge** | **友好年龄** | **描述** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 天 | 标识Cookie存储ECID以及与ECID相关的其他信息。 |
| **kndctr_orgid_consent_check** | 7200 | 2 小时 | 此Cookie存储用户对网站的同意首选项。 |
| **kndctr_orgid_consent** | 15552000 | 180 天 | 此基于会话的Cookie表示服务器在服务器端查找同意首选项。 |
| **kndctr_orgid_cluster** | 1800 | 30 分钟 | 此Cookie存储用于提供当前用户请求的体验边缘区域。 区域用在URL路径中，以便Experience Edge能够将请求路由到正确的区域。 此Cookie的生命周期为30分钟，因此如果用户连接不同的IP地址，则请求可以路由到最接近的区域。 |
| **mbox** | 63072000 | 2 年 | 当Target迁移设置设置为true时，将显示此Cookie。 这将允许Target [mbox cookie](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) 由Web SDK设置。 |
| **mboxEdgeCluster** | 1800 | 30 分钟 | 当Target迁移设置设置为true时，将显示此Cookie。 此Cookie允许Web SDK将正确的边缘群集与at.js通信，以便当用户在网站中导航时，Target配置文件可以保持同步。 |
| **AMCV_###@AdobeOrg** | 34128000 | 395 天 | 仅当在Adobe Experience Platform Web SDK中启用ID迁移时，才会显示此Cookie。 当网站的某些部分仍在使用visitor.js时，此Cookie可在过渡到Web SDK时提供帮助。 请参阅 [idMigrationEnabled文档](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#identity-options) 以了解有关此设置的更多信息。 |

使用Web SDK时，边缘网络会设置上述一个或多个Cookie。 边缘网络会使用 `secure` 和 `sameSite="none"` 属性。

如果您网站上当前同时具有安全和非安全部分，则可能会干扰用户标识。 当用户从站点的安全区域导航到非安全区域时，边缘网络会生成一个新的 `ECID` 请求。

## Adobe Experience Platform Web SDK支持哪些浏览器？

Adobe Experience Platform Web SDK可在最新版本的Google Chrome、Safari、Firefox、Internet Explorer 11和Microsoft Edge Chromium中发挥最佳工作效果。 在较旧版本的浏览器上使用某些功能时，您可能会遇到问题。

## 在哪里可以获取有关Adobe Experience Platform Web SDK的更多信息？

* [文档](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=zh-Hans)
* [源代码](https://github.com/adobe/alloy)

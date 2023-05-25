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

## 什么是Adobe Experience Platform Web SDK？

Adobe Experience Platform Web SDK是一个客户端JavaScript库，它允许Adobe Experience Cloud的客户与Experience Cloud中的各种服务进行交互。

它将以与解决方案无关的方式(XDM)将数据发送到Adobe Experience Platform Edge Network，然后它将数据映射到解决方案特定的格式和目标，并实时发送。

**更多信息**
[Adobe Summit演示](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Adobe Experience Platform Web SDK与以前的解决方案有何不同？

### Adobe Experience Platform SDK之前的版本

目前，您必须根据每个解决方案来部署不同的JavaScript库。

* 每个解决方案都有自己的JavaScript库、架构和域。
* 这些库都不是为了相互配合而构建的。
* 跨解决方案和Adobe Experience Platform用例要求这些不同的库是相互依赖的，这会导致部署摩擦。

虽然Platform中的标记使得部署和管理这些库尽可能轻松，但以下内容仍然存在问题：

* 库大小(页面上的Adobe代码过多)
* 性能（网站加载时间过长）
* 针对单个用例的多个调用
* 在个性化调用之前等待ECID返回（导致延迟）
* 分离的数据收集（什么是evar？）
* 解决方案之间的模式混淆(A4T)
* 很多其他不太理想的事情

此外，当前还没有JavaScript库直接将数据发送到Adobe Experience Platform。

### 使用Adobe Experience Platform Web SDK

新的Web SDK可将以下解决方案的数据发送到单一目标(Adobe Experience Platform Edge Network)，并解决上述最常见的解决方案用例。

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* 访客 ID
* Adobe Experience Platform

其他解决方案将在今年晚些时候推出。

Adobe Experience Platform Web SDK也可以将数据直接发送到Adobe Experience Platform。 此数据位于XDM中，并映射到服务器端解决方案架构。

## 此新Web SDK有什么价值？

**性能：** 与使用所有当前Adobe库相比，Web SDK更小，并且页面加载速度显着加快。

**简单性：** XDM、Web SDK、标记、Experience Edge、Adobe Experience Cloud解决方案和Adobe Experience Platform的组合创建了一个易于理解和易于遵循的数据收集案例。

* **XDM：** 用于将数据发送到Adobe的独立于解决方案的架构。 不再为evar或mbox添加标记。
* **Adobe Experience Platform Web SDK：** 使向Adobe Experience Platform Edge Network发送和接收数据更轻松。
* **标记：** 简化了Web SDK（以及任何其他JavaScript标记）在站点上的部署和配置。
* **Experience Edge：** 轻松地将数据以所需的格式路由到Adobe Experience Platform和解决方案。
* **Adobe Experience Platform和Adobe解决方案：** 实现他们的价值主张。

**控制：** 由于所有数据都使用单个连接的数据流，因此您可以在逻辑上跟踪和控制数据在其往返应用程序的旅程中每一毫秒的样子。

**现代，为未来做好准备：** Web SDK及其与Experience Edge Network的连接使Adobe能够显着更新Adobe如何处理数据收集、个性化、同意和未来第三方Cookie。 (它支持由Adobe管理的第一方域。)

**实现价值的时间：** Adobe已尽力（并将继续）轻松地通过标记部署Web SDK并将客户端数据映射到XDM。 完成此工作后，可以打开或关闭服务器端的所有其他Adobe解决方案和Adobe Experience Platform服务。 例如，如果您将此项用于Adobe Analytics，并且要打开Target或Experience Platform，则只需在数据流配置上翻动切换开关即可启用这些用例。

## 什么是Alloy？

Alloy是Adobe Experience Platform Web SDK的代码名称。 虽然Adobe Experience Platform Web SDK是正式名称，但它用在SDK的源代码和文件名中。

## 客户是否需要购买Adobe Experience Platform才能使用 [!DNL Web SDK]？

不会。任何Adobe数字体验客户都可以免费使用Adobe Experience Platform Web SDK。 希望使用 [!DNL Web SDK] 将需要在数据收集UI或Experience PlatformUI中配置正确的权限来创建架构、数据集、身份命名空间和数据流。

有关配置这些权限的更多信息，请参阅我们的文档，位置如下： [数据收集权限管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).

## 谁应使用Web SDK？

Adobe Experience Platform Web SDK专为以下人员开发：

* Adobe Experience Platform用户
   * 如果您需要直接从设备向Adobe Experience Platform发送数据，官方推荐使用此方法。
   * Adobe知道，如果客户已经拥有Adobe Analytics，则使用Adobe Analytics连接器会更快，但这不是数据收集的长期策略。

* Adobe Experience Cloud解决方案客户
   * 新的Adobe Analytics、Adobe Audience Manager和Adobe Target客户应该从新的Web SDK开始，而不是使用旧版库。
   * 希望尽可能获得最佳实施的现有客户应使用新的Web SDK。


## 如何获取开始使用Adobe Experience Platform Web SDK的访问权限？

Web SDK当前可供公众使用，并可用于将数据发送到Adobe Experience Cloud产品。 在不久的将来，我们将能够向第三方解决方案发送数据。 SDK免费，由Adobe免费托管。 如果需要，您可以免费下载它并将其托管在您自己的服务器上。 Platform Web SDK需要访问数据流配置和Adobe Experience Platform XDM架构生成器，以便Adobe的服务器能够正确处理来自SDK的入站数据。 如果您希望获得访问权限，请联系您的Adobe客户团队以开始申请流程。

## Web SDK当前支持哪些用例？

Web SDK正在迅速发展。 正在处理更多用例。 您可以找到 [此处当前支持的用例列表。](https://github.com/adobe/alloy/projects/5)

## 当前客户是否必须重新标记其网站？

这依具体情况而定。Adobe Experience Platform Web SDK可以两种不同的样式进行部署。 未来的迁移文档将提供更多详细信息。

* **只是另一个标记：** 如果网站已标记为提供解决方案，并且您无法重新标记，但希望将数据发送到Adobe Experience Platform Edge Network以获取Experience Platform用例或即将推出的事件转发功能（见下文），则可以添加 `alloy.js` 标记到站点，在那里它充当“另一个标记”。

* **唯一一个标记：** 如果要将Web SDK用于Experience Cloud解决方案，则必须将其用于 _所有_ 页面上的解决方案中。 例如，如果您的网站已标记为Adobe Analytics，并且您想要将其用于Target，则您需要将其用于两者，以及将来用于任何其他网站。

换言之，如果您决定将Adobe Experience Platform Web SDK用于非解决方案用例，则可以使用以下内容标记网站 `alloy.js` 然后继续前进，好像它是一个新的解决方案。 如果要将其用于Adobe Analytics、Target、Audience Manager或应用程序用例，则可能必须删除页面上的任何旧版代码。

## 我可以在开始使用Alloy时迁移ECID，以便我的网站访客不会开始显示为新访客吗？

是，Adobe Experience Platform Web SDK提供了身份迁移功能。 按照 [Platform Web SDK身份文档](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) 了解更多详细信息。

## Web SDK与标记有何不同？

* **Experience Platform中的标记** 管理设备代码。 使用它们可更轻松地部署代码。 他们自由而强大。

* **Adobe Experience Platform Web SDK** 是标记将为Adobe用例部署的新代码的正式名称。 它也是自由和强大的。

* **`alloy.js`** 是Adobe Experience Platform Web SDK代码的文件名。

## 我是否必须使用标记来部署Web SDK？

不会。您可以下载 `alloy.js` 自己归档。

但是:

* Adobe Experience Platform Web SDK需要数据流ID，以便边缘网络能够识别流并确定如何处理数据。 此ID是在Experience Platform中创建的。 这并不意味着您必须使用UI来创建属性或部署JavaScript代码，但您确实需要使用标记来创建配置ID。

* 标记不仅是最佳可用标记和SDK管理器，而且可以让您轻松部署 `alloy.js` 将数据映射到XDM架构。 如果您决定不使用标记，则必须管理部署 `alloy.js`，事件，并在发送数据之前将数据映射到XDM。 这是 _很多_ 比使用标记更困难的过程。

* 建议您使用标记进行部署 `alloy.js`，即使它是您用于的唯一标记。

## 什么是事件转发？

如果您使用我们的SDK并将XDM发送到Experience Edge，则这些新功能事件转发允许您安装新的服务器端扩展，并将该数据映射到我们的边缘网络中的任何内容，并将其发送到任何地方。 将其视为“数据收集即服务”。 这将需要付费，并且作为Adobe Experience Platform的一部分捆绑提供。

## 什么是CNAME域或第一方域，它为什么重要？

有关CNAME的更多信息，请参阅 [Adobe文档](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## Adobe Experience Platform Web SDK是否使用Cookie？ 如果是这样，它使用哪些Cookie？

是，当前Web SDK使用介于一到七个Cookie之间的任何位置，具体取决于您的实施。 以下是您在Web SDK中可能会看到的Cookie及其使用方式的列表：

| **名称** | **maxAge** | **友好年龄** | **描述** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 天 | 标识Cookie会存储ECID以及与ECID相关的其他信息。 |
| **kndctr_orgid_consent_check** | 7200 | 2 小时 | 此Cookie存储用户对网站的同意偏好。 |
| **kndctr_orgid_consent** | 15552000 | 180 天 | 此基于会话的Cookie指示服务器查找同意首选项服务器端。 |
| **kndctr_orgid_cluster** | 1800 | 30 分钟 | 此Cookie存储为当前用户的请求提供服务的Experience Edge区域。 区域用在URL路径中，以便Experience Edge能够将请求路由到正确的区域。 此Cookie的生命周期为30分钟，因此，如果用户使用不同的IP地址连接，则请求可以路由到最近的区域。 |
| **mbox** | 63072000 | 2 年 | 当Target迁移设置设置为true时，将显示此Cookie。 这将允许Target [mbox Cookie](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) 将由Web SDK设置。 |
| **mboxEdgeCluster** | 1800 | 30 分钟 | 当Target迁移设置设置为true时，将显示此Cookie。 此Cookie允许Web SDK将正确的边缘群集与at.js进行通信，以便在用户在站点间导航时，Target配置文件可以保持同步。 |
| **AMCV_###@AdobeOrg** | 34128000 | 395 天 | 只有在Adobe Experience Platform Web SDK上启用了ID迁移后，此Cookie才会显示。 当网站某些部分仍在使用visitor.js时，此Cookie有助于过渡到Web SDK。 请参阅 [idMigrationEnabled文档](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#identity-options) 以详细了解此设置。 |

使用Web SDK时，Edge Network会设置上述一个或多个Cookie。 Edge Network将所有Cookie设置为 `secure` 和 `sameSite="none"` 属性。

如果您的网站上当前同时存在安全部分和不安全部分，这可能会干扰用户识别。 当用户从站点的安全区导航到非安全区时，边缘网络生成一个新的 `ECID` 通过请求。

## Adobe Experience Platform Web SDK支持哪些浏览器？

Adobe Experience Platform Web SDK旨在以最佳方式在Google Chrome、Safari、Firefox、Internet Explorer 11和Microsoft Edge Chromium的最新版本中工作。 在旧版本的浏览器上使用某些功能时可能会遇到问题。

## 可在何处获取有关Adobe Experience Platform Web SDK的更多信息？

* [文档](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=zh-Hans)
* [源代码](https://github.com/adobe/alloy)

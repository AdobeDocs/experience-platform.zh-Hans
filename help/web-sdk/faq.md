---
title: Adobe Experience Platform Web SDK常见问题解答
description: 获取有关Adobe Experience Platform Web SDK的常见问题解答。
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '2268'
ht-degree: 2%

---


# 常见问题解答

本指南提供有关Adobe Experience Platform Web SDK的常见问题解答。

## 什么是Adobe Experience Platform Web SDK？

Adobe Experience Platform Web SDK是一个客户端JavaScript库，通过它，可与Adobe Experience Cloud中的各种服务进行交互。

Web SDK以与解决方案无关的方式(XDM)将数据发送到Experience Platform边缘网络，然后边缘网络将数据映射到解决方案特定的格式和目标并实时发送。

请观看以下视频，以了解有关Web SDK的更多信息： [再次满足Alloy.js要求，不再为eVar或Mbox添加标记](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html).

## Adobe Experience Platform Web SDK与以前的解决方案有何不同？

### Experience PlatformWeb SDK之前

目前，您必须根据每个解决方案来部署不同的JavaScript库。

* 每个解决方案都有自己的JavaScript库、架构和域。
* 这些库都不是为了相互配合而构建的。
* 跨解决方案和Adobe Experience Platform用例要求这些不同的库是相互依赖的，这会导致部署摩擦。

虽然Platform中的标记允许尽可能轻松地部署和管理这些库，但以下内容仍然存在问题：

* 库大小(页面上的Adobe代码过多)
* 性能（站点加载时间过长）
* 针对单个用例的多个调用
* 在个性化调用之前等待ECID返回（导致延迟）
* 断开的数据收集（什么是evar？）
* 解决方案之间的模式混淆(A4T)
* 很多其他不太好的东西

此外，当前也不存在将数据直接发送到Adobe Experience Platform的JavaScript库。

### 使用Experience PlatformWeb SDK

新的Web SDK可将以下解决方案的数据发送到单一目标(Experience Platform边缘网络)，并解决上述最常见的解决方案使用案例。

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* 访客 ID
* Adobe Experience Platform

其他解决方案也将随之而来。

Adobe Experience Platform Web SDK也可以将数据直接发送到Adobe Experience Platform。 此数据采用XDM格式，并映射到服务器端解决方案架构。

## 此新Web SDK有何价值？

**性能：** 与使用所有当前Adobe库相比，Web SDK更小，并且页面加载速度显着加快。

**简单性：** XDM、Web SDK、标记、Edge Network、Adobe Experience Cloud解决方案和Adobe Experience Platform的组合创建了一个易于理解和易于遵循的数据收集故事。

* **XDM：** 用于将数据发送到Adobe的与解决方案无关的架构。 不再为evar或mbox添加标记。
* **Web SDK：** 使向Adobe Experience Platform Edge Network发送和接收数据更轻松。
* **标记：** 简化网站上Web SDK（以及任何其他JavaScript标记）的部署和配置。
* **边缘网络：** 轻松地将数据以所需的格式路由到Adobe Experience Platform和解决方案。
* **Adobe Experience Platform和Adobe解决方案：** 实现他们的价值主张。

**控制：** 由于所有数据都使用单个连接的数据流，因此您可以逻辑地跟踪和控制数据在其进出应用程序的历程中的每一毫秒所呈现出的外观。

**现代，为未来做好准备：** Web SDK及其与Edge Network的连接使Adobe能够显着实现Adobe如何处理数据收集、个性化、同意和未来第三方Cookie的现代化。 (它支持由Adobe管理的第一方域。)

**实现价值的时间：** Adobe已尽力（并将继续）让您尽可能轻松地通过标记部署Web SDK并将客户端数据映射到XDM。 完成该工作后，可在服务器端打开或关闭所有其他Adobe解决方案和Adobe Experience Platform服务。 例如，如果您将此用于Adobe Analytics并且要打开Target或Experience Platform，则只需在数据流配置上切换开关，并阐明这些用例即可。

## 什么是 [!DNL alloy.js]？

[!DNL alloy.js] 是Web SDK JavaScript库的名称。 它在SDK源代码和文件名中引用。

## 客户是否需要购买Adobe Experience Platform才能使用 [!DNL Web SDK]？

不会。任何Adobe数字体验客户都可以免费使用Adobe Experience Platform Web SDK。 希望使用 [!DNL Web SDK] 将需要在数据收集UI或Experience PlatformUI中配置创建架构、数据集、身份命名空间和数据流的正确权限。

有关配置这些权限的更多信息，请参阅我们关于的文档 [数据收集权限管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## 哪些人应该使用Web SDK？

Adobe Experience Platform Web SDK专为以下客户开发：

* Adobe Experience Platform用户
   * 如果您需要直接从设备向Adobe Experience Platform发送数据，官方建议使用此方式。
   * Adobe知道，如果您已经拥有Adobe Analytics，则使用Adobe Analytics连接器会更快，但这不是数据收集的长期策略。

* Adobe Experience Cloud解决方案客户
   * 新的Adobe Analytics、Adobe Audience Manager和Adobe Target客户应该从新的Web SDK开始，而不是使用旧版库。
   * 现有客户如果想要获得尽可能优化的实施，应使用新的Web SDK。

## 如何访问Web SDK？

Web SDK当前可供一般公众使用，并且可用于将数据发送到Adobe Experience Cloud产品。 在不久的将来，将会推出将数据发送到第三方解决方案的功能。

SDK免费，并由Adobe免费托管。 如果需要，您可以免费下载它并将其托管在您自己的服务器上。

Web SDK需要访问 [数据流配置](../datastreams/overview.md) 和Experience Platform [XDM架构生成器](../xdm/tutorials/create-schema-ui.md)，以便Adobe的服务器能够正确处理来自SDK的入站数据。 如果您希望获得访问权限，请联系您的Adobe客户团队以开始申请流程。

## Web SDK当前支持哪些用例？

Web SDK正在快速演变。 正在处理更多用例。 您可以找到 [此处当前支持的用例列表。](https://github.com/orgs/adobe/projects/18/views/1?filterQuery=)

## 当前客户是否必须重新标记其网站？

这依具体情况而定。Adobe Experience Platform Web SDK可以采用两种不同的样式进行部署。 未来的迁移文档将提供更多详细信息。

* **只是另一个标记：** 如果网站已标记了解决方案，并且您无法重新标记，但希望将数据发送到Adobe Experience Platform Edge Network以了解Experience Platform用例或即将推出的事件转发功能（请参阅下文），则可以添加 `alloy.js` 标记到站点中，它的工作方式为“只是另一个标记”。

* **唯一一个标记：** 如果要将Web SDK用于Experience Cloud解决方案，则必须将其用于 _所有_ 页面上的解决方案中。 例如，如果您的网站已为Adobe Analytics进行了标记，并且您想要将其用于Target，则以后需要将其用于这两个网站，并用于任何其他网站。

换言之，如果您决定将Adobe Experience Platform Web SDK用于非解决方案用例，则可以使用以下内容标记网站 `alloy.js` 然后继续前进，好像它是一个新的解决方案。 如果您要将其用于Adobe Analytics、Target、Audience Manager或应用程序用例，则可能需要删除页面上的任何旧版代码。

## 我可以在开始使用Web SDK时迁移ECID，以便我的网站访客不会开始显示为新访客吗？

是，Adobe Experience Platform Web SDK提供了身份迁移功能。 请按照 [Platform Web SDK身份文档](/help/web-sdk/identity/overview.md#id-migration) 以了解更多详细信息。

## Web SDK与标记有何不同？

* **Experience Platform中的标记** 管理设备代码。 使用它们可更轻松地部署代码。 他们自由而强大。

* **Adobe Experience Platform Web SDK** 是标记将为Adobe用例部署的新代码的正式名称。 它也是自由和强大的。

* **`alloy.js`** 是Adobe Experience Platform Web SDK代码的文件名。

## 我是否必须使用标记来部署Web SDK？

不会。您可以下载 `alloy.js` 自己归档吧。

但是:

* Adobe Experience Platform Web SDK需要使用数据流ID，以便边缘网络能够识别流并确定如何处理数据。 此ID是在Experience Platform中创建的。 这并不意味着您必须使用UI创建属性或部署JavaScript代码，但您确实需要使用标记来创建配置ID。

* 标记不仅是最佳的可用标记和SDK管理器，而且可以让您轻松部署 `alloy.js` 并将数据映射到XDM架构。 如果您决定不使用标记，则必须管理部署 `alloy.js`，事件，并在发送数据之前将数据映射到XDM。 这是 _很多_ 比使用标记更难处理。

* 建议您使用标记进行部署 `alloy.js`，即使它是您用于的唯一标记。

## 什么是事件转发？

如果您使用我们的SDK并将XDM发送到Edge Network，则这些新增功能事件转发允许您安装新的服务器端扩展，并将该数据映射到我们的边缘网络中的任何内容，并将其发送到任何位置。 可将其视为“数据收集即服务”。 这将收取费用，并将作为Adobe Experience Platform的一部分捆绑提供。

## 什么是CNAME或第一方域，它为什么重要？

有关CNAME的详细信息，请参阅 [Adobe文档](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html)

## Adobe Experience Platform Web SDK是否使用Cookie？ 如果是这样，它使用哪些Cookie？

是，当前Web SDK使用介于一到七个Cookie之间的任何位置，具体取决于您的实施。 以下是您在Web SDK中可能会看到的Cookie及其使用方式的列表：

| **名称** | **maxAge** | **友好年龄** | **描述** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 天 | 身份Cookie会存储ECID以及与ECID相关的其他信息。 |
| **kndctr_orgid_consent_check** | 7200 | 2 小时 | 此Cookie存储用户对网站的同意首选项。 |
| **kndctr_orgid_consent** | 15552000 | 180 天 | 此基于会话的Cookie指示服务器查找同意首选项服务器端。 |
| **kndctr_orgid_cluster** | 1800 | 30 分钟 | 此Cookie存储为当前用户的请求提供服务的边缘网络区域。 URL路径中使用区域，以便Edge Network能够将请求路由到正确的区域。 此Cookie的生命周期为30分钟，因此，如果用户使用不同的IP地址连接，则请求可以路由到最近的区域。 |
| **mbox** | 63072000 | 2 年 | 当Target迁移设置设为true时，将显示此Cookie。 这将允许Target [mbox Cookie](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) 将由Web SDK设置。 |
| **mboxEdgeCluster** | 1800 | 30 分钟 | 当Target迁移设置设为true时，将显示此Cookie。 此Cookie允许Web SDK将正确的边缘群集传递给at.js，以便在用户浏览网站时，Target配置文件可以保持同步。 |
| **AMCV_###@AdobeOrg** | 34128000 | 395 天 | 只有在Adobe Experience Platform Web SDK上启用了ID迁移后，此Cookie才会显示。 在网站的某些部分仍在使用visitor.js的情况下，当过渡到Web SDK时，此Cookie会有所帮助。 请参阅 [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md) 以了解更多信息。 |

使用Web SDK时，边缘网络设置上述一个或多个Cookie。 边缘网络使用设置所有Cookie `secure` 和 `sameSite="none"` 属性。

如果您的网站上当前同时存在安全部分和不安全部分，这可能会干扰用户识别。 当用户从网站的安全区域导航到非安全区域时，边缘网络生成新的 `ECID` 请求。

## Adobe Experience Platform Web SDK支持哪些浏览器？

Adobe Experience Platform Web SDK旨在以最佳方式在Google Chrome、Safari、Firefox、Internet Explorer 11和Microsoft Edge Chromium的最新版本中工作。 在旧版本的浏览器上使用某些功能时可能会遇到问题。

## 可在何处获取有关Adobe Experience Platform Web SDK的更多信息？

* [文档](/help/web-sdk/home.md)
* [源代码](https://github.com/adobe/alloy)

### 支持Explorer {#support-internet-explore}

此SDK使用promise ，这是一种用于通信异步任务完成情况的方法。 此 [Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 除以下内容外，所有目标浏览器均本机支持SDK使用的实施 [!DNL Internet Explorer]. 要在上使用SDK，请执行以下操作 [!DNL Internet Explorer]，您必须拥有 `window.Promise` [多填充](https://remysharp.com/2010/10/08/what-is-a-polyfill).

以确定您是否已经拥有 `window.Promise` 多填充：

1. 在中打开您的网站 [!DNL Internet Explorer].
1. 打开浏览器的调试控制台。
1. 类型 `window.Promise` 进入控制台，然后按Enter。

如果不是 `undefined` 显示，您可能已经填充了 `window.Promise`. 确定是否 `window.Promise` ，方法是在完成上述安装说明后加载您的网站。 如果SDK抛出错误，提及了某个承诺的内容，则您可能没有进行复填 `window.Promise`.

如果您已确定，则必须进行多边形填充 `window.Promise`，请在之前提供的基础代码上方包含以下脚本标记：

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

此标记会加载一个脚本，用于确保 `window.Promise` 是有效的Promise实施。

>[!NOTE]
>
>如果选择加载其他Promise实施，请确保该实施支持 `Promise.prototype.finally`.

### 支持Explorer

Adobe Experience Platform SDK使用promise ，这是一种用于通信异步任务完成情况的方法。 此 [Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 除以下内容外，所有目标浏览器均本机支持SDK使用的实施 [!DNL Internet Explorer]. 要在上使用SDK，请执行以下操作 [!DNL Internet Explorer]，您必须拥有 `window.Promise` [多填充](https://remysharp.com/2010/10/08/what-is-a-polyfill).

有一个可用于聚合填充promise的库是promise-polyfill。 请参阅 [promise-polyfill文档](https://www.npmjs.com/package/promise-polyfill) 有关如何使用NPM安装的更多信息。

>[!NOTE]
>
>如果选择加载其他Promise实施，请确保该实施支持 `Promise.prototype.finally`.
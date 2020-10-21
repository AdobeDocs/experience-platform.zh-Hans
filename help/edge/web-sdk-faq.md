---
title: Web SDK常见问题解答
seo-title: Adobe Experience PlatformWeb SDK常见问题解答
description: 关于Adobe Experience PlatformWeb SDK的常见问题
seo-description: 关于Adobe Experience PlatformWeb SDK的常见问题
translation-type: tm+mt
source-git-commit: 2e28fda40a135330054c749d73439448a55db52c
workflow-type: tm+mt
source-wordcount: '1631'
ht-degree: 3%

---


# 关于 Experience Cloud 核心服务

本常见问题解答包括经常被询问的有关AdobeWeb SDK的问题。

## 什么是Adobe Experience PlatformWeb SDK?

Adobe Experience PlatformWeb SDK是客户端JavaScript库，它允许Adobe Experience Cloud的客户与Experience Cloud中的各种服务交互。

它以解决方案不可知的方式(XDM)将数据发送到Adobe Experience Platform边缘网络，然后将数据映射到解决方案特定的格式和目标并实时发送。

**更多信息** Adobe[峰会演示文稿](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Adobe Experience PlatformWeb SDK与先前的解决方案有何不同？

### 在Adobe Experience PlatformSDK之前

目前，您必须根据每个解决方案部署不同的JavaScript库。

* 每个解决方案都有自己的JavaScript库、模式和域。
* 这些图书馆都不是为了相互合作而建的。
* 跨解决方案和Adobe Experience Platform使用案例要求这些相互独立的库相互依赖，从而导致部署摩擦。

尽管Adobe Experience Platform Launch使部署和管理这些库变得尽可能容易，但仍有以下问题：

* 库大小(页面上的Adobe代码过多)
* 性能（站点加载时间过长）
* 针对单个用例的多次调用
* 在个性化呼叫之前等待ECID返回（导致延迟）
* 断开的数据收集（evar是什么？）
* 解决方案之间的模式混淆(A4T)
* 其他很多不那么理想的事

此外，目前还没有直接将数据发送到Adobe Experience Platform的JavaScript库。

### 使用Adobe Experience PlatformWeb SDK

新的Web SDK将以下解决方案的数据发送到单个目标(AEP Edge Network)，并针对最常见的上述解决方案使用情形进行了解决。

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Visitor ID
* Adobe Experience Platform

今年晚些时候还将推出其他解决方案。

Adobe Experience PlatformWeb SDK还可以直接将数据发送到Adobe Experience Platform。 此数据位于XDM中，并映射到服务器端解决方案模式。

## 此新Web SDK有何价值？

**性能：** Web SDK比使用所有当前Adobe库更小，并提供显着更快的页面加载。

**简单：** XDM、Web SDK、Experience Platform Launch、Experience Edge、Adobe Experience Cloud解决方案和Adobe Experience Platform的结合创建了一个易于理解和跟踪的数据收集故事。

* **XDM:** 用于向Adobe发送数据的与解决方案无关的模式。 无需再为evar或mbox添加标签。
* **Web SDK:** 便于向Adobe Experience Platform边缘网络发送和接收数据。
* **Experience Platform Launch:** 简化网站上Web SDK（和任何其他JavaScript标记）的部署和配置。
* **体验优势：** 轻松将数据以所需格式发送到Adobe Experience Platform和解决方案。
* **Adobe Experience Platform和Adobe解决方案：** 支持他们的价值主张。

**控制：** 由于所有数据都使用单一且连接的数据流，因此您可以逻辑上跟踪和控制数据在数据进出应用程序的每一毫秒的显示效果。

**现代化、面向未来：** Web SDK及其与Experience Edge Network的连接使Adobe能够大大实现Adobe处理数据收集、个性化、同意和第三方Cookie的未来的现代化。 (它启用由Adobe管理的第一方域。)

**价值转化时间：** Adobe已努力（并将继续）通过Experience Platform Launch部署Web SDK并将客户端数据映射到XDM。  完成该工作后，所有其他Adobe解决方案和Adobe Experience Platform服务都可在服务器端打开或关闭。 例如，如果您正在为Adobe Analytics使用此功能，并且要打开目标或Experience Platform，您只需打开Experience Edge配置的一个切换开关，然后启动这些用例。

## 什么是 `alloy.js`?

`Alloy.js` 是Adobe Experience Platform网络SDK的文件名。 Adobe Experience PlatformWeb SDK是官方名称，但许多开发者称它为“合金”。

## 客户需要购买Adobe Experience Platform才能使用Web SDK?

否。任何Adobe数字体验客户都可以使用它。 完全自由。 任何希望使用Web SDK的客户都将有权在Adobe Experience PlatformUI中创建模式和数据集。

## 谁应使用Web SDK?

Adobe Experience PlatformWeb SDK是为以下人员开发的：

* Adobe Experience Platform用户

   如果您需要直接从设备向Adobe Experience Platform发送数据，官方推荐使用这种方式。

   Adobe知道，如果客户已经拥有Adobe Analytics，则使用Adobe Analytics连接器会更快，但它不是数据收集的长期策略。

* Adobe Experience Cloud解决方案客户

   新Adobe Analytics、Adobe Audience Manager和Adobe Target客户应使用新的Web SDK进行开始，而不要使用旧版库。

   希望获得尽可能最优化实施的现有客户应使用新的Web SDK。


## 如何使用Adobe Experience PlatformWeb SDK访问开始?

Web SDK目前对公众可用，可用于向Adobe Experience Cloud产品发送数据。 不久的将来，将数据发送到第三方解决方案的能力将会到来。 如果您想要访问Web SDK，请与您的认证软件经理(CSM)联系以开始请求过程。

## Web SDK当前支持哪些用例？

Web SDK正在快速发展。 正在开发更多使用案例。 您可以在此处 [找到当前支持的使用案例列表。](https://github.com/adobe/alloy/projects/5)

## 当前客户是否必须重新标记其站点？

这依具体情况而定。Adobe Experience PlatformWeb SDK可以部署为两种不同的样式。 将来的迁移文档将提供更多详细信息。

* **只是另一个标签：** 如果该站点已标记有解决方案并且您无法重新标记，但您希望将数据发送到Adobe Experience Platform边缘网络以供Experience Platform使用案例或即将推出的Experience Platform Launch服务器端功能（见下文），则可以将标记添加到该站点，在该站点中，它将作为“另一个标记”工作。 `alloy.js`

* **唯一的标签：** 如果要将Web SDK用于Experience Cloud解决方案，则必须将它用 _于该页_ 上的所有解决方案。 例如，如果您的网站已标记为Adobe Analytics，并且您希望将其用于目标，则您需要将其用于这两个站点，以及将来的任何其他站点。

换言之，如果您决定将Adobe Experience PlatformWeb SDK用于非解决方案用例，则可以用标记站点 `alloy.js` ，并像使用新解决方案一样继续工作。 如果要将其用于Adobe Analytics、目标或Audience Manager，或用于应用程序用例，您可能必须删除页面上的任何旧代码。

## 当我使用合金进行开始时，是否可以迁移ECID，以便我的网站访客不会将开始显示为新访客?

是的，Adobe Experience PlatformWeb SDK提供身份迁移功能。 请按照此文档 [中的说明](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/identity.html#id-migration) ，了解详细信息。

## Web SDK与Adobe Experience Platform Launch有何不同？

* **Experience Platform Launch** 是设备代码管理器。 使用它更轻松地部署代码。 它自由而强大。

* **Adobe Experience Platform** Web SDK是Experience Platform Launch将为Adobe用例部署的新代码的正式名称。 它也是自由和强大的。

* **`alloy.js`** 是Adobe Experience Platform网络SDK代码的文件名。

## 我是否必须使用Adobe Experience Platform Launch部署Web SDK?

否。您可以自己下 `alloy.js` 载文件。

但是：

* Adobe Experience PlatformWeb SDK需要一种称为Experience Edge配置ID的工具，这样边缘网络就可以识别流并确定如何处理数据。 此ID是在Experience Platform Launch中创建的。 这并不意味着您必须使用Experience Platform Launch来创建属性或部署JavaScript代码，但您确实需要使用Experience Platform Launch来创建配置ID。

* Adobe Experience Platform Launch不仅是最佳的可用标签和SDK管理器，它还使得部署数据并将数据映射 `alloy.js` 到XDM模式变得非常容易。 如果您决定不使用Experience Platform Launch，则必须先管理的部 `alloy.js`署、事件处理以及将数据映射到XDM，然后再发送数据。 这比使用 _Experience Platform Launch_ ，要困难得多。

* 建议您使用Experience Platform Launch进行部 `alloy.js`署，即使它是您唯一使用它的标记。

## 什么是“Adobe Experience Platform Launch服务器端”?

2020年晚些时候，Experience Platform Launch将发布服务器端转发功能。 如果您使用我们的SDK并将XDM发送到Experience Edge，这些新增功能将允许您安装新的服务器端扩展并将数据映射到任何内容，并从我们的边缘网络将其发送到任何地方。 将其视为“数据收集为服务”。  这项服务将收取费用，并作为Adobe Experience Platform的一部分进行捆绑。

## 什么是CNAME或第一方域，它为何重要？

有关CNAME的更多信息，请参阅 [Adobe文档](https://docs.adobe.com/content/help/zh-Hans/id-service/using/reference/analytics-reference/cname.html)

## 哪里可以获取有关Adobe Experience PlatformWeb SDK的更多信息？

* [文档](https://docs.adobe.com/content/help/zh-Hans/experience-platform/edge/home.html)
* [源代码](https://github.com/adobe/alloy)

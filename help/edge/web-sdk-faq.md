---
title: Adobe Experience Platform Web SDK常见问题解答
description: 获取有关Adobe Experience Platform Web SDK的常见问题解答。
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 2%

---


# 关于 Experience Cloud 核心服务

本指南提供有关Adobe Experience Platform Web SDK的常见问题解答。

## 什么是Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK是客户端JavaScript库，它允许Adobe Experience Cloud客户与Experience Cloud中的各种服务交互。

它以解决方案不可知的方式(XDM)将数据发送到Adobe Experience Platform Edge Network，然后将数据映射到解决方案特定的格式和目标并实时发送。

**更多信**
[息Adobe峰会演示](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Adobe Experience Platform Web SDK与以前的解决方案有何不同？

### 在Adobe Experience Platform SDK之前

目前，您必须根据每个解决方案部署不同的JavaScript库。

* 每个解决方案都有其自己的JavaScript库、模式和域。
* 这些图书馆都不是为了彼此合作而建的。
* 跨解决方案和Adobe Experience Platform使用案例需要这些相互独立的库相互依存，从而导致部署摩擦。

尽管Adobe Experience Platform Launch使部署和管理这些库变得尽可能简单，但仍存在以下问题：

* 库大小(页面上的Adobe代码过多)
* 性能（站点加载时间过长）
* 针对单个用例的多次调用
* 等待ECID在个性化呼叫前返回（导致延迟）
* 断开的数据收集（什么是evar？）
* 解决方案之间的模式混淆(A4T)
* 其他很多不那么理想的事

此外，目前还没有直接将数据发送到Adobe Experience Platform的JavaScript库。

### 使用Adobe Experience Platform Web SDK

新的Web SDK将以下解决方案的数据发送到单个目标(Adobe Experience Platform Edge Network)，并针对最常见的上述解决方案用例进行了解决。

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Visitor ID
* Adobe Experience Platform

今年晚些时候还将推出其他解决方案。

Adobe Experience Platform Web SDK还可以直接将数据发送到Adobe Experience Platform。 此数据位于XDM中，并映射到服务器端解决方案模式。

## 此新Web SDK的价值何在？

**性能：** Web SDK比使用所有当前Adobe库小，并且提供了显着更快的页面加载。

**简单：** XDM、Web SDK、Experience Platform Launch、Experience Edge、Adobe Experience Cloud解决方案和Adobe Experience Platform的结合创建了一个易于理解和跟踪的数据收集故事。

* **XDM：用** 于向Adobe发送数据的与解决方案无关的模式。无需再为evar或mbox添加标签。
* **Adobe Experience Platform Web SDK:** 使向Adobe Experience Platform Edge Network发送和接收数据更简单。
* **Experience Platform Launch:** 简化站点上Web SDK（和任何其他JavaScript标签）的部署和配置。
* **体验边缘：** 轻松将数据以所需的格式发送到Adobe Experience Platform和解决方案。
* **Adobe Experience Platform和Adobe解决方案：实** 现他们的价值主张。

**控制：** 由于所有数据都使用单一且连接的数据流，因此您可以逻辑上跟随和控制数据在数据往返应用程序的每一毫秒中的显示。

**现代且面向未来：** Web SDK及其与Experience Edge Network的连接使Adobe能够使Adobe处理数据收集、个性化、同意和第三方Cookie未来的方式大幅现代化。(它启用由Adobe管理的第一方域。)

**时间到价值：** Adobe努力（并将继续），以尽可能轻松地通过Experience Platform Launch部署Web SDK，并将客户端数据映射到XDM。完成该工作后，所有其他Adobe解决方案和Adobe Experience Platform服务都可以在服务器端打开或关闭。 例如，如果您将此功能用于Adobe Analytics，并且要打开目标或Experience Platform，您只需打开Experience Edge配置上的切换开关，然后启动这些用例。

## 什么是合金？

Alloy是Adobe Experience Platform Web SDK的代码名。 它用在SDK的源代码和文件名中，但Adobe Experience Platform Web SDK是官方名称。

## 客户是否需要购买Adobe Experience Platform才能使用Web SDK?

否。任何Adobe数字体验客户都可以使用它。 完全自由。 任何希望使用Web SDK的客户都将有权在Adobe Experience Platform UI中创建模式和数据集。

## 谁应使用Web SDK?

Adobe Experience Platform Web SDK是为以下人员开发的：

* Adobe Experience Platform用户

   如果您需要将数据从设备直接发送到Adobe Experience Platform，官方推荐使用此方式。

   Adobe知道，如果客户已经拥有Adobe Analytics，则使用Adobe Analytics连接器会更快，但它不是数据收集的长期策略。

* Adobe Experience Cloud解决方案客户

   新的Adobe Analytics、Adobe Audience Manager和Adobe Target客户应使用新的Web SDK进行开始，而不要使用旧版库。

   希望获得尽可能优化的实施的现有客户应使用新的Web SDK。


## 如何使用Adobe Experience Platform Web SDK访问开始?

Web SDK目前对公众可用，并可用于向Adobe Experience Cloud产品发送数据。 将数据发送到第三方解决方案的能力即将到来。 SDK是免费的，由Adobe免费托管，并且可以下载，这样您就可以在自己的服务器上免费托管它（如果需要）。 平台Web SDK需要访问平台边缘网络配置和Adobe Experience Platform XDM模式构建器，以便Adobe的服务器正确处理来自SDK的入站数据。 如果您希望获得访问权限，请联系您的客户成功经理(CSM)以开始请求流程。

## Web SDK当前支持哪些用例？

Web SDK正在迅速发展。 正在制定更多使用案例。 您可以在此处找到当前支持的[使用案例列表。](https://github.com/adobe/alloy/projects/5)

## 当前客户是否必须重新标记其网站？

这依具体情况而定。Adobe Experience Platform Web SDK可以部署为两种不同的样式。 将来的迁移文档将提供更多详细信息。

* **只是另一个标**  `alloy.js` 签：如果站点已为解决方案添加标签，您无法重新添加标签，但您希望将数据发送到Adobe Experience Platform Edge Network以备Experience Platform用例或即将推出的Experience Platform Launch服务器端功能（见下文），则可以将标签添加到站点，在站点中，它将作为“其他标签”工作。

* **唯一的标签：如** 果要将Web SDK用于Experience Cloud解决方案，则必须将它用于该 __ 页上的所有解决方案。例如，如果您的站点已标记为Adobe Analytics，并且您希望将其用于目标，则您需要同时将其用于这两个站点，以及将来的任何其他站点。

换句话说，如果您决定将Adobe Experience Platform Web SDK用于非解决方案用例，则可以用`alloy.js`标记站点并像使用新解决方案一样继续工作。 如果要将它用于Adobe Analytics、目标或Audience Manager，或用于应用程序用例，您可能需要删除页面上的任何旧代码。

## 当我使用Alloy进行开始时，我是否可以迁移ECID，以便我的网站访客不会以新访客的形式显示开始?

是的，Adobe Experience Platform Web SDK提供身份迁移功能。 有关更多详细信息，请按照[平台Web SDK标识文档](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration)中有关ID迁移的说明进行操作。

## Web SDK与Adobe Experience Platform Launch有何不同？

* **Experience Platform** 启动是设备代码管理器。使用它更轻松地部署代码。 它自由而强大。

* **Adobe Experience Platform Web** SDK是Experience Platform Launch将为Adobe用例部署的新代码的正式名称。它也是免费和强大的。

* **`alloy.js`** 是Adobe Experience Platform Web SDK代码的文件名。

## 是否必须使用Adobe Experience Platform Launch来部署Web SDK?

否。您可以自己下载`alloy.js`文件。

但是：

* Adobe Experience Platform Web SDK需要一种称为Experience Edge配置ID的工具，这样边缘网络就可以识别流并确定如何处理数据。 此ID是在Experience Platform Launch中创建的。 这并不意味着您必须使用Experience Platform Launch创建属性或部署JavaScript代码，但您确实需要使用Experience Platform Launch创建配置ID。

* Adobe Experience Platform Launch不仅是最佳的可用标签和SDK管理器，还使部署`alloy.js`和将数据映射到XDM模式变得非常容易。 如果您决定不使用Experience Platform Launch，则必须先管理`alloy.js`的部署、事件处理以及将数据映射到XDM，然后再发送数据。 这是比使用Experience Platform Launch更难的&#x200B;__&#x200B;过程。

* 建议您使用Experience Platform Launch部署`alloy.js`，即使它是您使用它的唯一标记。

## 什么是“Adobe Experience Platform Launch服务器端？

2020年晚些时候，Experience Platform Launch将发布服务器端转发功能。 如果您使用我们的SDK并将XDM发送到Experience Edge，这些新增功能将允许您安装新的服务器端扩展并将数据映射到来自我们边缘网络的任何内容，并将其发送到任何位置。 将其视为“数据收集为服务”。  此服务将收取费用，并作为Adobe Experience Platform的一部分进行捆绑。

## 什么是CNAME或第一方域，它为何重要？

[Adobe文档](https://docs.adobe.com/content/help/zh-Hans/id-service/using/reference/analytics-reference/cname.html)中提供了有关CNAME的更多信息

## Adobe Experience Platform Web SDK是否使用cookies? 如果是，它使用什么Cookie?

是的，目前Web SDK使用1-4个cookie之间的任意位置，具体取决于您的实施。 以下是Web SDK中可能显示的4个Cookie的列表及其使用方式：

**kndct_orgid_identity：标** 识cookie用于存储ECID以及与ECID相关的其他一些信息。

**kndctr_orgid_connence:** 此Cookie存储用户对网站的同意首选项。

**kndctr_orgid_personalization：此** Cookie包含Adobe Target用于个性化网页的会话信息。

**kndctr_orgid_anconventcheck：此基** 于会话的cookie指示服务器查找同意首选项服务器端。

## 哪里可以获取有关Adobe Experience Platform Web SDK的更多信息？

* [文档](https://docs.adobe.com/content/help/zh-Hans/experience-platform/edge/home.html)
* [源代码](https://github.com/adobe/alloy)

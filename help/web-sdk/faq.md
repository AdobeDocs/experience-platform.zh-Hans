---
title: Adobe Experience Platform Web SDK常见问题解答
description: 获取有关Adobe Experience Platform Web SDK的常见问题解答。
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 2%

---

# 常见问题解答

本指南提供有关Adobe Experience Platform Web SDK的常见问题解答。

## 什么是Adobe Experience Platform Web SDK？

Adobe Experience Platform Web SDK是一个客户端JavaScript库，它允许您与Adobe Experience Cloud中的各种服务进行交互。

Web SDK以与解决方案无关的方式(XDM)将数据发送到Experience Platform Edge Network，会将数据映射到解决方案特定的格式和目标，并实时发送。

请观看以下视频，以了解有关Web SDK的更多信息：[再次体验eVar或Mbox的Alloy.js和从不标记](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)。

## Adobe Experience Platform Web SDK与以前的解决方案有何不同？

### 使用Experience Platform Web SDK之前

目前，您必须根据各个解决方案来部署不同的JavaScript库。

* 每个解决方案都有自己的JavaScript库、架构和域。
* 这些库都不是为了相互配合而构建的。
* 跨解决方案和Adobe Experience Platform用例要求这些不同的库是相互依赖的，这会导致部署摩擦。

虽然Experience Platform中的标记允许尽可能轻松地部署和管理这些库，但以下内容仍然存在问题：

* 库大小(页面上的Adobe代码过多)
* 性能（站点加载时间过长）
* 针对单个用例的多个调用
* 在个性化调用之前等待ECID返回（导致延迟）
* 断开的数据收集（什么是evar？）
* 解决方案之间的模式混淆(A4T)
* 很多其他不太好的东西

此外，当前也不存在将数据直接发送到Adobe Experience Platform的JavaScript库。

### 使用Experience Platform Web SDK

新的Web SDK可将以下解决方案的数据发送到单一目标(Experience Platform Edge Network)，并解决上述最常见的解决方案使用案例。

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* 访客 ID
* Adobe Experience Platform

其他解决方案也将随之而来。

Adobe Experience Platform Web SDK也可以将数据直接发送到Adobe Experience Platform。 此数据采用XDM格式，并映射到服务器端解决方案架构。

## 这个新的Web SDK有什么价值？

**性能：** Web SDK比使用所有当前Adobe库都要小，并且页面加载速度更快。

**简单性：** XDM、Web SDK、标记、Edge Network、Adobe Experience Cloud解决方案和Adobe Experience Platform的组合创建了一个易于理解和易于遵循的数据收集故事。

* **XDM：**&#x200B;用于将数据发送到Adobe的与解决方案无关的架构。 不再为evar或mbox添加标记。
* **Web SDK：**&#x200B;使向Adobe Experience Platform Edge Network发送和接收数据更容易。
* **标记：**&#x200B;简化了Web SDK(以及任何其他JavaScript标记)在站点上的部署和配置。
* **Edge Network：**&#x200B;以所需的格式将数据轻松路由到Adobe Experience Platform和解决方案。
* **Adobe Experience Platform和Adobe解决方案：**&#x200B;启用其价值主张。

**控制：**&#x200B;由于所有数据都使用单个连接的数据流，因此您可以在逻辑上跟踪和控制数据在其往返应用程序的历程中的每一毫秒所呈现出的外观。

**现代，并为未来做好准备：** Web SDK及其与Edge Network的连接使Adobe能够显着更新Adobe处理数据收集、个性化、同意和未来第三方Cookie的方式。 (它支持由Adobe管理的第一方域。)

**实现价值时间：** Adobe已努力（并将继续）尽可能轻松地通过标记部署Web SDK并将客户端数据映射到XDM。 完成此工作后，可以在服务器端打开或关闭所有其他Adobe解决方案和Adobe Experience Platform服务。 例如，如果您将此用于Adobe Analytics并且要打开Target或Experience Platform，则只需在数据流配置上切换开关，并突出显示这些用例。

## 什么是 [!DNL alloy.js]？

[!DNL alloy.js]是Web SDK JavaScript库的名称。 在SDK源代码和文件名中引用。

## 客户是否需要购买Adobe Experience Platform才能使用[!DNL Web SDK]？

不会。任何Adobe Digital Experience客户都可以免费使用Adobe Experience Platform Web SDK。

* 具有&#x200B;*非*&#x200B;访问权限且希望使用[!DNL Web SDK]的Experience Platform或Real-time CDP客户将需要配置正确权限，才能在数据收集UI或Experience Platform UI中创建架构和数据流。
* 有权访问Experience Platform或Real-time CDP并希望使用[!DNL Web SDK]的客户将需要配置正确权限，以便在Experience Platform UI或Data Collection UI中创建架构、数据集、身份命名空间和数据流。

有关配置这些权限的详细信息，请参阅我们关于[数据收集权限管理](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=zh-Hans)的文档。

## 谁应该使用Web SDK？

Adobe Experience Platform Web SDK专为以下客户开发：

* Adobe Experience Platform用户
   * 如果您需要直接从设备向Adobe Experience Platform发送数据，官方建议使用此方式。
   * Adobe知道，如果您已经拥有Adobe Analytics，则使用Adobe Analytics连接器会更快，但这不是数据收集的长期策略。

* Adobe Experience Cloud解决方案客户
   * 新的Adobe Analytics、Adobe Audience Manager和Adobe Target客户应该从新的Web SDK开始，而不是使用旧版库。
   * 现有客户如果想要获得尽可能优化的实施，则应使用新的Web SDK。

## 如何访问Web SDK？

Web SDK当前可供一般公众使用，并可用于将数据发送到Adobe Experience Cloud产品。 在不久的将来，将会推出将数据发送到第三方解决方案的功能。

SDK免费，由Adobe免费托管。 如果需要，您可以免费下载它并将其托管在您自己的服务器上。

Web SDK需要访问[数据流配置](../datastreams/overview.md)和Experience Platform [XDM架构生成器](../xdm/tutorials/create-schema-ui.md)，以便Adobe的服务器能够正确处理来自SDK的入站数据。 如果您希望获得访问权限，请联系您的Adobe客户团队以开始请求流程。

## Web SDK当前支持哪些用例？

Web SDK正在快速演变。 正在处理更多用例。 您可以在此处找到当前支持的[用例列表。](https://github.com/orgs/adobe/projects/18/views/1?filterQuery=)

## 当前客户是否必须重新标记其网站？

视情况而定。 Adobe Experience Platform Web SDK可以采用两种不同的样式进行部署。 未来的迁移文档将提供更多详细信息。

* **只是另一个标记：**&#x200B;如果网站已针对解决方案进行了标记，并且您无法重新标记，但您希望将数据发送到Adobe Experience Platform Edge Network以用于Experience Platform用例或即将推出的事件转发功能（见下文），则可以将`alloy.js`标记添加到该网站，它在其中用作“只是另一个标记”。

* **唯一一个标记：**&#x200B;如果要将Web SDK用于Experience Cloud解决方案，必须将其用于该页面上的&#x200B;_所有_&#x200B;解决方案。 例如，如果您的网站已为Adobe Analytics进行了标记，并且您想要将其用于Target，则以后需要将其用于这两个网站，并用于任何其他网站。

换言之，如果您决定将Adobe Experience Platform Web SDK用于非解决方案用例，则可以使用`alloy.js`标记网站，并像使用新解决方案一样继续操作。 如果您要将其用于Adobe Analytics、Target、Audience Manager或应用程序用例，则可能必须在您的页面上删除任何旧版代码。

## 我可以在开始使用Web SDK时迁移ECID，以便我的网站访客不会开始显示为新访客吗？

是，Adobe Experience Platform Web SDK提供了身份迁移功能。 有关更多详细信息，请按照[Experience Platform Web SDK标识文档](/help/web-sdk/identity/overview.md#id-migration)中有关ID迁移的说明操作。

## Web SDK与标记有何不同？

* Experience Platform **中的**&#x200B;标记管理设备代码。 使用它们可更轻松地部署代码。 他们自由而强大。

* **Adobe Experience Platform Web SDK**&#x200B;是标记将为Adobe用例部署的新代码的正式名称。 它也是自由和强大的。

* **`alloy.js`**&#x200B;是Adobe Experience Platform Web SDK代码的文件名。

## 我是否必须使用标记来部署Web SDK？

不会。您可以自行下载`alloy.js`文件。

但是：

* Adobe Experience Platform Web SDK需要使用数据流ID，以便边缘网络能够识别流并确定如何处理数据。 此ID是在Experience Platform中创建的。 这并不意味着您必须使用UI创建资产或部署JavaScript代码，但您确实需要使用标记来创建配置ID。

* 标记不仅是最佳可用标记和SDK Manager，它还使得部署`alloy.js`并将数据映射到XDM架构非常容易。 如果您决定不使用标记，则必须在发送数据之前管理部署`alloy.js`、事件和将数据映射到XDM。 与使用标记相比，这是一个&#x200B;_多得多的过程_。

* 建议使用标记来部署`alloy.js`，即使它是您用于的唯一标记。

## 什么是事件转发？

如果您使用我们的SDK并将XDM发送到Edge Network，则这些新功能事件转发允许您安装新的服务器端扩展，并将该数据映射到我们的边缘网络中的任何内容，并将该数据发送到任何位置。 可将其视为“数据收集即服务”。 这将收取费用，并将作为Adobe Experience Platform的一部分捆绑提供。

## 什么是CNAME或第一方域，它为什么重要？

有关CNAME的详细信息，请参阅[Adobe文档](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html?lang=zh-Hans)

## Adobe Experience Platform Web SDK是否使用Cookie？ 如果是这样，它使用哪些Cookie？

是，当前Web SDK会根据您的实施在1到7个Cookie之间的任意位置使用。 以下是您在Web SDK中可能会看到的Cookie及其使用方式列表：

| **名称** | **maxAge** | **友好年龄** | **描述** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 天 | 身份Cookie会存储ECID以及与ECID相关的其他信息。 |
| **kndctr_orgid_consent_check** | 7200 | 2 小时 | 此基于会话的Cookie指示服务器查找同意首选项服务器端。 |
| **kndctr_orgid_consent** | 15552000 | 180 天 | 此Cookie存储用户对网站的同意首选项。 |
| **kndctr_orgid_cluster** | 1800 | 30 分钟 | 此Cookie存储为当前用户的请求提供服务的Edge Network区域。 URL路径中使用区域，以便Edge Network能够将请求路由到正确的区域。 此Cookie的生命周期为30分钟，因此，如果用户使用不同的IP地址连接，则请求可以路由到最近的区域。 |
| **mbox** | 63072000 | 2 年 | 当Target迁移设置设为true时，将显示此Cookie。 这将允许Web SDK设置Target [mbox Cookie](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/)。 |
| **mboxEdgeCluster** | 1800 | 30 分钟 | 当Target迁移设置设为true时，将显示此Cookie。 此Cookie允许Web SDK将正确的边缘群集与at.js进行通信，以便在用户在站点间导航时，Target配置文件可以保持同步。 |
| **AMCV_###@AdobeOrg** | 34128000 | 395 天 | 只有在Adobe Experience Platform Web SDK上启用了ID迁移后，此Cookie才会显示。 在网站的某些部分仍在使用visitor.js的情况下，当过渡到Web SDK时，此Cookie会很有帮助。 有关详细信息，请参阅[`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md)。 |

使用Web SDK时，Edge Network会设置上述一个或多个Cookie。 Edge Network使用`secure`和`sameSite="none"`属性设置所有Cookie。

如果您的网站上当前同时存在安全部分和不安全部分，这可能会干扰用户识别。 当用户从网站的安全区域导航到非安全区域时，Edge Network会使用请求生成新的`ECID`。

## Adobe Experience Platform Web SDK支持哪些浏览器？

Adobe Experience Platform Web SDK旨在以最佳方式在Google Chrome、Safari、Firefox和Microsoft Edge Chromium的最新版本中工作。 在旧版本的浏览器或已弃用的浏览器（如Internet Explorer）上使用某些功能时，可能会遇到问题。

## 可在何处获取有关Adobe Experience Platform Web SDK的更多信息？

* [文档](/help/web-sdk/home.md)
* [Source代码](https://github.com/adobe/alloy)

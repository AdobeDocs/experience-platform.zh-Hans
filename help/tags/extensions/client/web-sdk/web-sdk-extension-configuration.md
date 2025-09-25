---
title: 配置Web SDK标记扩展
description: 了解如何在标记UI中配置Experience Platform Web SDK标记扩展。
exl-id: 22425daa-10bd-4f06-92de-dff9f48ef16e
source-git-commit: 7c2afd6d823ebb2db0fabb4cc16ef30bcbfeef13
workflow-type: tm+mt
source-wordcount: '3107'
ht-degree: 3%

---

# 配置Web SDK标记扩展

[!DNL Web SDK]标记扩展通过Experience Platform Edge Network从Web资产向Adobe Experience Cloud发送数据。

该扩展允许您将数据流式传输到Experience Platform中、同步身份、处理客户同意信号并自动收集上下文数据。

本文档介绍如何在标记UI中配置标记扩展。

## 安装Web SDK标记扩展 {#install}

Web SDK标记扩展需要在上安装资产。 如果您尚未这样做，请参阅有关[创建标记属性](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html?lang=zh-Hans)的文档。

创建属性后，打开该属性并选择左侧栏上的&#x200B;**[!UICONTROL 扩展]**&#x200B;选项卡。

选择&#x200B;**[!UICONTROL 目录]**&#x200B;选项卡。 从可用扩展列表中，找到[!DNL Web SDK]扩展并选择&#x200B;**[!UICONTROL 安装]**。

![显示选择了Web SDK扩展的Tags UI的图像](assets/web-sdk-install.png)

选择&#x200B;**[!UICONTROL 安装]**&#x200B;后，必须配置Web SDK标记扩展并保存配置。

>[!NOTE]
>
>标记扩展仅在保存配置后进行安装。 请参阅以下部分，了解如何配置标记扩展。

## 创建自定义Web SDK内部版本 {#custom-build}

Web SDK库包含多个模块，用于提供各种功能，如个性化、身份识别、链接跟踪等。 根据您的用例，您可能只需要特定功能，而无需整个库。 通过创建自定义Web SDK内部版本，您可以仅选择所需的模块，从而减小库大小并提高性能。

创建自定义Web SDK内部版本时，该内部版本将由您的所有Web SDK实例使用。

>[!IMPORTANT]
>
>禁用Web SDK组件可能会破坏现有的实施。 每次禁用组件时，请确保彻底测试实施，以确保所需的所有功能都按预期工作。
>&#x200B;>禁用某个组件后，无法再编辑该组件的设置。

要使用Web SDK标记扩展创建自定义Web SDK内部版本，请执行以下步骤。

1. 在标记扩展配置页面中，展开&#x200B;**[!UICONTROL 自定义生成组件]**&#x200B;部分。
1. 根据需要启用或禁用组件。 您可以从以下组件中进行选择：
   * **[!UICONTROL Activity收集器]**：此组件启用自动链接收集和Activity Map跟踪。
   * **[!UICONTROL Advertising]**：此组件包含Adobe Advertising所需的所有JavaScript代码。 它还在[!UICONTROL Adobe Advertising实例]部分中添加了[!UICONTROL SDK]设置，在标记规则中添加了[!UICONTROL Advertising]设置，以定义如何将广告数据用于归因测量。
   * **[!UICONTROL 受众]**：此组件支持Audience Manager集成，包括URL和基于Cookie的目标以及ID同步。
   * **[!UICONTROL 同意]**：此组件启用同意集成。 禁用此组件将禁用以下元素：
      * [设置同意](action-types.md#set-consent)操作类型
   * **[!UICONTROL 上下文]**：此组件启用上下文数据的自动收集。
   * **[!UICONTROL 事件合并]**： _已弃用_。 禁用此组件将禁用以下元素：
      * [事件合并ID](action-types.md#data)数据元素
      * **[!UICONTROL 重置事件合并ID]**&#x200B;操作类型
   * **[!UICONTROL Media Analytics桥]**：此组件使用Media Analytics界面启用Edge Network Streaming Media。 禁用此组件将禁用以下元素：
      * [获取Media Analytics跟踪器](action-types.md#get-media-analytics-tracker)操作类型
   * **[!UICONTROL Personalization]**：此组件启用Adobe Target和Adobe Journey Optimizer集成。 禁用此组件将禁用以下元素：
      * [应用建议](action-types.md#apply-propositions)操作类型
   * **[!UICONTROL 推送通知]**：此组件启用Adobe Journey Optimizer的Web推送通知。
   * **[!UICONTROL 规则引擎]**：此组件启用Adobe Journey Optimizer设备上决策。 禁用此组件将禁用以下元素：
      * [评估规则集](action-types.md#evaluate-rulesets)操作类型
      * [订阅规则集项](event-types.md#subscribe-ruleset-items)事件类型
   * **[!UICONTROL 流媒体]**：此组件启用Edge Network流媒体。 禁用此组件将禁用以下元素：
      * [发送媒体事件](action-types.md#send-media-event)操作类型

## 配置实例设置 {#general}

页面顶部的配置选项可告知Adobe Experience Platform将数据路由到何处以及要在服务器上使用的配置。

![在标记UI中显示Web SDK标记扩展的一般设置的图像](assets/web-sdk-ext-general.png)

* **[!UICONTROL 名称]**： Adobe Experience Platform Web SDK扩展支持页面上的多个实例。 该名称用于通过标记配置向多个组织发送数据。 实例名称默认为`alloy`。 但是，您可以将实例名称更改为任何有效的JavaScript对象名称。
* **[!UICONTROL IMS组织ID]**：您希望在Adobe上发送数据的组织的ID。 大多数情况下，使用自动填充的默认值。 当页面上有多个实例时，使用您要向其发送数据的第二个组织的值填充此字段。
* **[!UICONTROL Edge域]**：扩展发送和接收数据的域。 Adobe建议对此扩展使用第一方域(CNAME)。 默认的第三方域适用于开发环境，但不适合生产环境。[此处](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=zh-Hans)列出了有关如何设置第一方 CNAME 的说明。
* **[!UICONTROL Adobe Advertising]**：在选择`Advertising`组件时可用。 仅使用Adobe Advertising DSP的组织设置：
   * **[!UICONTROL Adobe Advertising DSP]**：启用显示到达跟踪。
   * **[!UICONTROL 广告商]**：启用[!UICONTROL Adobe Advertising DSP]时可用。 要为其启用显示到达跟踪的广告商。
   * **[!UICONTROL ID5合作伙伴ID]**：可选。 在启用[!UICONTROL Adobe Advertising DSP]时可用。 您组织的ID5合作伙伴ID。 此设置允许Web SDK收集ID5通用ID。
   * **[!UICONTROL RampID JavaScript路径]**：可选。 在启用[!UICONTROL Adobe Advertising DSP]时可用。 您组织的[!DNL LiveRamp RampID] JavaScript代码(`ats.js`)的路径。  此设置允许Web SDK收集[!DNL RampID]个通用ID。

## 配置数据流设置 {#datastreams}

此部分允许您为三个可用环境（生产、暂存和开发）中的每一个选择应使用的数据流。

当请求发送至Edge Network时，将使用数据流ID来引用服务器端配置。 您无需在网站上更改代码即可更新配置。

请参阅[数据流](../../../../datastreams/overview.md)指南，了解如何配置数据流。

您可以从可用下拉菜单中选择数据流，也可以选择&#x200B;**[!UICONTROL 输入值]**&#x200B;并为每个环境输入自定义数据流ID。

![在标记UI中显示Web SDK标记扩展的数据流设置的图像](assets/web-sdk-ext-datastreams.png)

## 配置隐私设置 {#privacy}

利用此部分，可配置Web SDK如何处理来自您网站的用户同意信号。 具体来说，它允许您选择在没有提供其他明确的同意首选项的情况下假定为用户的默认同意级别。

默认同意级别未保存到用户配置文件。

![在标记UI中显示Web SDK标记扩展的隐私设置的图像](assets/web-sdk-ext-privacy.png)

| [!UICONTROL 默认同意级别] | 描述 |
| --- | --- |
| [!UICONTROL 位于] | 收集在用户提供同意首选项之前发生的事件。 |
| [!UICONTROL 出] | 丢弃在用户提供同意首选项之前发生的事件。 |
| [!UICONTROL 挂起] | 在用户提供同意首选项之前发生的队列事件。 提供同意首选项时，将根据提供的首选项收集或丢弃事件。 |
| [!UICONTROL 由数据元素提供] | 默认同意级别由您定义的单独数据元素决定。 使用此选项时，必须使用提供的下拉菜单指定数据元素。 |

>[!TIP]
>
>如果您的业务操作需要明确的用户同意，请使用&#x200B;**[!UICONTROL Out]**&#x200B;或&#x200B;**[!UICONTROL Pending]**。

## 配置身份设置 {#identity}

利用此部分，可定义Web SDK在处理用户标识时的行为。

![在标记UI中显示Web SDK标记扩展的标识设置的图像](assets/web-sdk-ext-identity.png)

* **[!UICONTROL 从VisitorAPI迁移ECID]**：默认情况下启用此选项。 启用此功能后，SDK可以读取`AMCV`和`s_ecid` Cookie并设置`AMCV`使用的[!DNL Visitor.js] Cookie。 在迁移到Web SDK时，此功能很重要，因为某些页面可能仍在使用[!DNL Visitor.js]。 此选项允许SDK继续使用同一[!DNL ECID]，这样用户就不会被标识为两个不同的用户。
* **[!UICONTROL 使用第三方Cookie]**：启用此选项后，Web SDK会尝试将用户标识符存储在第三方Cookie中。 如果成功，则在用户跨多个域导航时将用户标识为单个用户，而不是在每个域上将用户标识为单独的用户。 如果启用了此选项，则如果SDK不支持第三方Cookie或用户将其配置为不允许第三方Cookie，则浏览器仍可能无法将用户标识符存储在第三方Cookie中。 在这种情况下，SDK只将标识符存储在第一方域中。

  >[!IMPORTANT]
  >&#x200B;>第三方Cookie与Web SDK中的[第一方设备ID](../../../../web-sdk/identity/first-party-device-ids.md)功能不兼容。
  >&#x200B;>您可以使用第一方设备ID，也可以使用第三方Cookie，但不能同时使用这两项功能。
  >

## 配置个性化设置 {#personalization}

利用此部分，可配置在加载个性化内容时如何隐藏页面的某些部分。 这可确保访客仅看到个性化页面。

![在标记UI中显示Web SDK标记扩展的个性化设置的图像](assets/web-sdk-ext-personalization.png)

* **[!UICONTROL 将Target从at.js迁移到Web SDK]**：使用此选项可允许[!DNL Web SDK]读取和写入at.js `mbox`或`mboxEdgeCluster`库使用的旧版`1.x`和`2.x` Cookie。 这有助于在从使用Web SDK的页面移动到使用at.js `1.x`或`2.x`库的页面时保留访客配置文件，反之亦然。

### 预隐藏样式 {#prehiding-style}

使用预隐藏样式编辑器，可定义自定义CSS规则以隐藏页面的特定部分。 加载页面时，Web SDK使用此样式来隐藏需要个性化的部分，检索个性化，然后取消隐藏个性化的页面部分。 这样，您的访客将看到已个性化的页面，而不看到个性化检索过程。

### 预隐藏代码片段 {#prehiding-snippet}

异步加载Web SDK库时，预隐藏代码片段很有用。 在这种情况下，为了避免闪烁，我们建议在加载Web SDK库之前隐藏内容。

要使用预隐藏代码片段，请将其复制并粘贴到页面的`<head>`元素中。

>[!IMPORTANT]
>
>使用预隐藏代码片段时，Adobe建议使用与[!DNL CSS]预隐藏样式[使用的规则相同的](#prehiding-style)规则。

## 配置数据收集设置 {#data-collection}

管理数据收集配置设置。 JavaScript库中的类似设置可以使用[`configure`](/help/web-sdk/commands/configure/overview.md)命令使用。

![在标记UI中显示Web SDK标记扩展的数据收集设置的图像。](assets/web-sdk-ext-collection.png)

* **[!UICONTROL 在事件发送回调之前]**：一个回调函数，用于评估和修改发送到Adobe的有效负载。 使用回调函数中的`content`变量修改有效负载。 此回调是相当于JavaScript库中[`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md)的标记。
* **[!UICONTROL 收集内部链接点击次数]**：用于收集网站或属性内部链接跟踪数据的复选框。 启用此复选框后，将显示事件分组选项：
   * **[!UICONTROL 无事件分组]**：链接跟踪数据在单独的事件中发送到Adobe。 在单独事件中发送链接点击次数可能会增加发送到Adobe Experience Platform的数据在合同中的使用量。
   * **[!UICONTROL 使用会话存储进行事件分组]**：将链接跟踪数据存储在会话存储中，直到发生下一页事件。 在以下页面上，存储的链接跟踪数据和页面查看数据将同时发送到Adobe。 Adobe建议在跟踪内部链接时启用此设置。
   * **[!UICONTROL 使用本地对象进行事件分组]**：将链接跟踪数据存储在本地对象中，直到发生下一页事件。 如果访客导航到新页面，则链接跟踪数据将丢失。 此设置在单页应用程序的上下文中最为有用。

  当您选择使用会话存储或本地对象进行事件分组，并且要向Real-Time CDP、Customer Journey Analytics、Adobe Journey Optimizer或Mix Modeler发送数据时，必须更新标记规则。 在将数据发送到Adobe之前，请确保每个页面查看事件都明确将页面名称（作为字符串）和页面查看值（作为整数，通常为1）映射到XDM对象。

  如果您将数据发送到Adobe Analytics，则这些值会自动包含在内，而无需进行其他配置。

* **[!UICONTROL 收集外部链接点击次数]**：启用外部链接收集的复选框。
* **[!UICONTROL 收集下载链接点击次数]**：用于收集下载链接的复选框。
* **[!UICONTROL 下载链接限定符]**：将链接URL限定为下载链接的正则表达式。
* **[!UICONTROL 筛选点击属性]**：一个回调函数，用于在集合之前评估和修改与点击相关的属性。 此函数在事件发送回调[!UICONTROL 之前的]On之前运行。
* **上下文设置**：自动收集访客信息，这些信息会为您填充特定的XDM字段。 您可以选择&#x200B;**[!UICONTROL 所有默认上下文信息]**&#x200B;或&#x200B;**[!UICONTROL 特定上下文信息]**。 该标记等同于JavaScript库中的[`context`](/help/web-sdk/commands/configure/context.md)。
   * **[!UICONTROL Web]**：收集有关当前页面的信息。
   * **[!UICONTROL 设备]**：收集有关用户设备的信息。
   * **[!UICONTROL 环境]**：收集有关用户浏览器的信息。
   * **[!UICONTROL 放置上下文]**：收集有关用户位置的信息。
   * **[!UICONTROL 高熵用户代理提示]**：收集有关用户设备的更多详细信息。

>[!TIP]
>
>**[!UICONTROL On before link click send]**&#x200B;字段是一个已弃用的回调，仅对已配置该回调的属性可见。 该标记等同于JavaScript库中的[`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md)。 使用&#x200B;**[!UICONTROL 筛选点击属性]**&#x200B;回调筛选或调整点击数据，或者使用&#x200B;**[!UICONTROL 在事件发送回调前开启]**&#x200B;筛选或调整发送到Adobe的整体有效负载。 如果同时设置了&#x200B;**[!UICONTROL 筛选条件点击属性]**&#x200B;回调和&#x200B;**[!UICONTROL 在链接点击之前打开]**&#x200B;回调，则只有&#x200B;**[!UICONTROL 筛选条件点击属性]**&#x200B;回调运行。

## 配置媒体收集设置 {#media-collection}

媒体收集功能可帮助您收集与网站上的媒体会话相关的数据。

收集的数据可以包括有关媒体回放、暂停、完成和其他相关事件的信息。 收集之后，您可以将此数据发送到Adobe Experience Platform和/或Adobe Analytics以生成报表。 此功能为跟踪和了解您网站上的媒体消费行为提供了全面的解决方案。

![在标记UI中显示Web SDK标记扩展的媒体收集设置的图像](assets/media-collection.png)


* **[!UICONTROL 频道]**：发生媒体收集的频道名称。 示例：`Video channel`。
* **[!UICONTROL 播放器名称]**：媒体播放器的名称。
* **[!UICONTROL 应用程序版本]**：媒体播放器应用程序的版本。
* **[!UICONTROL 主ping间隔]**：主内容ping的频率（以秒为单位）。 默认值为 `10`。值可以介于`10`到`50`秒之间。  如果未指定值，则在使用[自动跟踪的会话](../../../../web-sdk/commands/createmediasession.md#automatic)时使用默认值。
* **[!UICONTROL 广告Ping间隔]**：广告内容的Ping频率（以秒为单位）。 默认值为 `10`。值可以介于`1`到`10`秒之间。 如果未指定值，则在使用[自动跟踪的会话](../../../../web-sdk/commands/createmediasession.md#automatic)时使用默认值

## 配置数据流覆盖 {#datastream-overrides}

数据流覆盖允许您为数据流定义其他配置，这些配置通过 Web SDK 传递到 Edge Network。

这可以帮助您触发与默认数据流行为不同的数据流行为，而无需创建新的数据流或修改现有设置。

数据流配置覆盖是一个两步过程：

1. 首先，您必须在[数据流配置页面](/help/datastreams/configure.md)中定义数据流配置覆盖。
2. 然后，您必须通过Web SDK命令或使用Web SDK标记扩展将覆盖发送到Edge Network。

有关如何覆盖数据流配置的详细说明，请参阅数据流[配置覆盖文档](/help/datastreams/overrides.md)。

作为通过Web SDK命令传递覆盖的替代方法，您可以在下面显示的标记扩展屏幕中配置覆盖。

>[!IMPORTANT]
>
> 必须为每个环境配置数据流覆盖。 开发、暂存和生产环境都具有单独的覆盖。 您可以使用以下屏幕中显示的专用选项复制它们之间的设置。

![显示使用Web SDK标记扩展页的数据流配置覆盖的图像。](assets/datastream-overrides.png)

默认情况下，数据流配置覆盖处于禁用状态。 默认情况下已选择&#x200B;**[!UICONTROL 匹配数据流配置]**&#x200B;选项。

![显示数据流配置的Web SDK标记扩展用户界面将覆盖默认设置。](assets/datastream-override-default.png)

要在标记扩展中启用数据流覆盖，请从下拉菜单中选择&#x200B;**[!UICONTROL 已启用]**。

![Web SDK标记扩展用户界面显示数据流配置覆盖“已启用”设置。](assets/datastream-override-enabled.png)

启用数据流配置覆盖后，可以为下述每项服务配置覆盖。

以下数据流覆盖设置将覆盖所选环境的任何服务器端数据流配置和规则。

### Adobe Analytics {#analytics}

使用此部分中的设置可覆盖到Adobe Analytics服务的数据路由。

![显示Adobe Analytics数据流覆盖设置的Web SDK标记扩展UI图像。](assets/datastream-override-analytics.png)

* **[!UICONTROL 已启用]** / **[!UICONTROL 已禁用]**：使用此下拉菜单启用或禁用到Adobe Analytics服务的数据路由。
* **[!UICONTROL 报表包]**： Adobe Analytics中目标报表包的ID。 该值必须是来自您的数据流配置的预配置覆盖报表包（或以逗号分隔的报表包列表）。 此设置将覆盖主报表包。
* **[!UICONTROL 添加报表包]**：选择此选项可添加其他报表包。

### Adobe Audience Manager {#audience-manager}

使用此部分中的设置可覆盖到Adobe Audience Manager服务的数据路由。

![显示Adobe Audience Manager数据流覆盖设置的Web SDK标记扩展UI图像。](assets/datastream-override-audience-manager.png)

* **[!UICONTROL 已启用]** / **[!UICONTROL 已禁用]**：使用此下拉菜单启用或禁用到Adobe Audience Manager服务的数据路由。
* **[!UICONTROL 第三方ID同步容器]**： Audience Manager中目标第三方ID同步容器的ID。 该值必须是来自数据流配置的预配置辅助容器，并覆盖主容器。

### Adobe Experience Platform {#experience-platform}

使用此部分中的设置可覆盖到Adobe Experience Platform服务的数据路由。

![显示Adobe Experience Platform数据流覆盖设置的Web SDK标记扩展UI图像。](assets/datastream-override-experience-platform.png)

* **[!UICONTROL 已启用]** / **[!UICONTROL 已禁用]**：使用此下拉菜单启用或禁用到Adobe Experience Platform服务的数据路由。
* **[!UICONTROL 事件数据集]**： Adobe Experience Platform中目标事件数据集的ID。 该值必须是来自数据流配置的预配置辅助数据集。
* **[!UICONTROL Offer Decisioning]**：使用此下拉菜单启用或禁用到[!DNL Offer Decisioning]服务的数据路由。
* **[!UICONTROL Edge分段]**：使用此下拉菜单启用或禁用到[!DNL Edge Segmentation]服务的数据路由。
* **[!UICONTROL Personalization目标]**：使用此下拉菜单启用或禁用到个性化目标的数据路由。
* **[!UICONTROL Adobe Journey Optimizer]**：使用此下拉菜单启用或禁用到[!DNL Adobe Journey Optimizer]服务的数据路由。

### Adobe服务器端事件转发 {#ssf}

使用此部分中的设置可覆盖发送到Adobe服务器端事件转发服务的数据路由。

![Web SDK标记扩展UI图像显示Adobe服务器端事件转发数据流覆盖设置。](assets/datastream-override-ssf.png)

* **[!UICONTROL 已启用]** / **[!UICONTROL 已禁用]**：使用此下拉菜单启用或禁用到Adobe服务器端事件转发服务的数据路由。

### Adobe Target {#target}

使用此部分中的设置可覆盖到Adobe Target服务的数据路由。

![显示Adobe Target数据流覆盖设置的Web SDK标记扩展UI图像。](assets/datastream-override-target.png)

* **[!UICONTROL 已启用]** / **[!UICONTROL 已禁用]**：使用此下拉菜单启用或禁用到Adobe Target服务的数据路由。

## 配置高级设置

如果需要更改用于与Edge交互的基本路径，请使用&#x200B;**[!UICONTROL Edge Network基本路径]**&#x200B;字段。 这不需要更新，但是如果您参与Beta或Alpha测试，Adobe可能会要求您更改此字段。

![显示使用Web SDK标记扩展页的高级设置的图像。](assets/advanced-settings.png)

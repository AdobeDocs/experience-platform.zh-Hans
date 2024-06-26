---
title: 配置Web SDK标记扩展
description: 了解如何在标记UI中配置Experience PlatformWeb SDK标记扩展。
exl-id: 22425daa-10bd-4f06-92de-dff9f48ef16e
source-git-commit: 1d1bb754769defd122faaa2160e06671bf02c974
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 6%

---

# 配置Web SDK标记扩展

此 [!DNL Web SDK] 标记扩展会通过Experience PlatformEdge Network从Web资产向Adobe Experience Cloud发送数据。

该扩展允许您将数据流式传输到Platform、同步身份、处理客户同意信号并自动收集上下文数据。

本文档介绍如何在标记UI中配置标记扩展。

## 安装Web SDK标记扩展 {#install}

Web SDK标记扩展需要在上安装资产。 如果您尚未这样做，请参阅相关的文档 [创建标记属性](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html).

创建资产后，打开该资产并选择 **[!UICONTROL 扩展]** 选项卡。

选择 **[!UICONTROL 目录]** 选项卡。 从可用扩展列表中，找到 [!DNL Web SDK] 扩展并选择 **[!UICONTROL 安装]**.

![显示选中了Web SDK扩展的标记UI的图像](assets/web-sdk-install.png)

选择后 **[!UICONTROL 安装]**&#x200B;中，您必须配置Web SDK标记扩展并保存配置。

>[!NOTE]
>
>标记扩展仅在保存配置后进行安装。 请参阅以下部分，了解如何配置标记扩展。

## 配置实例设置 {#general}

页面顶部的配置选项可告知Adobe Experience Platform将数据路由到何处以及要在服务器上使用的配置。

![该图像显示了标记UI中Web SDK标记扩展的常规设置](assets/web-sdk-ext-general.png)

* **[!UICONTROL 名称]**：Adobe Experience Platform Web SDK扩展支持页面上的多个实例。 该名称用于通过标记配置向多个组织发送数据。 实例名称默认为 `alloy`. 但是，您可以将实例名称更改为任何有效的JavaScript对象名称。
* **[!UICONTROL IMS组织ID]**：您希望在Adobe时向其发送数据的组织的ID。 大多数情况下，使用自动填充的默认值。 当页面上有多个实例时，使用您要向其发送数据的第二个组织的值填充此字段。
* **[!UICONTROL 边缘域]**：扩展发送和接收数据的域。 Adobe建议对此扩展使用第一方域(CNAME)。 默认的第三方域适用于开发环境，但不适合生产环境。[此处](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=zh-Hans)列出了有关如何设置第一方 CNAME 的说明。

## 配置数据流设置 {#datastreams}

此部分允许您为三个可用环境（生产、暂存和开发）中的每一个选择应使用的数据流。

向Edge Network发送请求时，将使用数据流ID来引用服务器端配置。 您无需在网站上更改代码即可更新配置。

请参阅指南，网址为 [数据流](../../../../datastreams/overview.md) 了解如何配置数据流。

您可以从可用下拉菜单中选择数据流，也可以选择 **[!UICONTROL 输入值]** 并输入每个环境的自定义数据流ID。

![该图像显示了标记UI中Web SDK标记扩展的数据流设置](assets/web-sdk-ext-datastreams.png)

## 配置隐私设置 {#privacy}

在此部分中，您可以配置Web SDK如何处理来自您网站的用户同意信号。 具体来说，它允许您选择在没有提供其他明确的同意首选项的情况下假定为用户的默认同意级别。

默认同意级别未保存到用户配置文件。

![此图像显示了标记UI中Web SDK标记扩展的隐私设置](assets/web-sdk-ext-privacy.png)

| [!UICONTROL 默认同意级别] | 描述 |
| --- | --- |
| [!UICONTROL 在] | 收集在用户提供同意首选项之前发生的事件。 |
| [!UICONTROL 去话] | 丢弃在用户提供同意首选项之前发生的事件。 |
| [!UICONTROL 待处理] | 在用户提供同意首选项之前发生的队列事件。 提供同意首选项时，将根据提供的首选项收集或丢弃事件。 |
| [!UICONTROL 由数据元素提供] | 默认同意级别由您定义的单独数据元素决定。 使用此选项时，必须使用提供的下拉菜单指定数据元素。 |

>[!TIP]
>
>使用 **[!UICONTROL 去话]** 或 **[!UICONTROL 待处理]** 如果您的业务运营需要明确的用户同意。

## 配置身份设置 {#identity}

利用此部分，可定义Web SDK在处理用户标识时的行为。

![此图像显示了标记UI中Web SDK标记扩展的身份设置](assets/web-sdk-ext-identity.png)

* **[!UICONTROL 从VisitorAPI迁移ECID]**：默认启用此选项。 启用此功能后，SDK可以 `AMCV` 和 `s_ecid` Cookie并设置 `AMCV` 使用的Cookie [!DNL Visitor.js]. 在迁移到Web SDK时，此功能很重要，因为某些页面可能仍在使用 [!DNL Visitor.js]. 此选项允许SDK继续使用相同的 [!DNL ECID] 这样就不会将用户标识为两个单独的用户。
* **[!UICONTROL 使用第三方Cookie]**：启用此选项后，Web SDK会尝试将用户标识符存储在第三方Cookie中。 如果成功，则在用户跨多个域导航时将用户标识为单个用户，而不是在每个域上将用户标识为单独的用户。 如果启用此选项，则当浏览器不支持第三方Cookie或用户已配置为不允许第三方Cookie时，SDK仍可能无法将用户标识符存储在第三方Cookie中。 在这种情况下，SDK仅将标识符存储在第一方域中。

  >[!IMPORTANT]
  >>第三方Cookie与 [第一方设备Id](../../../../web-sdk/identity/first-party-device-ids.md) Web SDK中的功能。
您可以使用第一方设备ID，也可以使用第三方Cookie，但不能同时使用这两项功能。
  >
## 配置个性化设置 {#personalization}

利用此部分，可配置在加载个性化内容时如何隐藏页面的某些部分。 这可确保访客仅看到个性化页面。

![该图像显示了标记UI中Web SDK标记扩展的个性化设置](assets/web-sdk-ext-personalization.png)

* **[!UICONTROL 将Target从at.js迁移到Web SDK]**：使用此选项可启用 [!DNL Web SDK] 读写旧版 `mbox` 和 `mboxEdgeCluster` at.js使用的Cookie `1.x` 或 `2.x` 库。 这有助于您在从使用Web SDK的页面移动到使用at.js的页面时保留访客配置文件 `1.x` 或 `2.x` 库或反之。

### 预隐藏样式 {#prehiding-style}

使用预隐藏样式编辑器，可定义自定义CSS规则以隐藏页面的特定部分。 在加载页面时，Web SDK使用此样式来隐藏需要个性化的部分，检索个性化，然后取消隐藏个性化的页面部分。 这样，您的访客将看到已个性化的页面，而不看到个性化检索过程。

### 预隐藏代码片段 {#prehiding-snippet}

异步加载Web SDK库时，预隐藏代码片段很有用。 在这种情况下，为了避免闪烁，我们建议在加载Web SDK库之前隐藏内容。

要使用预隐藏代码片段，请将其复制并粘贴到 `<head>` 元素。

>[!IMPORTANT]
>
在使用预隐藏代码片段时，Adobe建议使用相同的 [!DNL CSS] 规则作为 [预隐藏样式](#prehiding-style).

## 配置数据收集设置 {#data-collection}

![该图像显示了标记UI中Web SDK标记扩展的数据收集设置](assets/web-sdk-ext-collection.png)

* **[!UICONTROL 回调函数]**：扩展中提供的回调函数也称为 [`onBeforeEventSend` 函数](/help/web-sdk/commands/configure/onbeforeeventsend.md) 在图书馆里。 此函数允许您在将事件发送到Edge Network之前对其进行全局修改。
* **[!UICONTROL 启用点击数据收集]**：Web SDK可以自动为您收集链接点击信息。 默认情况下，此功能处于启用状态，但使用此选项可禁用该功能。 如果链接包含中列出的下载表达式之一，则也会将其标记为下载链接 [!UICONTROL 下载链接限定符] 文本框。 Adobe为您提供一些默认的下载链接限定符。 您可以根据需要编辑它们。
* **[!UICONTROL 自动收集的上下文数据]**：默认情况下，Web SDK会收集有关设备、Web、环境和位置上下文的特定上下文数据。 如果不希望收集此数据，或只希望收集某些类别的数据，请选择 **[!UICONTROL 特定上下文信息]** 并选择要收集的数据。 请参阅 [`context`](/help/web-sdk/commands/configure/context.md) 以了解更多信息。

## 配置媒体收集设置 {#media-collection}

媒体收集功能可帮助您收集与网站上的媒体会话相关的数据。

收集的数据可以包括有关媒体回放、暂停、完成和其他相关事件的信息。 收集之后，您可以将此数据发送到Adobe Experience Platform和/或Adobe Analytics以生成报表。 此功能为跟踪和了解您网站上的媒体消费行为提供了全面的解决方案。

![此图像显示了标记UI中Web SDK标记扩展的媒体收集设置](assets/media-collection.png)


* **[!UICONTROL 渠道]**：发生媒体收集的渠道的名称。 示例：`Video channel`。
* **[!UICONTROL 播放器名称]**：媒体播放器的名称。
* **[!UICONTROL 应用程序版本]**：媒体播放器应用程序的版本。
* **[!UICONTROL 主ping间隔]**：主内容Ping的频率（以秒为单位）。 默认值为 `10`。值可以介于 `10` 到 `50` 秒。  如果未指定值，则在使用 [自动跟踪的会话](../../../../web-sdk/commands/createmediasession.md#automatic).
* **[!UICONTROL 广告Ping间隔]**：广告内容的Ping频率（以秒为单位）。 默认值为 `10`。值可以介于 `1` 到 `10` 秒。 如果未指定值，则在使用 [自动跟踪的会话](../../../../web-sdk/commands/createmediasession.md#automatic)

## 配置数据流覆盖 {#datastream-overrides}

数据流覆盖允许您为数据流定义其他配置，这些配置通过 Web SDK 传递到 Edge Network。

这可以帮助您触发与默认数据流行为不同的数据流行为，而无需创建新的数据流或修改现有设置。

数据流配置覆盖是一个两步过程：

1. 首先，您必须在[数据流配置页面](/help/datastreams/configure.md)中定义数据流配置覆盖。
2. 然后，您必须通过Web SDK命令或Web SDK标记扩展将覆盖发送到Edge Network。

查看数据流 [配置覆盖文档](/help/datastreams/overrides.md) 以获取有关如何覆盖数据流配置的详细说明。

作为通过Web SDK命令传递覆盖的替代方法，您可以在下面显示的标记扩展屏幕中配置覆盖。

>[!IMPORTANT]
>
必须为每个环境配置数据流覆盖。 开发、暂存和生产环境都具有单独的覆盖。 您可以使用以下屏幕中显示的专用选项复制它们之间的设置。

![此图像显示了使用Web SDK标记扩展页面进行数据流配置覆盖。](assets/datastream-overrides.png)

## 配置高级设置

使用 **[!UICONTROL 边缘基本路径]** Edge Network字段。 这不需要更新，但是如果您参与Beta或Alpha测试，Adobe可能会要求您更改此字段。

![此图像显示了使用Web SDK标记扩展页面的高级设置。](assets/advanced-settings.png)

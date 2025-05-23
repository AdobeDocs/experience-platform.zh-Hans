---
title: Adobe-Managed主机概述
description: 了解用于在Adobe Experience Platform中部署标记库内部版本的默认托管选项。
exl-id: 9042c313-b0d3-4f6e-963d-0051d760fd16
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 55%

---

# Adobe-managed 主机概述

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../../term-updates.md)。

Adobe-managed主机是您在Adobe Experience Platform中部署标记库内部版本时默认的主机设置。 当您通过数据收集用户界面创建新资产时，您会获得一个默认的Adobe-managed主机。

凭借 Adobe-managed 主机，可将库版本交付至已与 Adobe 签约的第三方内容分发网络 (CDN)。由于这些CDN独立于Adobe运行，因此即使Experience Platform正在进行维护或由于其他原因而停止运行，您的部署代码仍可以在站点和应用程序中继续正常运转。 Adobe-managed 主机的嵌入代码引用了 CDN 上的主要库文件，因此客户端设备可在运行时检索文件。

本文档概述了Experience Platform中的Adobe-managed主机，并提供了有关如何在UI中创建新的Adobe-managed主机的步骤。

## Akamai

目前，[Akamai](https://www.akamai.com/cn/zh/) 是 Adobe 的主要 CDN 提供商。Akamai 构建的可靠 CDN 旨在为全球大容量 Web 访客受众提供内容。CDN 运行的冗余网络由负载均衡、地理优化的节点构成，可以尽快为遍布全球的访客提供内容。

具体而言，Akamai 在 87 个国家/地区运行着 137,000 多台服务器，涉及超过 1,150 个网络。在冗余方面，CDN不仅可以从一台服务器路由到另一台服务器，还可以根据需要从一个服务器节点路由到另一个服务器节点。 换句话说，每个节点都由多台服务器组成，因此一台服务器的停机绝不会导致问题，因为同一节点上的其他服务器可以接管这台停机的服务器。

如果整个节点陷入瘫痪，Akamai会从具有相同缓存内容的下一个最接近节点提供内容。 节点是根据访客位置、流量负载和其他因素动态选取的，因此，始终能够通过最适合每个访客的当地节点提供内容。

托管在 Akamai 上的文件将使用域 `assets.adobedtm.com`。判断能否安全引用域（`http://` 或 `https://`）时，取决于您在嵌入代码 `<script>` 中调用上述域的方式。

>[!WARNING]
>
>如果您没有将库托管在Akamai网络上，那么Experience Platform则无法阻止因此而引发的任何错误。

## 库版本缓存

使用 Adobe-managed 主机时，您的库版本会缓存到以下两个位置：

* [Edge缓存](#edge)
* [浏览器缓存](#browser)

### Edge缓存 {#edge}

CDN的主要用途是智能地将内容分发到地理位置更接近于最终用户的服务器，以便客户端设备可以更快地检索内容。 CDN 通过以下方法来实现上述目标：生成的内容副本适用于遍布在世界各地的服务器（“边缘节点”）。

当您的库版本部署到 Adobe-managed 主机后，CDN 会把该版本分发到多台中央服务器（“原点”），这些服务器随后会将库版本的副本发送至全球大量不同的边缘节点，以此来进行缓存。最终，客户端设备会获得存储在这些边缘节点上的库缓存版本。

![](../images/cdn-diagram.png)

>[!NOTE]
>
>对于 Adobe-managed 主机而言，发布到任何新环境的首个库，最多可能需要五分钟即可传送到遍布全球的 CDN。

当边缘节点收到针对特定文件（如库内部版本）的请求时，该节点会首先检查文件的过期时间。 如果时间未过期，边缘节点将提供缓存的版本。 如果时间已过期，边缘节点则会请求最近的源提供新副本，然后根据新的过期时间缓存刷新后的副本。

>[!NOTE]
>
>除边缘节点缓存之外，还可能存在执行自身缓存的中间网络（例如，公司网络或移动网络）。如果您的版本未按预期进行缓存，根本原因可能在于这些中间网络。

#### Edge缓存失效 {#invalidation}

当您上传新的库内部版本时，所有适用边缘节点上的缓存都将失效。 这意味着每个节点都认为其缓存的版本无效，无论其检索最新副本的时间有多近。 在某个边缘节点下次收到针对该文件的请求时，这个节点会再次从原点检索新副本。

由于Akamai具有多个源服务器，这些服务器会在它们之间复制文件，并且由于无法知道哪个源首先收到您的文件，因此这些节点请求可能会命中一个没有最新版本的原点。 然后，它会再次缓存较旧的版本。 为防止出现上述情况，会按照以下时间间隔，对每个新版本执行多个缓存失效设置：

* 上传后立即执行
* 上传 5 分钟后执行
* 上传 60 分钟后执行

这些交错的缓存失效设置为原点服务器组提供了相互复制文件最新版本的时间，以便都能检索到最新版本的文件。

### 浏览器缓存 {#browser}

除此之外，还可以通过使用 `cache-control` HTTP 标头，在浏览器上缓存库版本。使用 Adobe-managed 主机时，由于无法控制 API 响应中返回的标头，因此采用了 Adobe 默认缓存设置。换句话说，您无法对 Adobe-managed 主机使用自定义标头。如果要自定义 `cache-control` 标头，则需要考虑选用[自托管](self-hosting-libraries.md)的方法来代替。

浏览器缓存的库内部版本的过期时间（由`cache-control`标头决定）将因您使用的标记环境而异：

| 环境 | `cache-control` 值 |
| --- | --- |
| 开发 | `max-age=0, no-cache, no-store` |
| 暂存 | `max-age=0, no-cache, no-store` |
| 生产 | `max-age=3600` |

如上表所示，开发环境和暂存环境不支持浏览器缓存。因此，您不应在高流量或生产环境中使用开发或暂存嵌入代码。

缓存控制标头仅应用于主库内部版本。 主库下的所有子资源始终被视为新资源，因此无需在浏览器中缓存它们。

## 在UI中使用Adobe管理的主机

首次在Experience Platform UI或数据收集UI中创建属性时，将自动为您创建Adobe-managed主机。 默认情况下，具有立即可用属性的所有可用环境也会分配给Adobe-managed主机。

>[!NOTE]
>
>如果默认的 Adobe-managed 主机未从所有环境中分配，则可以删除该主机。如果要在执行此操作后切换回 Adobe-managed 主机，可通过以下步骤创建新主机：
>
>1. 选择属性上的&#x200B;**[!UICONTROL 主机]**&#x200B;选项卡，然后选择&#x200B;**[!UICONTROL 添加主机]**。
>1. 提供主机的名称，选择&#x200B;**[!UICONTROL 由Adobe管理]**&#x200B;作为主机类型，然后选择&#x200B;**[!UICONTROL 保存]**。
>
>接下来，您可以根据需要将环境重新分配给 Adobe-managed 主机。

## 后续步骤

本文档概述了Adobe Experience Platform中由Adobe管理的标记库托管。 有关其他托管选项的信息，请参阅以下文档：

* [SFTP托管](./sftp-host.md)
* [自托管库](./self-hosting-libraries.md)

有关如何管理环境中的主机的详细信息，请参阅[环境指南](../environments.md)。

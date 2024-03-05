---
keywords: Experience Platform；主页；热门主题；数据收集；Launch；Web SDK
solution: Experience Platform
title: 数据收集概述
description: 了解在Adobe Experience Platform中收集客户体验数据涉及的各种技术。
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 6%

---

# 数据收集概述

Adobe Experience Platform提供了一套方法，可让您从客户端源收集客户体验数据，并将该数据发送到Adobe Experience Platform Edge Network，可在其中丰富和转换数据，并在几秒钟内将数据分发到Adobe或非Adobe目标。

以下客户端源支持数据收集：

* 基于Web的应用
* 本机移动设备应用程序
* 过顶(OTT)应用程序

数据收集侧重于摄取的数据集的可发现性和可访问性，包括以下内容：

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [标记](../tags/home.md)
* [数据流](../datastreams/overview.md)
* [事件转发](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../web-sdk/home.md)
* [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)
* [边缘网络服务器 API](../server-api/overview.md)
* [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [Experience Platform保证](../assurance/home.md)


本指南简要介绍如何收集数据，以及如何通过Platform Edge Network将数据发送到Adobe Experience Cloud产品和非Adobe应用程序。

## 标记、Web SDK和移动SDK

Platform Web SDK和Platform Mobile SDK可分别折叠所有Adobe产品库并将其压缩为用于Web和移动平台的单个开发工具包。 可以使用原始代码或使用以下代码实现这些目标： [标记](../tags/home.md) 通过数据收集UI或Adobe Experience Platform UI。

压缩这些库可加快数据收集速度，并将从客户端设备到Platform Edge Network的操作整合到单个流中。

![标记、Web SDK、移动SDK](./images/home/tags-sdks.png)

## Platform边缘网络和数据流 {#edge}

Platform Edge Network是一个全球分布式、快速可靠的服务器网络，能够接收和处理超大规模的数据。 使用标记，您可以设置 [数据流](../datastreams/overview.md) Adobe Target、Adobe Audience Manager和Adobe Analytics等产品，这些产品允许您在不更改客户端代码的情况下在服务器端激活这些产品。

此外，数据流与多种平台功能集成，有助于确保您发送的任何敏感数据都能在组织政策和法律法规方面得到适当处理。 请参阅以下部分 [处理敏感数据](../datastreams/overview.md#sensitive) 数据流文档以了解更多信息。

![数据流和Adobe解决方案](./images/home/adobe-solutions.png)

>[!NOTE]
>
>有关Platform Edge Network的概要介绍，请参阅以下内容 [交互式产品导览](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## 事件转发

[事件转发](../tags/ui/event-forwarding/overview.md) 可挖掘到任何Experience Platform数据流，从而允许您转换、扩充数据并以极低的延迟将数据发送到任何非Adobe目标，而无需向客户端设备添加任何第三方代码。

![事件转发](./images/home/event-forwarding.png)

>[!NOTE]
>
>事件转发是一项付费功能，包含在Adobe Real-time Customer Data Platform Connections、Prime或Ultimate产品中。

## 后续步骤

本文档全面概述了数据收集如何自动将收集的客户体验数据发送到Adobe产品和第三方目标。

![数据收集框架](./images/home/collection.png)

有关通过Edge Network发送事件数据所涉及的常规工作流的更多信息，请参阅 [端到端概述](./e2e.md).

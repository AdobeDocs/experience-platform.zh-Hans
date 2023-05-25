---
keywords: Experience Platform；主页；热门主题；数据收集；Launch；Web SDK
solution: Experience Platform
title: 数据收集概述
description: 了解在Adobe Experience Platform中收集客户体验数据涉及的各种技术。
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 13c02dd5930905e3851ff147c0ea4d914e3dc6c7
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 7%

---

# 数据收集概述

Adobe Experience Platform提供了一套技术，可让您从客户端源收集客户体验数据，并将其发送到Adobe Experience Platform Edge Network，可在其中丰富和转换数据，并在几秒钟内将数据分发到Adobe或非Adobe目标。

以下客户端源支持数据收集：

* 基于Web的应用
* 本机移动应用程序
* 过顶(OTT)应用程序

数据收集侧重于摄取的数据集的可发现性和可访问性，包括以下内容：

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [标记](../tags/home.md)
* [数据流](../edge/datastreams/overview.md)
* [事件转发](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../edge/home.md)
* [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/)
* [Adobe Experience Platform调试器](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob?hl=en)
* [体验数据模型(XDM)](../xdm/home.md)
* [Adobe Experience Platform Identity Service](../identity-service/home.md)

本指南简要介绍数据收集以及它如何通过Platform Edge Network向Adobe Experience Cloud产品和非Adobe应用程序发送数据。

## 标记、Web SDK和Mobile SDK

Platform Web SDK和Platform Mobile SDK分别压缩所有Adobe产品库，并将其压缩为用于Web和移动平台的单个开发工具包。 可以使用原始代码或通过使用以下方式实现这些目标 [标记](../tags/home.md) 通过数据收集UI或Adobe Experience Platform UI。

压缩这些库可加快数据收集速度，并将从客户端设备到Platform Edge Network的操作整合到单个流中。

![标记、Web SDK、Mobile SDK](./images/home/tags-sdks.png)

## Platform Edge Network和数据流 {#edge}

Platform Edge Network是一个全球分布式、快速且可靠的服务器网络，能够接收和处理超大规模的数据。 使用标记，您可以设置 [数据流](../edge/datastreams/overview.md) 适用于Adobe Target、Adobe Audience Manager和Adobe Analytics等产品，通过这些产品，您可以在服务器端激活这些产品，而无需更改客户端代码。

此外，数据流与多项平台功能集成，有助于确保您发送的任何敏感数据都得到符合组织政策和法规的适当处理。 请参阅以下部分： [处理敏感数据](../edge/datastreams/overview.md#sensitive) 有关更多信息，请参阅数据流文档。

![数据流和Adobe解决方案](./images/home/adobe-solutions.png)

>[!NOTE]
>
>有关Platform Edge Network的概要介绍，请参阅以下内容 [交互式产品导览](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1).

## 事件转发

[事件转发](../tags/ui/event-forwarding/overview.md) 可以进入任何Experience Platform数据流，允许您转换、扩充数据并以极低的延迟将数据发送到任何非Adobe目标，而且无需向客户端设备添加任何第三方代码。

![事件转发](./images/home/event-forwarding.png)

>[!NOTE]
>
>事件转发是一项付费功能，包含在Adobe Real-time Customer Data Platform Connections、Prime或Ultimate产品中。

## 后续步骤

本文档概要介绍了数据收集如何工作以自动化将收集的客户体验数据发送到Adobe产品和第三方目标的过程。

![数据收集框架](./images/home/collection.png)

有关通过Edge Network发送事件数据的一般工作流的详细信息，请参阅 [端到端概述](./e2e.md).

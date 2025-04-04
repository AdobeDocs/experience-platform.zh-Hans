---
keywords: Experience Platform；主页；热门主题；数据收集；Launch；Web SDK
solution: Experience Platform
title: 数据收集概述
description: 了解在Adobe Experience Platform中收集客户体验数据涉及的各种技术。
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 4%

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
* [Experience Platform Assurance](../assurance/home.md)


本指南简要介绍数据收集以及它如何通过Experience Platform Edge Network将数据发送到Adobe Experience Cloud产品和非Adobe应用程序。

## 标记、Web SDK和Mobile SDK

Experience Platform Web SDK和Experience Platform Mobile SDK可折叠所有Adobe产品库，并将其分别压缩为适用于Web平台和移动平台的单个开发工具包。 可以使用原始代码或通过数据收集UI或Adobe Experience Platform UI使用[标记](../tags/home.md)实现这些目标。

压缩这些库可加快数据收集速度，并将从客户端设备到Experience Platform Edge Network的操作整合到单个流中。

![标记， Web SDK， Mobile SDK](./images/home/tags-sdks.png)

## Experience Platform Edge Network和数据流 {#edge}

Experience Platform Edge Network是一个全球分布式、快速且可靠的服务器网络，能够大规模接收和处理数据。 使用标记，您可以为Adobe Target、Adobe Audience Manager和Adobe Analytics等产品设置[数据流](../datastreams/overview.md)，这样您就可以在服务器端激活这些产品，而无需更改客户端代码。

此外，数据流与多项Experience Platform功能集成，这有助于确保您发送的任何敏感数据都能在组织政策和法律法规方面得到适当处理。 有关详细信息，请参阅数据流文档中有关[处理敏感数据](../datastreams/overview.md#sensitive)的部分。

![数据流和Adobe解决方案](./images/home/adobe-solutions.png)

## 事件转发

[事件转发](../tags/ui/event-forwarding/overview.md)可以进入任何Experience Platform数据流，从而允许您转换、扩充数据并以极低的延迟将数据发送到任何非Adobe目标，而无需向客户端设备添加任何第三方代码。

![事件转发](./images/home/event-forwarding.png)

>[!NOTE]
>
>事件转发是一项付费功能，包含在Adobe Real-Time Customer Data Platform连接、Prime或Ultimate产品中。

## 后续步骤

本文档全面概述了数据收集如何自动将收集的客户体验数据发送到Adobe产品和第三方目标。

![数据收集框架](./images/home/collection.png)

有关通过Edge Network发送事件数据时涉及的常规工作流的详细信息，请参阅[端到端概述](./e2e.md)。

---
keywords: Experience Platform；主页；热门主题；数据收集；启动；Web SDK
solution: Experience Platform
title: 数据收集概述
topic-legacy: overview
description: 了解与收集Adobe Experience Platform中客户体验数据相关的各种技术。
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: f61a845b915df3d803085fbf528e014c8acd9dbd
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 2%

---

# 数据收集概述

Adobe Experience Platform提供了一套技术，允许您从客户端源收集客户体验数据，并将其发送到Adobe Experience Platform边缘网络，在该网络中，可以在几秒内对数据进行扩充、转换并分发到Adobe或非Adobe目标。

以下客户端源支持数据收集：

* 基于Web的应用程序
* 本机移动设备应用程序
* 过顶(OTT)应用程序

Experience Platform提供的数据收集技术重点关注所摄取数据集的发现性和可访问性。 这些技术包括：

* [Adobe Experience Platform边缘网络](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [标记](../tags/home.md)
* [事件转发](../tags/ui/event-forwarding/overview.md)
* [Adobe Experience Platform Web SDK](../edge/home.md)
* [体验数据模型(XDM)](../xdm/home.md)

![](./images/Collection.png)

## 更简单的实施，更快的客户端性能

Adobe Experience Platform Web和Mobile SDK会折叠所有Adobe产品库，并将其压缩为适用于Web平台或移动平台的单个开发工具包。 压缩这些库可加快数据收集速度，并将操作整合到从客户端设备到Adobe Experience Platform边缘网络的单个流中。

## 切换过程以部署Adobe技术 {#edge}

Platform Edge Network是一个全球分布式、快速、可靠的服务器网络，能够大规模接收和处理数据。 使用标记，您可以为Adobe Target、Adobe Audience Manager和Adobe Analytics等产品设置[数据流](../edge/fundamentals/datastreams.md)，这样您就可以在服务器端激活这些产品，而无需更改客户端代码。

![](./images/deploy.png)

>[!NOTE]
>
>有关Platform Edge Network的高级介绍，请参阅以下[交互式产品导览](https://adobe-ideacloud.forgedx.com/adobe-adobe-edge-collection/adobe-experience-edge/public/mx?SUID=hgb1a48ICSCpbM6MzBYHbxnsh9DgjUy1)。

## 快速安全地转换、扩充和发送数据

[Adobe Experience Platform中的事件转](../tags/ui/event-forwarding/overview.md) 发可以点按任何Platform数据流。您可以以极低的延迟转换、扩充数据，并将数据发送到任何非Adobe目的地，而无需向客户端设备添加任何第三方代码，从而提供更快、更安全的数据收集和分发。

![](./images/launch.png)

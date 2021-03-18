---
keywords: Experience Platform；主页；热门主题；数据收集；启动；web sdk
solution: Experience Platform
title: 数据收集概述
topic: 概述
description: 了解与收集Adobe Experience Platform客户体验数据相关的各种技术。
translation-type: tm+mt
source-git-commit: 629fe68029a9f45e45d5e2d238ffff455c7d6de6
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 3%

---


# 数据收集概述

Adobe Experience Platform提供一套技术，允许您从客户端源收集客户体验数据，并将其发送到Adobe Experience Platform Edge Network，在几秒钟内将其丰富、转换并分发到Adobe或非Adobe目标。

支持以下客户端源的数据收集：

* 基于Web的应用程序
* 本机移动应用程序
* 机顶盒(OTT)应用程序

Experience Platform提供的数据收集技术侧重于所摄取数据集的可发现性和可访问性。 这些技术包括：

* [Adobe Experience Platform Edge Network](https://experienceleague.adobe.com/docs/web-sdk-learn/tutorials/introduction-to-web-sdk-and-edge-network.html)
* [Adobe Experience Platform Launch](https://adobe.com/go/launch_help_en)
* [Adobe Experience Platform Web SDK](../edge/home.md)
* [体验数据模型(XDM)](../xdm/home.md)

![](./images/Collection.png)

## 实现更简单，客户端性能更高

Adobe Experience Platform Web和移动SDK可折叠所有Adobe产品库并将其压缩为用于Web或移动平台的单个开发工具包。 压缩这些库可加快数据收集并将操作合并到从客户端设备到Adobe Experience Platform Edge Network的单个流中。

## 通过切换过程部署Adobe技术

Platform Edge Network是一个全球分布式、快速、可靠的服务器网络，能够大规模地接收和处理数据。 使用Platform launch，您可以为Adobe Target、Adobe Audience Manager和Adobe Analytics等产品设置[边缘配置](../edge/fundamentals/edge-configuration.md)，这样您就可以在服务器端激活这些产品，而无需更改客户端代码。

![](./images/deploy.png)

## 快速、安全地转换、丰富和发送数据

[Adobe Experience Platform Launch Server ](https://experienceleague.adobe.com/docs/launch/using/server-side-info/server-side-overview.html) Sidecan接入任何平台数据流。您可以以极低的延迟转换、丰富数据并将数据发送到任何非Adobe目标，而无需向客户端设备添加任何第三方代码，从而提供更快、更安全的数据收集和分发。

![](./images/launch.png)
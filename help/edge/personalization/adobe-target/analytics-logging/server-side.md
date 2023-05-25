---
title: Platform Web SDK中的A4T数据的服务器端日志记录
description: 了解如何使用Experience PlatformWeb SDK为Adobe Analytics for Target (A4T)启用服务器端日志记录。
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t；target；web；sdk；平台；日志记录；
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: 38d54b2c793c9dcb1a45ec4acbb9016d1e927d23
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Platform Web SDK中的A4T数据的服务器端日志记录

Adobe Experience Platform Web SDK允许您在Platform Edge Network上实施Adobe Analytics for Target (A4T)功能。 启用服务器端日志记录后，通过Edge Network发送的所有Analytics点击量都会在服务器端使用Target详细信息进行增强，而无需经过点击拼合过程。

当在数据流配置中启用Analytics时，将启用Analytics的服务器端日志记录：

![已启用Analytics数据流配置](../assets/enable-analytics-datastream.png)

下图显示了启用服务器端Analytics日志记录时数据如何流经系统：

![服务器端日志记录流程](../assets/analytics-server-side-logging.png)

## 后续步骤

本指南介绍了Web SDK中A4T数据的服务器端日志记录。 请参阅指南，网址为 [客户端日志记录](./client-side.md) 以了解有关如何在客户端处理A4T数据的更多信息。

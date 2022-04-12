---
title: Platform Web SDK中A4T数据的服务器端日志记录
description: 了解如何使用Experience PlatformWeb SDK为Adobe Analytics for Target(A4T)启用服务器端日志记录。
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;Target;Web;SDK；平台；日志记录
source-git-commit: a2214465001f90d19d88c0622c154e7a4ae3bb03
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Platform Web SDK中A4T数据的服务器端日志记录

Adobe Experience Platform Web SDK允许您在Platform Edge Network上实施Adobe Analytics for Target(A4T)功能。 启用服务器端日志记录后，通过边缘网络发送的所有Analytics点击都将通过服务器端的Target详细信息进行增强，而无需执行点击拼合过程。

在数据流配置中启用Analytics时，将启用Analytics的服务器端日志记录：

![已启用Analytics数据流配置](../assets/enable-analytics-datastream.png)

下图显示了启用服务器端Analytics日志记录时数据如何通过系统流动：

![服务器端日志记录流](../assets/analytics-server-side-logging.png)

## 后续步骤

本指南介绍了Web SDK中A4T数据的服务器端日志记录。 请参阅 [客户端日志记录](./client-side.md) 有关如何在客户端处理A4T数据的更多信息。

---
title: Platform Web SDK中A4T数据的服务器端日志记录
description: 了解如何使用Experience PlatformWeb SDK为Adobe Analytics for Target (A4T)启用服务器端日志记录。
seo-title: Server-side logging for A4T data in Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t；target；web；sdk；平台；日志记录；
exl-id: 26c25f58-e43c-4147-8595-69ea85af561f
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 1%

---

# Platform Web SDK中A4T数据的服务器端日志记录

Adobe Experience Platform Web SDK允许您在Platform Edge Network上实施Adobe Analytics for Target (A4T)功能。 启用服务器端日志记录后，所有通过Edge Network发送的Analytics点击量都会在服务器端使用Target详细信息增加，而无需经过点击拼合过程。

当在数据流配置中启用Analytics时，将启用Analytics的服务器端日志记录：

![Analytics数据流配置已启用](../assets/enable-analytics-datastream.png)

下图显示了启用服务器端Analytics日志记录时数据如何流经系统：

![服务器端日志记录流程](../assets/analytics-server-side-logging.png)

## 后续步骤

本指南介绍Web SDK中A4T数据的服务器端日志记录。 请参阅指南，网址为 [客户端日志记录](./client-side.md) 以了解有关如何在客户端处理A4T数据的更多信息。

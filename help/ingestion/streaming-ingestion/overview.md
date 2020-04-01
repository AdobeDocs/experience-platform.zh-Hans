---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform流摄取概述
topic: overview
translation-type: tm+mt
source-git-commit: a570a7a3d905c4618d80f56f01747cced1d124e8

---


# 流摄取概述

Adobe Experience Platform的流摄取为用户提供了一种将数据从客户端和服务器端设备实时发送到Experience Platform的方法。

## 您可以使用流式摄取做什么？

Adobe Experience Platform使您能够为每位客户生成实时客户用户档案，从而推动协调一致的相关体验。 流化摄取在构建这些用户档案中起着关键作用，它使您能够在尽可能少的延迟的情况下将用户档案数据交付到数据湖中。

### 流用户档案记录和ExperienceEvent

通过流式摄取，用户可以在数秒内将用户档案记录和ExperienceEvents流式传送到平台，从而帮助推动实时个性化。 发送到流式摄取API的所有数据将自动保留在数据湖中。

请阅读创建 [流连接指南](../tutorials/create-streaming-connection.md) ，了解更多信息。

### 流到数据集

一旦您确信数据是干净的，您就可以为实时客户用户档案和标识服务启用数据集。

有关为用户档案和标识服务启用数据集的详细信息，请阅读配置 [数据集指南](../../profile/tutorials/dataset-configuration.md)。

## 平台上的流化摄取预期的延迟是什么？

| 目标 | 预期延迟 |
| --------- | ---------------- |
| 实时客户资料 | &lt; 1分钟 |
| 数据湖 | &lt; 60 分钟 |

## Adobe Experience Platform 扩展

您可以使用Adobe Experience Platform扩展创建新的流连接。 Experience Platform扩展可提供将Experience Data Model(XDM)格式的信标发送到Experience Platform的实时接收操作。 有关详细 [信息，请访问Experience Platform Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) 文档。
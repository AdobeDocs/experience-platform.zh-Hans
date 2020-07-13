---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform流摄取概述
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 3%

---


# 流摄取概述

Adobe Experience Platform的流式获取为用户提供了一种将数据从客户端和服务器端设备实时发送到Experience Platform的方法。

## 流摄取有哪些功能？

Adobe Experience Platform使您能够为每位客户生成实时客户用户档案，从而推动协调、一致和相关的体验。 流式摄取在构建这些用户档案方面起着关键作用，使您能够尽可能少的延迟将用户档案数据交付到数据湖。

以下视频旨在帮助您理解流摄取，并概述上述概念。

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 流用户档案记录和ExperienceEvents

借助流式摄取，用户可以在数秒内将用户档案记录和ExperienceEvents流式传输到平台，从而帮助推动实时个性化。 发送到流式摄取API的所有数据将自动保留在数据湖中。

请阅读创建 [流连接指南](../tutorials/create-streaming-connection.md) ，了解详细信息。

### 流到数据集

一旦您确信数据是干净的，您就可以启用数据集，供实时客户用户档案和身份服务使用。

有关为用户档案和身份服务启用数据集的详细信息，请阅 [读配置数据集指南](../../profile/tutorials/dataset-configuration.md)。

## 平台上的流式接收预期延迟是多少？

| 目标 | 预期延迟 |
| --------- | ---------------- |
| 实时客户资料 | &lt; 1分钟 |
| 数据湖 | &lt; 60 分钟 |

## Adobe Experience Platform 扩展

您可以使用Adobe Experience Platform扩展创建新的流连接。 Experience Platform扩展提供操作，以将体验数据模型(XDM)中格式化的信标实时发送到Experience Platform。 有关详细 [信息，请访](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) 问Experience Platform扩展文档。
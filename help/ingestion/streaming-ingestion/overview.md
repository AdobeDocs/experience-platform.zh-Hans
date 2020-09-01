---
keywords: Experience Platform;home;popular topics;data ingestion;ingested data;streaming;overview;streaming ingestion;latency;streaming latency;
solution: Experience Platform
title: Adobe Experience Platform流摄取概述
topic: overview
description: Adobe Experience Platform的流式摄取为用户提供了一种将数据从客户端和服务器端设备实时发送到Experience Platform的方法。
translation-type: tm+mt
source-git-commit: c04fb056d4564e53f192e0734a700a13820f5ba7
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 3%

---


# 流摄取概述

Adobe Experience Platform的流式摄取为用户提供了一种将数据从客户端和服务器端设备实时 [!DNL Experience Platform] 发送到的方法。

## 流摄取有哪些功能？

Adobe Experience Platform通过为每个客户生成一个，使您能够推动协调、一 [!DNL Real-time Customer Profile] 致和相关的体验。 流式摄取在构建这些用户档案方面起着关键作用，您可 [!DNL Profile] 以在尽可能 [!DNL Data Lake] 少的延迟下向中传送数据。

以下视频旨在帮助您理解流摄取，并概述上述概念。

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 流用户档案记录和 [!DNL ExperienceEvents]

借助流式摄取，用户可以流式传输用户档案 [!DNL ExperienceEvents] 记录 [!DNL Platform] 并在数秒内完成，从而帮助推动实时个性化。 发送到流式摄取API的所有数据将自动保留在 [!DNL Data Lake]中。

请阅读创建 [流连接指南](../tutorials/create-streaming-connection.md) ，了解更多信息。

### 流到数据集

一旦您确信数据是干净的，您就可以为和启用数据 [!DNL Real-time Customer Profile] 集 [!DNL Identity Service]。

有关为和启用数据集的更 [!DNL Profile] 多信 [!DNL Identity Service]息，请阅读 [配置数据集指南](../../profile/tutorials/dataset-configuration.md)。

## What is the expected latency for streaming ingestion on [!DNL Platform]?

| 目标 | 预期延迟 |
| --------- | ---------------- |
| 实时客户资料 | &lt; 1分钟 |
| 数据湖 | &lt; 60 分钟 |

## Adobe Experience Platform 扩展

您可以使用Adobe Experience Platform扩展创建新的流连接。 扩 [!DNL Experience Platform] 展功能提供将格式化为( [!DNL Experience Data Model] XDM)的信标实时接收到的操作 [!DNL Experience Platform]。 有关详细 [信息，请访](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) 问Experience Platform扩展文档。
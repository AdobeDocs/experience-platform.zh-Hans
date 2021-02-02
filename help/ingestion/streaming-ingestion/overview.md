---
keywords: Experience Platform；主页；热门主题；数据摄取；摄取的数据；流；概述；流摄取；延迟；流延迟；
solution: Experience Platform
title: Adobe Experience Platform流摄取概述
topic: overview
description: Adobe Experience Platform的流式摄取为用户提供了一种将数据从客户端和服务器端设备实时发送到Experience Platform的方法。
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 3%

---


# 流摄取概述

Adobe Experience Platform的流摄取为用户提供了一种将数据从客户端和服务器端设备实时发送到[!DNL Experience Platform]的方法。

## 流摄取有哪些功能？

Adobe Experience Platform通过为每位客户生成[!DNL Real-time Customer Profile]，帮您打造协调、一致、相关的体验。 流摄取在构建这些用户档案中起着关键作用，您可以在尽可能少的延迟的情况下将[!DNL Profile]数据传送到[!DNL Data Lake]中。

以下视频旨在帮助您理解流摄取，并概述上述概念。

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 流用户档案记录和[!DNL ExperienceEvents]

借助流式摄取，用户可以在数秒内将用户档案记录和[!DNL ExperienceEvents]流化到[!DNL Platform]，从而帮助推动实时个性化。 发送到流式摄取API的所有数据将自动保留在[!DNL Data Lake]中。

请阅读[创建流连接指南](../tutorials/create-streaming-connection.md)以了解更多信息。

### 流到数据集

一旦您确信数据是干净的，就可以为[!DNL Real-time Customer Profile]和[!DNL Identity Service]启用数据集。

有关为[!DNL Profile]和[!DNL Identity Service]启用数据集的详细信息，请阅读[配置数据集指南](../../profile/tutorials/dataset-configuration.md)。

## 在[!DNL Platform]上流化接收的预期延迟是什么？

| 目标 | 预期延迟 |
| --------- | ---------------- |
| 实时客户资料 | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| 数据湖 | &lt; 60 分钟 |

## Adobe Experience Platform 扩展

您可以使用Adobe Experience Platform扩展创建新的流连接。 [!DNL Experience Platform]扩展提供将在[!DNL Experience Data Model](XDM)中格式化的信标实时接收到[!DNL Experience Platform]的操作。 有关详细信息，请访问[Experience Platform扩展](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html)文档。
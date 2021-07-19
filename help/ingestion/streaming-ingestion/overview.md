---
keywords: Experience Platform；主页；热门主题；数据摄取；摄取数据；流；概述；流摄取；延迟；流延迟；
solution: Experience Platform
title: 流摄取概述
topic-legacy: overview
description: Adobe Experience Platform的流式摄取为用户提供了一种方法，可将数据从客户端和服务器端设备实时发送到Experience Platform。
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 3%

---

# 流摄取概述

Adobe Experience Platform的流式摄取为用户提供了一种方法，可将数据从客户端和服务器端设备实时发送到[!DNL Experience Platform]。

## 使用流式引入可以执行哪些操作？

Adobe Experience Platform可以为您的每个客户生成[!DNL Real-time Customer Profile] ，从而促进协调、一致和相关的体验。 流式摄取在构建这些配置文件方面发挥着关键作用，具体方法是让您能够在尽可能少的延迟下将[!DNL Profile]数据交付到[!DNL Data Lake]中。

以下视频旨在帮助支持您了解流摄取，并概述了上述概念。

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 流配置文件记录和[!DNL ExperienceEvents]

通过流式引入，用户可以在数秒内将用户档案记录和[!DNL ExperienceEvents]流式传输到[!DNL Platform]，以帮助促进实时个性化。 发送到流式引入API的所有数据都会自动保留在[!DNL Data Lake]中。

请阅读[创建流连接指南](../tutorials/create-streaming-connection.md)以了解详细信息。

### 流到数据集

确定数据是干净的后，您便可以为[!DNL Real-time Customer Profile]和[!DNL Identity Service]启用数据集。

有关为[!DNL Profile]和[!DNL Identity Service]启用数据集的更多信息，请阅读[配置数据集指南](../../profile/tutorials/dataset-configuration.md)。

## [!DNL Platform]上的流式引入的预期滞后时间是多少？

| 目标 | 预期滞后 |
| --------- | ---------------- |
| 实时客户资料 | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| 数据湖 | &lt; 60 分钟 |

## Adobe Experience Platform 扩展

您可以使用Adobe Experience Platform扩展创建新的流连接。 [!DNL Experience Platform]扩展提供操作，以将[!DNL Experience Data Model](XDM)中格式的信标实时摄取到[!DNL Experience Platform]。 有关更多信息，请访问[Experience Platform扩展](../../tags/extensions/web/sdk/overview.md)文档。

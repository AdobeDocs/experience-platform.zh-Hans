---
keywords: Experience Platform；主页；热门主题；数据摄取；引入的数据；流；概述；流摄取；延迟；流延迟；
solution: Experience Platform
title: 流式摄取概述
description: Adobe Experience Platform的流式摄取为用户提供了一种实时将数据从客户端和服务器端设备发送到Experience Platform的方法。
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: f5ae9170b312d9f24c863a14b8cc2310fcaf1cb2
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 2%

---

# 流摄取概述

Adobe Experience Platform的流式摄取为用户提供了一种方法，可实时将数据从客户端和服务器端设备发送到[!DNL Experience Platform]。

## 您可以使用流式摄取做什么？

Adobe Experience Platform允许您通过为每个客户生成[!DNL Real-Time Customer Profile]来推动协调、一致和相关体验。 流式摄取在生成这些配置文件方面发挥着关键作用，它允许您以尽可能少的延迟将[!DNL Profile]数据传送到[!DNL Data Lake]。

以下视频旨在帮助您了解流摄取，并概述了上述概念。

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 流配置文件记录和[!DNL ExperienceEvents]

通过流式摄取，用户可在几秒内流式传输配置文件记录和[!DNL ExperienceEvents]到[!DNL Experience Platform]，以帮助实现实时个性化。 发送到流式引入API的所有数据都会自动保留在[!DNL Data Lake]中。

有关详细信息，请参阅[创建流连接指南](../tutorials/create-streaming-connection.md)。

### 流到数据集

一旦您确信数据是干净的，就可以为[!DNL Real-Time Customer Profile]和[!DNL Identity Service]启用数据集。

有关为[!DNL Profile]和[!DNL Identity Service]启用数据集的详细信息，请参阅[配置数据集指南](../../profile/tutorials/dataset-configuration.md)。

## 在Experience Platform上流式摄取的预期滞后时间是多少？

>[!IMPORTANT]
>
>流式摄取的护栏将绑定到与您的整个组织对应的总许可证使用授权。 此外，开发沙盒中的数据使用限制为总配置文件的10%。 有关许可证使用授权的更多信息，请阅读[数据管理最佳实践指南](../../landing/license-usage-and-guardrails/data-management-best-practices.md)。 要了解如何设置流吞吐量的限制，请阅读[容量概述](../../landing/license-usage-and-guardrails/capacity.md)。

| 目标 | 预期延迟 |
| --------- | ---------------- |
| 实时客户轮廓 | &lt; 15分钟，位于第95百分位数 |
| 数据湖 | &lt; 60分钟 |

## 流摄取的每秒请求(RPS)指南

下表显示了有关流式摄取的请求每秒数限制的指南。

| RPS限制 | 注释 |
| --- | --- |
| 每秒1000个请求 | 使用`/collection/batch`终结点时，这些消息可以包含多条消息。 |
| 每秒10000封个别邮件 | 使用`/collection/`端点时，可以将消息分组为更少的实际请求。 |

>[!IMPORTANT]
>
>使用同步验证时，强制限制变为每分钟&#x200B;**60个请求**，因为此限制用于调试目的。

## Adobe Experience Platform扩展

您可以使用Adobe Experience Platform扩展创建新的流连接。 [!DNL Experience Platform]扩展提供操作以将[!DNL Experience Data Model] (XDM)格式的信标实时摄取到[!DNL Experience Platform]。 有关详细信息，请访问[Experience Platform扩展](../../tags/extensions/client/web-sdk/overview.md)文档。

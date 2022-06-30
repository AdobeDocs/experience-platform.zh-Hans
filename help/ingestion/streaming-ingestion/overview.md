---
keywords: Experience Platform；主页；热门主题；数据摄取；摄取数据；流；概述；流摄取；延迟；流延迟；
solution: Experience Platform
title: 流摄取概述
topic-legacy: overview
description: Adobe Experience Platform的流式摄取为用户提供了一种方法，可将数据从客户端和服务器端设备实时发送到Experience Platform。
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 3ec4bfcb185459ec644ce1826e2a970cb6294538
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 2%

---

# 流摄取概述

Adobe Experience Platform的流式摄取为用户提供了一种将数据从客户端和服务器端设备发送到 [!DNL Experience Platform] 实时。

## 使用流式引入可以执行哪些操作？

Adobe Experience Platform让您能够通过生成 [!DNL Real-time Customer Profile] 针对每个客户。 流式摄取通过使您能够交付 [!DNL Profile] 数据 [!DNL Data Lake] 尽可能少的延迟。

以下视频旨在帮助支持您了解流摄取，并概述了上述概念。

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 流用户档案记录和 [!DNL ExperienceEvents]

通过流式引入，用户可以流式传输用户档案记录和 [!DNL ExperienceEvents] to [!DNL Platform] 以秒为单位帮助促进实时个性化。 发送到流式引入API的所有数据都会自动保留在 [!DNL Data Lake].

请阅读 [创建流连接指南](../tutorials/create-streaming-connection.md) 以了解更多信息。

### 流到数据集

确定数据是干净的后，您便可以为 [!DNL Real-time Customer Profile] 和 [!DNL Identity Service].

有关为 [!DNL Profile] 和 [!DNL Identity Service]，请阅读 [配置数据集指南](../../profile/tutorials/dataset-configuration.md).

## 上的流式摄取的预期滞后时间是多少 [!DNL Platform]?

| 目标 | 预期滞后 |
| --------- | ---------------- |
| 实时客户个人资料 | &lt; 1分钟 |
| 数据湖 | &lt; 60 分钟 |

## 流摄取的每秒请求(RPS)指南

下表显示了有关流摄取的请求每秒数限制的指导。

| RPS限制 | 注释 |
| --- | --- |
| 每秒1000次请求 | 使用 `/collection/batch` 端点。 |
| 每秒10000条单条消息 | 使用 `/collection/batch` 端点。 |

>[!IMPORTANT]
>
>强制限制将变为 **每分钟60次请求** 在将同步验证用于调试目的时。

## Adobe Experience Platform 扩展

您可以使用Adobe Experience Platform扩展创建新的流连接。 的 [!DNL Experience Platform] 扩展提供了用于发送 [!DNL Experience Data Model] (XDM)，用于实时摄取到 [!DNL Experience Platform]. 访问 [Experience Platform扩展](../../tags/extensions/web/sdk/overview.md) 文档以了解更多信息。

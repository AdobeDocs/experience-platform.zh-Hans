---
keywords: Experience Platform；主页；热门主题；数据摄取；引入的数据；流；概述；流摄取；延迟；流延迟；
solution: Experience Platform
title: 流式摄取概述
description: Adobe Experience Platform的流式摄取为用户提供了一种实时将数据从客户端和服务器端设备发送到Experience Platform的方法。
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 5adcdf3108fbbaee9e81dc737ae67b563e4dbf1d
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 4%

---

# 流式摄取概述

Adobe Experience Platform的流式摄取为用户提供了一种从客户端和服务器端设备将数据发送到的方法 [!DNL Experience Platform] 实时。

## 您可以使用流式摄取做什么？

Adobe Experience Platform允许您通过生成 [!DNL Real-Time Customer Profile] 每个客户的服务。 流式摄取通过让您提供，在构建这些用户档案的过程中扮演着关键角色 [!DNL Profile] 数据进入 [!DNL Data Lake] 尽可能缩短延迟。

以下视频旨在帮助您了解流摄取，并概述了上述概念。

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 流配置文件记录和 [!DNL ExperienceEvents]

通过流式摄取，用户可以流式传输配置文件记录并 [!DNL ExperienceEvents] 到 [!DNL Platform] 以秒为单位，帮助推动实时个性化。 发送到流式引入API的所有数据都会自动保留在 [!DNL Data Lake].

请阅读 [创建流连接指南](../tutorials/create-streaming-connection.md) 以了解更多信息。

### 流到数据集

一旦您确信数据是干净的，就可以为以下项启用数据集 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service].

有关启用数据集的更多信息 [!DNL Profile] 和 [!DNL Identity Service]，请阅读 [配置数据集指南](../../profile/tutorials/dataset-configuration.md).

## 流式摄取的预期滞后时间是多少？ [!DNL Platform]？

| 目标 | 预期延迟 |
| --------- | ---------------- |
| 实时客户配置文件 | &lt; 15 分钟 |
| 数据湖 | &lt; 60 分钟 |

## 流摄取的每秒请求(RPS)指南

下表显示了有关流式摄取的请求每秒数限制的指南。

| RPS限制 | 注释 |
| --- | --- |
| 每秒1000个请求 | 使用时，这些消息可能包含多条消息 `/collection/batch` 端点。 |
| 每秒10000封个别邮件 | 使用时，可将消息分组为更少的实际请求 `/collection/batch` 端点。 |

>[!IMPORTANT]
>
>强制限制将变为 **每分钟60个请求** 在使用同步验证时，由于它用于调试目的。

## Adobe Experience Platform 扩展

您可以使用Adobe Experience Platform扩展创建新的流连接。 此 [!DNL Experience Platform] 扩展提供了用于发送信标的操作，格式如下： [!DNL Experience Data Model] (XDM)实时摄取到 [!DNL Experience Platform]. 访问 [Experience Platform扩展](../../tags/extensions/client/web-sdk/overview.md) 文档，以了解更多信息。

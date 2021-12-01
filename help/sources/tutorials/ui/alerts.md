---
keywords: Experience Platform；主页；热门主题；警报
description: 创建数据流时，您可以订阅警报，以接收有关流程运行状态、成功或失败的警报消息。
title: 在UI中订阅上下文关联警报
hide: true
hidefromtoc: true
source-git-commit: a81d21f615206e644044c2f0f546a458d1aebbf3
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# 订阅警报消息，以在UI中监视源数据流

Adobe Experience Platform允许您订阅有关Adobe Experience Platform活动的基于事件的警报。 警报可减少或消除轮询 [[!DNL Observability Insights] API](../../../observability/api/overview.md) 为了检查作业是否已完成、是否已到达工作流中的某个里程碑，或是否发生任何错误。

创建数据流时，您可以订阅警报，以接收有关流程运行状态、成功或失败的警报消息。

本文档提供了有关如何订阅警报以及接收流运行的警报消息的步骤。

## 快速入门

本文档要求您对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../home.md): [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用来构建、标记和增强传入数据 [!DNL Platform] 服务。
* [可观测性](../../../observability/home.md): [!DNL Observability Insights] 允许您通过使用统计量度和事件通知来监控平台活动。
   * [警报](../../../observability/alerts/overview.md):当您的Platform操作达到一组特定条件（例如，当系统超出阈值时可能出现问题）时，Platform可以向组织中订阅了这些条件的任何用户发送警报消息。

## 在UI中订阅警报 {#subscribe-sources-alerts}

>[!CONTEXTUALHELP]
>id="platform_sources_alerts_subscribe"
>title="订阅源警报"
>abstract="警报允许您根据源数据流的状态接收通知。 如果数据流已启动、成功、失败或未摄取任何数据，则可以设置警报通知以获取更新。"
>text="Learn more in documentation"

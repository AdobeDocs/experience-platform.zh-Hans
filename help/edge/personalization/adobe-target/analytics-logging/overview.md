---
title: Platform Web SDK中的Adobe Analytics for Target (A4T)记录
description: 了解如何使用Experience PlatformWeb SDK控制Adobe Analytics for Target (A4T)数据的收集。
seo-title: Adobe Analytics for Target (A4T) Logging in the Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t；日志记录；analytics；sdk；web sdk；
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# Platform Web SDK中的Adobe Analytics for Target (A4T)记录

在使用Adobe Target进行个性化时，您可以选择想要用于性能测量的系统。 每个 [Target活动](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) 允许您在Target报表和Adobe Analytics报表之间进行选择。

如果您使用的是Analytics报表，则Adobe Target必须向Analytics传达以下信息：

* 您的访客已进入哪个Adobe Target活动
* 他们看到的体验
* 已达到哪个转化

Adobe Experience Platform Web SDK支持两种类型的Analytics Logging for Target (A4T)用例：

| 日志记录方法 | 描述 |
| --- | --- |
| 服务器端Analytics | 通过Edge Network发送的所有Analytics点击在服务器端都通过Target详细信息进行增强，而无需经过点击拼合过程。 |
| 客户端分析日志记录 | Target数据会在客户端返回，从而允许您使用 [数据插入API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

日志记录方法取决于您配置的服务器上是否启用了Adobe Analytics [数据流](../../../datastreams/overview.md)：

![日志记录方法决策流程](../assets/analytics-logging.png)

## 后续步骤

本文档简要介绍了Web SDK中针对A4T数据的各种记录方法。 有关上述每种方法的更多详细信息，请参阅以下文档：

* [Platform Web SDK中的A4T数据的服务器端日志记录](./server-side.md)
* [Platform Web SDK中A4T数据的客户端日志记录](./client-side.md)

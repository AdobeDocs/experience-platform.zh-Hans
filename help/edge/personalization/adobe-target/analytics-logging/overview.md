---
title: Adobe Analytics for Target(A4T)在平台Web SDK中日志记录
description: 了解如何使用Adobe Analytics Web SDK控制Target(A4T)Experience Platform的收集。
seo-title: Adobe Analytics for Target (A4T) Logging in the Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t；日志记录；analytics;sdk;web sdk;
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# Adobe Analytics for Target(A4T)在Platform Web SDK中日志记录

使用Adobe Target进行个性化时，您可以选择要用于性能测量的系统。 每个 [Target活动](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) 允许您在Target报表和Adobe Analytics报表之间进行选择。

如果您使用的是Analytics报表，Adobe Target必须将以下内容与Analytics通信：

* 访客已进入的Adobe Target活动
* 他们看过哪些体验
* 已实现哪种转化

Adobe Experience Platform Web SDK支持两种类型的Analytics for Target(A4T)日志记录用例：

| 日志记录方法 | 描述 |
| --- | --- |
| 服务器端分析日志记录 | 通过边缘网络发送的所有Analytics点击都将通过服务器端的Target详细信息进行增强，而无需完成点击拼合过程。 |
| 客户端分析日志记录 | Target数据在客户端返回，允许您使用 [数据插入API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

日志记录方法取决于您是否在配置的 [数据流](../../../datastreams/overview.md):

![测井方法决策流程](../assets/analytics-logging.png)

## 后续步骤

本文档简要介绍Web SDK中A4T数据的不同日志记录方法。 有关每种方法的更多详细信息，请参阅以下文档：

* [平台Web SDK中A4T数据的服务器端日志记录](./server-side.md)
* [平台Web SDK中A4T数据的客户端日志记录](./client-side.md)

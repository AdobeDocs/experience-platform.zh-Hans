---
title: Platform Web SDK中的Adobe Analytics for Target (A4T)日志记录
description: 了解如何使用Experience PlatformWeb SDK控制Adobe Analytics for Target (A4T)数据的收集。
seo-title: Adobe Analytics for Target (A4T) Logging in the Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t；日志记录；analytics；sdk；web sdk；
exl-id: f1c90ccd-48a9-4668-b2ac-eacd5bec0b91
source-git-commit: 5f2358c2e102c66a13746004ad73e2766e933705
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# Platform Web SDK中的Adobe Analytics for Target (A4T)日志记录

使用Adobe Target进行个性化时，您可以选择用于性能测量的系统。 每个 [Target活动](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) 允许您在Target报表和Adobe Analytics报表之间进行选择。

如果您使用的是Analytics报表，则Adobe Target必须向Analytics传达以下信息：

* 访客已进入哪个Adobe Target活动
* 他们看到的体验
* 已达到哪个转化

Adobe Experience Platform Web SDK支持以下两种类型的Analytics Logging for Target (A4T)用例：

| 日志记录方法 | 描述 |
| --- | --- |
| 服务器端Analytics日志 | 所有通过Edge Network发送的Analytics点击量都会在服务器端使用Target详细信息进行增强，而无需经过点击拼合过程。 |
| 客户端分析日志记录 | Target数据会在客户端返回，从而允许您使用手动补充数据并将数据发送到Analytics。 [数据插入API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html). |

日志记录方法取决于您配置的是否启用了Adobe Analytics [数据流](../../../../datastreams/overview.md)：

![日志记录方法决策流程](../assets/analytics-logging.png)

## 后续步骤

本文档简要介绍Web SDK中针对A4T数据的各种记录方法。 有关每种方法的更多详细信息，请参阅以下文档：

* [Platform Web SDK中A4T数据的服务器端日志记录](./server-side.md)
* [Platform Web SDK中A4T数据的客户端日志记录](./client-side.md)

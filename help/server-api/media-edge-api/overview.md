---
keywords: Experience Platform；media edge；热门主题；日期范围
solution: Experience Platform
title: Media Edge API
description: Media Edge API概述。
exl-id: null
source-git-commit: 696ddd93d87601f9f6dedfd651ee12573dc4990a
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 4%

---


# Media Edge API概述

Media Edge API构建于Adobe Experience Platform (AEP)之上，用于在的框架内提供媒体事件跟踪数据 [XDM架构](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=en#:~:text=Experience%20Data%20Model%20(XDM)%2C,the%20power%20of%20digital%20experiences). 对于Media Analytics客户，这将使以下功能可用：

* 替换为 [Customer Journey Analytics(CJA)](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hans)，客户可以获得关于持续时间、开始和停止的近乎实时、精细的详细信息，以便评估和组合媒体量度。 从Adobe Analytics迁移的客户可在CJA中使用所有报告指标。

* 替换为 [Adobe Real-time Customer Data Platform (CDP)](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=zh-Hans)，客户可以使用媒体使用情况数据丰富其实时用户档案。

* 替换为 [Adobe Journey Optimizer (AJO)](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=en)，客户可以优化全渠道营销活动，并通过媒体消费信号自动化历程。


## 优化媒体跟踪数据流

两者 [媒体收集API](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/streaming-media-apis/mc-api-overview.html?lang=en&amp;media-tracking-data-flows) 和Media Edge API将媒体跟踪数据作为RESTful服务提供。 但使用Media Edge服务具有以下优势：

* 这是将XDM架构融入数据流的最简单方法。

* 呼叫将从媒体播放器直接定向到 [Experience Edge Platform Network](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=en).

* 它最有效地跟踪媒体事件。

下表显示了适用于各种Media Analytics案例的AdobeAPI服务：

| 用例 | API服务 |
| -------- | ------ |
| AEP解决方案（CJA、RTDCP、AJO等） | 媒体边缘 |
| CDP + CJA | 媒体边缘 |
| Adobe Analytics + AEP解决方案 | 媒体边缘 |
| 仅限Adobe Analytics（已跟踪） | 媒体收集 |

>[!NOTE]
>
> Analytics的媒体收集API服务仍会接收XDM数据，但不会针对Media Edge服务的程度对其进行优化。 根据从媒体播放器发送的数据，还可以通过Media Edge API服务路由某些仅限Analytics的数据。

下图显示了这两个API服务的数据流：


![Media Analytics数据流](../assets/edge-api-dataflow.png)


有关使用Media Edge API的更多信息，请参阅入门文档。

有关使用Platform Edge的更多信息，请参阅 [使用Experience Platform边缘安装Media Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/implementation-edge.html?lang=en).





---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；experienceevent查询；experienceevent查询；体验事件查询；
title: 列出用户的页面查看次数
description: 了解如何使用Experience Events编写查询，以创建指定用户使用的最后100页的列表。
exl-id: d831910d-d3a4-4a5a-b897-b09f0546dab0
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 1%

---

# 列出用户的页面查看次数

本文档提供了一个列出指定用户的页面查看所需的SQL示例。 使用Adobe Experience Platform查询服务，您可以编写使用[!DNL Experience Events]来捕获各种用例的查询。 体验事件由体验数据模型(XDM) ExperienceEvent类表示，该类捕获用户与网站或服务交互时系统的不可变和非聚合快照。 体验事件甚至可用于时域分析。 请参阅[后续步骤部分](#next-steps)以了解更多涉及[!DNL Experience Events]的用例以生成访客报告。

有关XDM和[!DNL Experience Events]的更多信息，请参阅[[!DNL XDM System] 概述](../../xdm/home.md)。 通过将查询服务与[!DNL Experience Events]相结合，您可以有效地跟踪用户之间的行为趋势。 以下文档提供了涉及[!DNL Experience Events]的查询示例。

## 目标

以下示例列出了指定用户查看的最后100个页面。

```sql
SELECT 
timestamp, 
web.webReferrer.type as referrerType, 
web.webReferrer.URL as referrer, 
web.webPageDetails.name as pageName, 
_experience.analytics.event1to100.event1.value as A, 
_experience.analytics.event1to100.event2.value as B, 
_experience.analytics.event1to100.event3.value as C, 
web.webPageDetails.pageviews.value as pageViews
FROM your_analytics_table 
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
ORDER BY timestamp 
LIMIT 100;
```

此查询的结果如下所示。

```console
      timestamp       |  referrerType  |                            referrer                                |                 pageName            |  A  |  B  |  C  | pageViews
|----------------------+----------------+--------------------------------------------------------------------+-------------------------------------+-----+-----+-----+--------------
2019-11-08 17:15:28.0 | typed_bookmark |                                                                    |                                     |     |     |     |
2019-11-08 17:53:05.0 | social         | http://www.reddit.com                                              | Home                                |     |     |     |          1.0
2019-11-08 17:53:45.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 19:22:34.0 | typed_bookmark |                                                                    |                                     |     |     |     |          
2019-11-08 20:01:12.0 | search_engine  | http://www.google.com/search?ie=UTF-8&q=laundry parkas&cid=sem:115 | Home                                |     |     |     |          1.0 
2019-11-08 20:01:57.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 20:03:36.0 | typed_bookmark |                                                                    | Search Results                      | 1.0 |     |     |          1.0
2019-11-08 20:04:30.0 | typed_bookmark |                                                                    | Product Details: Pemmican Power Bar |     |     |     |          1.0
2019-11-08 20:05:27.0 | typed_bookmark |                                                                    | Shopping Cart: Cart Details         |     |     |     |          1.0
2019-11-08 20:06:07.0 | typed_bookmark |                                                                    | Shopping Cart: Shipping Information |     |     |     |          1.0
2019-11-08 20:07:02.0 | typed_bookmark |                                                                    | Shopping Cart: Billing Information  |     |     | 1.0 |          1.0
2019-11-08 20:07:52.0 | typed_bookmark |                                                                    | Shopping Cart: Order Review         |     |     |     |          1.0
2019-11-08 20:08:45.0 | typed_bookmark |                                                                    | Order Confirmation                  |     |     |     |          1.0
2019-11-08 20:09:24.0 | typed_bookmark |                                                                    | Home                                |     |     |     |          1.0
2019-11-08 20:10:03.0 | typed_bookmark |                                                                    | Editorial Page: Camping Essentials  |     |     |     |          1.0
2019-11-08 20:11:01.0 | typed_bookmark |                                                                    | Account Registration|Form           |     |     |     |          1.0
2019-11-08 20:11:38.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
2019-11-08 20:12:10.0 | typed_bookmark |                                                                    | Blog: Iris Sagan                    |     |     |     |          1.0
2019-11-08 20:13:09.0 | typed_bookmark |                                                                    | Product Details: UltraTech Socks    |     |     |     |          1.0
2019-11-08 20:14:05.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
```

## 后续步骤 {#next-steps}

通过阅读本文档，您可以更好地了解如何将查询服务与[!DNL Experience Events]结合使用，以将页面查看作为指定用户列出。

请参阅以下用例，了解其他基于访客的用例：

- [检索按页面查看次数组织的访客列表。](./visitors-by-number-of-page-views.md)
- [查看访客的汇总报表。](./roll-up-report-of-a-visitor.md)
- [按日期创建事件趋势报表。](./trended-report-of-events.md)

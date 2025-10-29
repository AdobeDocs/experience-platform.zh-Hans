---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；experienceevent查询；experienceevent查询；体验事件查询；
title: 创建事件的趋势报表
description: 了解如何使用体验事件编写查询以创建指定日期范围内的事件趋势报表，并按日期分组。
exl-id: 8f7ed5b5-c265-4a1e-a360-4293d1e86e97
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# 创建事件的趋势报表

本文档提供了一个所需的SQL示例，用于按日期创建特定日期范围内的事件的趋势报表。 使用Adobe Experience Platform查询服务，您可以编写使用[!DNL Experience Events]来捕获各种用例的查询。 体验事件由体验数据模型(XDM) ExperienceEvent类表示，该类捕获用户与网站或服务交互时系统的不可变和非聚合快照。 体验事件甚至可用于时域分析。 请参阅[后续步骤部分](#next-steps)以了解更多涉及[!DNL Experience Events]的用例以生成访客报告。

通过报表，您可以访问Experience Platform数据，从而有利于您组织的战略业务洞察。 借助这些报表，您可以通过多种方式检查Experience Platform数据，以易于理解的格式显示关键量度，以及共享生成的见解。

有关XDM和[!DNL Experience Events]的更多信息，请参阅[[!DNL XDM System] 概述](../../xdm/home.md)。 通过将查询服务与[!DNL Experience Events]相结合，您可以有效地跟踪用户之间的行为趋势。 以下文档提供了涉及[!DNL Experience Events]的查询示例。

## 目标

以下示例创建指定日期范围内事件的趋势报表，并按日期分组。 具体来说，此SQL示例汇总了各种analytics值，如`A`、`B`和`C`，然后汇总了在一个月内查看公园的次数。

在[!DNL Experience Event]数据集中找到的时间戳列采用UTC格式。 该示例使用`from_utc_timestamp()`函数将时间戳从UTC转换为EDT，然后使用`date_format()`函数将日期与时间戳的其余部分隔离。

```sql
SELECT 
date_format( from_utc_timestamp(timestamp, 'EDT') , 'yyyy-MM-dd') as Day,
SUM(web.webPageDetails.pageviews.value) as pageViews,
SUM(_experience.analytics.event1to100.event1.value) as A,
SUM(_experience.analytics.event1to100.event2.value) as B,
SUM(_experience.analytics.event1to100.event3.value) as C,
SUM(
    CASE 
    WHEN _experience.analytics.customDimensions.evars.evar1 = 'parkas' 
    THEN 1 
    ELSE 0 
    END) as viewedParkas
FROM your_analytics_table 
WHERE TIMESTAMP >= to_timestamp('2019-03-01') AND TIMESTAMP <= to_timestamp('2019-03-31')
GROUP BY Day 
ORDER BY Day ASC, pageViews DESC;
```

此查询的结果如下所示。

```console
     Day     | pageViews |   A    |   B   |    C    | viewedParkas
|-------------+-----------+--------+-------+---------+--------------
 2019-03-01  |   55317.0 | 8503.0 | 804.0 | 1578.0  |           73
 2019-03-02  |   55302.0 | 8600.0 | 854.0 | 1528.0  |           86
 2019-03-03  |   54613.0 | 8162.0 | 795.0 | 1568.0  |          100
 2019-03-04  |   54501.0 | 8479.0 | 832.0 | 1509.0  |          100
 2019-03-05  |   54941.0 | 8603.0 | 816.0 | 1514.0  |           73
 2019-03-06  |   54817.0 | 8434.0 | 855.0 | 1538.0  |           76
 2019-03-07  |   55201.0 | 8604.0 | 843.0 | 1517.0  |           64
 2019-03-08  |   55020.0 | 8490.0 | 849.0 | 1536.0  |           99
 2019-03-09  |   43186.0 | 6736.0 | 643.0 | 1150.0  |           52
 2019-03-10  |   48471.0 | 7542.0 | 772.0 | 1272.0  |           70
 2019-03-11  |   56307.0 | 8721.0 | 818.0 | 1571.0  |           81
 2019-03-12  |   55374.0 | 8653.0 | 843.0 | 1501.0  |           59
 2019-03-13  |   55046.0 | 8509.0 | 887.0 | 1556.0  |           65
 2019-03-14  |   55518.0 | 8551.0 | 848.0 | 1516.0  |           77
 2019-03-15  |   55329.0 | 8575.0 | 818.0 | 1607.0  |           96
 2019-03-16  |   55030.0 | 8651.0 | 815.0 | 1542.0  |           66
 2019-03-17  |   55143.0 | 8435.0 | 774.0 | 1572.0  |           65
 2019-03-18  |   54065.0 | 8211.0 | 816.0 | 1574.0  |          111
 2019-03-19  |   55097.0 | 8395.0 | 771.0 | 1498.0  |           86
 2019-03-20  |   55198.0 | 8472.0 | 863.0 | 1583.0  |           82
 2019-03-21  |   54978.0 | 8490.0 | 820.0 | 1580.0  |           83
 2019-03-22  |   55464.0 | 8561.0 | 820.0 | 1559.0  |           83
 2019-03-23  |   55384.0 | 8482.0 | 800.0 | 1139.0  |           82
 2019-03-24  |   55295.0 | 8594.0 | 841.0 | 1382.0  |           78
 2019-03-25  |   42069.0 | 6365.0 | 606.0 | 1509.0  |           62
 2019-03-26  |   49724.0 | 7629.0 | 724.0 | 1553.0  |           44
 2019-03-27  |   55111.0 | 8524.0 | 804.0 | 1524.0  |           94
 2019-03-28  |   55030.0 | 8439.0 | 822.0 | 1554.0  |           73
 2019-03-29  |   55281.0 | 8601.0 | 854.0 | 1580.0  |           73
 2019-03-30  |   55162.0 | 8538.0 | 846.0 | 1534.0  |           79
 2019-03-31  |   55437.0 | 8486.0 | 807.0 | 1649.0  |           68
 (31 rows)
```

## 后续步骤 {#next-steps}

通过阅读本文档，您可以更好地了解如何将查询服务与[!DNL Experience Events]结合使用，以有效地跟踪用户之间的行为趋势。

要了解使用[!DNL Experience Events]的其他基于访客的用例，请阅读以下文档：

- [检索按页面查看次数组织的访客列表。](./visitors-by-number-of-page-views.md)
- [列出访客以前的会话。](./list-visitor-sessions.md)
- [查看访客的汇总报表。](./roll-up-report-of-a-visitor.md)

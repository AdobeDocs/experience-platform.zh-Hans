---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；experienceevent查询；experienceevent查询；体验事件查询；
title: 查看特定访客的汇总报表
description: 以下文档提供了在Adobe Experience Platform查询服务中涉及Experience事件的查询示例。
exl-id: 1348503f-65c1-41f9-b111-1284a49449a1
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# 查看特定访客的汇总报表

本文档提供了一个SQL示例，用于聚合特定用户的多个分析属性中的数据，并在一个报表中查看这些数据。 使用Adobe Experience Platform查询服务，您可以编写使用[!DNL Experience Events]来捕获各种用例的查询。 体验事件由体验数据模型(XDM) ExperienceEvent类表示，该类捕获用户与网站或服务交互时系统的不可变和非聚合快照。 体验事件甚至可用于时域分析。 请参阅[后续步骤部分](#next-steps)以了解更多涉及[!DNL Experience Events]的用例以生成访客报告。

有关XDM和[!DNL Experience Events]的更多信息，请参阅[[!DNL XDM System] 概述](../../xdm/home.md)。 通过将查询服务与[!DNL Experience Events]相结合，您可以有效地跟踪用户之间的行为趋势。 以下文档提供了涉及[!DNL Experience Events]的查询示例。

## 目标

以下SQL示例说明如何查看指定用户的各种分析值的聚合报告。

```sql
SELECT 
endUserIds._experience.aaid.id, 
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
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
GROUP BY endUserIds._experience.aaid.id
ORDER BY pageViews DESC;
```

查询结果显示在下表中。

```console
               id                 | pageViews |   A   |   B   |   C   | viewedParkas
|----------------------------------+-----------+-------+-------+-------+--------------
457C3510571E5930-69AA721C4CBF9339 |     706.0 | 83.0  |  7.0  | 38.0  |          22
```

## 后续步骤 {#next-steps}

通过阅读本文档，您能够更好地了解如何将查询服务与[!DNL Experience Events]结合使用，以查看指定用户的分析值的汇总报告。

请参阅以下用例，了解其他基于访客的用例：

- [检索按页面查看次数组织的访客列表。](./visitors-by-number-of-page-views.md)
- [列出访客以前的会话。](./list-visitor-sessions.md)
- [按日期创建事件趋势报表。](./trended-report-of-events.md)

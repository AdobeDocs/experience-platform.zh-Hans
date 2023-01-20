---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；体验事件查询；体验事件查询；体验事件查询；
title: 查看特定访客的汇总报表
description: 以下文档提供了与Adobe Experience Platform查询服务中的体验事件有关的查询示例。
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# 查看特定访客的汇总报表

本文档提供了一个SQL示例，用于从特定用户的多个分析属性中聚合数据，并在一个报表中一起查看该数据。 通过Adobe Experience Platform查询服务，您可以编写使用 [!DNL Experience Events] 来捕获各种用例。 体验事件由体验数据模型(XDM)ExperienceEvent类表示，该类可在用户与网站或服务交互时捕获系统的不可更改和非聚合快照。 体验事件甚至可用于时域分析。 请参阅 [“下一步”部分](#next-steps) 对于涉及 [!DNL Experience Events] 以生成访客报表。

有关XDM和 [!DNL Experience Events] 可在 [[!DNL XDM System] 概述](../../xdm/home.md). 通过将查询服务与 [!DNL Experience Events]，则可以有效地跟踪用户中的行为趋势。 以下文档提供了涉及 [!DNL Experience Events].

## 目标

以下SQL示例显示如何查看指定用户的各种分析值的聚合报表。

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
----------------------------------+-----------+-------+-------+-------+--------------
457C3510571E5930-69AA721C4CBF9339 |     706.0 | 83.0  |  7.0  | 38.0  |          22
```

## 后续步骤 {#next-steps}

通过阅读本文档，您可以更好地了解如何在 [!DNL Experience Events] 查看指定用户的分析值汇总报表。

请参阅以下用例，了解其他基于访客的用例：

- [检索按页面查看次数组织的访客列表。](./visitors-by-number-of-page-views.md)
- [列出访客以前的会话。](./list-visitor-sessions.md)
- [按天创建事件的趋势报表。](./trended-report-of-events.md)

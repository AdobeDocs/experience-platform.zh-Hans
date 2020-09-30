---
keywords: Experience Platform;home;popular topics;query service;Query service;adobe defined functions;query;using adobe defined functions;
solution: Experience Platform
title: Adobe定义函数
topic: queries
type: Tutorial
description: 此文档涵盖Adobe定义的功能(ADF)，可支持三个关键的Analytics活动会话化、归因和路径。
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 5%

---


# 使用Adobe定义的函数

Adobe的主要优势之一是他们了解体验数据以及客户需要如何处理这些数据。 您可以利用这种理解来构建助手功能，使您的工作更轻松。

此文档涵盖Adobe定义的功能(ADF)，以支持三个关键 [!DNL Analytics] 活动:
- [会话化](#sessionization)
- [归因](#attribution)
- [路径分析](#pathing)

## 会话化

重现 `SESS_TIMEOUT()` 了与Adobe Analytics的访问组。 它执行类似的基于时间的分组，但具有可自定义的参数。

**语法：**

`SESS_TIMEOUT(timestamp, timeout_in_seconds) OVER ([partition] [order] [frame])`

**返回：**

具有字段的结构 `(timestamp_diff, num, is_new, depth)`

### 浏览行级和 `SESS_TIMEOUT()` 输出

```sql
SELECT analyticsVisitor,
      session.is_new,
      session.timestamp_diff,
      session.num,
      session.depth
FROM  (
        SELECT endUserIDs._experience.aaid.id as analyticsVisitor,
        SESS_TIMEOUT(timestamp, 60 * 30)
        OVER (PARTITION BY endUserIDs._experience.aaid.id
        ORDER BY timestamp
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
        FROM your_analytics_table
        WHERE TIMESTAMP >= to_timestamp('2018-12-01') AND TIMESTAMP <= to_timestamp('2018-12-31')
      )
LIMIT 100;
```

![图像](../images/queries/adobe-functions/sess-timeout.png)

### 创建包含访客、会话和页面视图的新趋势报告

```sql
SELECT
      date_format( from_utc_timestamp(timestamp, 'EDT') , 'yyyy-MM-dd') as Day,
      COUNT(DISTINCT analyticsVisitor ) as Visitors,
      COUNT(DISTINCT analyticsVisitor || session.num ) as Sessions,
      SUM( PageViews ) as PageViews
FROM
    (
      SELECT
          timestamp,
          endUserIDs._experience.aaid.id as analyticsVisitor,
          SESS_TIMEOUT(timestamp, 60 * 30)
      OVER (PARTITION BY endUserIDs._experience.aaid.id
      ORDER BY timestamp
      ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS session,
          web.webPageDetails.pageviews.value as PageViews
      FROM your_analytics_table
      WHERE TIMESTAMP >= to_timestamp('2018-12-01') AND TIMESTAMP <= to_timestamp('2018-12-31')
    )
GROUP BY Day 
ORDER BY Day DESC 
LIMIT 31;
```

![图像](../images/queries/adobe-functions/trended-report.png)

## 归因

归因是您如何为营销工作分配指标或转化率，如收入、订单或注册。

在Adobe Analytics，属性设置使用eVar等变量进行配置，并在摄取数据时生成。

中找到的归因 [!DNL Query Service] ADF允许在查询时定义和生成这些分配。

此示例重点介绍最后一次触碰归因，但Adobe也会优惠第一次触碰归因。

>[!NOTE]
>
>其他超时选项和基于事件的过期选项将在以后的版本中可用 [!DNL Query Service]。

**语法：**

`ATTRIBUTION_LAST_TOUCH(timestamp, [channel_name], column) OVER ([partition] [order] [frame])`

**返回：**

具有场的结构 `(value)`

### 探索行级归因

```sql
SELECT
  endUserIds._experience.aaid.id,
  _experience.analytics.customDimensions.evars.evar10 as MemberLevel,
  ATTRIBUTION_LAST_TOUCH(timestamp, 'eVar10', _experience.analytics.customDimensions.evars.evar10)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
      AS LastMemberLevel,
  commerce.purchases.value as Orders
FROM your_analytics_table 
WHERE TIMESTAMP >= to_timestamp('2018-04-01') AND TIMESTAMP <= to_timestamp('2018-04-30')
LIMIT 50;
```

![图像](../images/queries/adobe-functions/row-level-attribution.png)

### 按上一成员层创建订单细分(eVar10)

```sql
SELECT
  LastMemberLevel,
  SUM(Orders) as MemberLevelOrders
FROM 
(SELECT
  ATTRIBUTION_LAST_TOUCH(timestamp, 'eVar10', _experience.analytics.customDimensions.evars.evar10)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
      AS LastMemberLevel,
  commerce.purchases.value as Orders
FROM your_analytics_table 
WHERE TIMESTAMP >= to_timestamp('2018-04-01') AND TIMESTAMP <= to_timestamp('2018-04-30')
)
GROUP BY LastMemberLevel 
ORDER BY MemberLevelOrders DESC
LIMIT 25;
```

![图像](../images/queries/adobe-functions/last-member-level.png)

## 路径分析

寻路功能有助于了解客户如何浏览您的网站。 ADF `NEXT()` 和 `PREVIOUS()` ADF使这成为可能。

**语法：**

```sql
NEXT(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])
PREVIOUS(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])
```

**返回：**

具有场的结构 `(value)`

### 选择当前页面和下一页

```sql
SELECT 
      endUserIds._experience.aaid.id,
      timestamp,
      web.webPageDetails.name,
      NEXT(web.webPageDetails.name, 1, true)
          OVER(PARTITION BY endUserIds._experience.aaid.id
              ORDER BY timestamp
              ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
          AS next_pagename
FROM your_analytics_table
WHERE TIMESTAMP >= to_timestamp('2018-12-01') AND TIMESTAMP <= to_timestamp('2018-12-31') 
LIMIT 10;
```

![图像](../images/queries/adobe-functions/select-current-page.png)

### 创建会话条目中前五个页面名称的细分报告

```sql
  SELECT 
    PageName,
    PageName_2,
    PageName_3,
    PageName_4,
    PageName_5,
    SUM(PageViews) as PageViews
  FROM
    (SELECT
      PageName,
      NEXT(PageName, 1, true)
        OVER(PARTITION BY VisitorID, session.num
              ORDER BY timestamp
              ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
        AS PageName_2,
      NEXT(PageName, 2, true)
        OVER(PARTITION BY VisitorID, session.num
              ORDER BY timestamp
              ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
        AS PageName_3,
      NEXT(PageName, 3, true)
         OVER(PARTITION BY VisitorID, session.num
              ORDER BY timestamp
              ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
        AS PageName_4,
      NEXT(PageName, 4, true)
         OVER(PARTITION BY VisitorID, session.num
              ORDER BY timestamp
              ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING).value
        AS PageName_5,
      PageViews,
      session.depth AS SessionPageDepth
    FROM
      (SELECT
        endUserIds._experience.aaid.id as VisitorID,
        timestamp,
        web.webPageDetails.pageviews.value AS PageViews,
        web.webPageDetails.name AS PageName,
        SESS_TIMEOUT(timestamp, 60 * 30) 
          OVER (PARTITION BY endUserIDs._experience.aaid.id 
                ORDER BY timestamp 
                ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
        AS session
      FROM your_analytics_table
      WHERE TIMESTAMP >= to_timestamp('2018-12-01') AND TIMESTAMP <= to_timestamp('2018-12-31')
    )
  WHERE SessionPageDepth=1
  GROUP BY PageName, PageName_2, PageName_3, PageName_4, PageName_5
  ORDER BY PageViews DESC
  LIMIT 100;
```

![图像](../images/queries/adobe-functions/create-breakdown-report.png)

## Journey Orchestration

以下视频演示如何在Adobe Experience Platform接口和PSQL客户端中运行查询。 此外，视频还使用涉及XDM对象中各个属性的示例，使用Adobe定义的函数，以及使用CREATE TABLE AS SELECT(CTAS)。

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)


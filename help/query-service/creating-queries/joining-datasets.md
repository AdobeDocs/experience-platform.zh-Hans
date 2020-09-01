---
keywords: Experience Platform;home;popular topics;query service;Query service;joining datasets;joining dataset;
solution: Experience Platform
title: 加入数据集
topic: queries
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '53'
ht-degree: 3%

---


# 加入数据集

加入数据集后，您可以将来自查询中其他数据集的数据包含进来。 此示例使用自定义操作系统数据集将 `operatingsystemID` 该值映 `operatingsystem` 射到。

数据集:
- your_analytics_table
- custom_operating_system_lookup

按页 `SELECT` 面视图数为前50个操作系统创建一个语句。

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE _ACP_YEAR=2018 
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

![图像](../images/queries/joining-datasets/select-operating-systems.png)
---
keywords: Experience Platform;home;popular topics;query service;Query service;joining datasets;joining dataset;
solution: Experience Platform
title: 加入数据集
topic: queries
type: Tutorial
description: 加入数据集后，您可以将来自查询中其他数据集的数据包含进来。 此示例使用自定义操作系统数据集将操作系统ID映射到操作系统值。
translation-type: tm+mt
source-git-commit: 37356db1666b0c800119b1e254940ad72550848a
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 2%

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
WHERE TIMESTAMP >= ('2018-01-01') AND TIMESTAMP <= ('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

![图像](../images/queries/joining-datasets/select-operating-systems.png)
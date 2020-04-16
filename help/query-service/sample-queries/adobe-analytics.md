---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 示例查询
topic: queries
translation-type: tm+mt
source-git-commit: 2f0f155beacbc6a4ba2892ae211a9c0305e969ac

---


# Adobe Analytics数据的示例查询

来自选定Adobe Analytics报告套件的数据将转换为XDM ExperienceEvents，并作为数据集引入Adobe Experience Platform。 本文档概述了Adobe Experience Platform查询服务利用这些数据的许多使用案例，其中包含的示例查询应与您的Adobe Analytics数据集结合使用。 有关映射 [到XDM ExperienceEvents的更多信息](../../sources/connectors/adobe-applications/analytics-mapping.md) ，请参阅Analytics字段映射文档。

## 入门指南

本文档中的SQL示例要求您编辑SQL并根据您感兴趣的评估数据集、eVar、事件或时间范围为查询填写预期参数。 在随后的SQL示例 `{ }` 中，随时提供参数。

## 常用SQL示例

### 给定日的每小时访客计数

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {target_table}
WHERE _acp_year = {target_year} 
      AND _acp_month = {target_month}  
      AND _acp_day = {target_day}
GROUP BY Day, Hour
ORDER BY Hour;
```

### 指定日期前10个查看页面

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### 最活跃的10大用户

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### 按用户活动列出的10大城市

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### 10大查看产品

```sql
SELECT Product_SKU,
       Sum(Product_Views) AS Total_Product_Views
FROM  (SELECT Explode(productlistitems.sku) AS Product_SKU, 
              commerce.productviews.value   AS Product_Views 
       FROM   {target_table}
       WHERE  _acp_year = {target_year}
              AND _acp_month = {target_month}
              AND _acp_day = {target_day}
              AND commerce.productviews.value IS NOT NULL) 
GROUP BY Product_SKU 
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### 前10大订单收入

```sql
SELECT Purchase_ID, 
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue 
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID, 
               Explode(productlistitems)   AS Product_Items 
        FROM   {target_table} 
        WHERE  commerce.`order`.purchaseid IS NOT NULL 
               AND _acp_year = {target_year} 
               AND _acp_month = {target_month}  
               AND _acp_day = {target_day}) 
GROUP BY Purchase_ID 
ORDER BY total_order_revenue DESC 
LIMIT  10;
```

### 事件按日计数

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{target_event}.value) AS Event_Count
FROM   {target_table}
WHERE  _experience.analytics.event1to100.{target_event}.value IS NOT NULL 
        AND _acp_year = {target_year} 
        AND _acp_month = {target_month}  
        AND _acp_day = {target_day}
GROUP BY Day, Hour
ORDER BY Hour;
```

## 销售变量（产品语法）

在Adobe Analytics中，可以通过称为“销售变量”的特殊配置变量收集自定义产品级数据。 这些事件基于eVar或自定义变量。 这些变量与其标准用法的区别在于，它们代表在点击中找到的每个产品的单独值，而不是仅代表点击的单个值。 这些变量称为产品语法销售变量。 这允许在客户的搜索结果中收集每个产品的“折扣额”或有关产品“页面位置”的信息。

以下是用于访问Analytics数据集中的销售变量的XDM字段：

### eVar

```
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

其中 `[#]` 是数组索引， `evar#` 是特定的eVar变量。

### 自定义事件

```
productListItems[#]._experience.analytics.event1to100.event#.value
```

其中 `[#]` 是数组索引， `event#` 是特定的自定义事件变量。

### 示例查询

以下是返回销售eVar的示例查询，以及中找到的第一个产品的事件 `productListItems`。

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE _ACP_YEAR=2019 AND _ACP_MONTH=7 AND _ACP_DAY=23
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

下一个查询“爆炸”每个 `productListItems` 商品的eVar和事件，并返回每个产品。 该字 `_id` 段包含在内，用于显示与原始点击的关系。 该 `_id` 值是ExperienceEvent数据集中唯一的主键。

```sql
SELECT
  _id,
  productItem._experience.analytics.customDimensions.evars.eVar1,
  productItem._experience.analytics.event1to100.event1.value
FROM (
  SELECT
    _id,
    explode(productListItems) as productItem
  FROM adobe_analytics_midvalues
  WHERE _ACP_YEAR=2019 AND _ACP_MONTH=7 AND _ACP_DAY=23
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

### 实施示例查询时的常见错误

当您尝试检索当前数据集中不存在的字段时，会遇到“No suct field”（无此类结构字段）错误。 评估错误消息中返回的原因以标识可用字段，然后更新查询并重新运行。

```
ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
```

## 销售变量（转换语法）

在Adobe Analytics中找到的另一个类型是“转化语法”。 使用产品语法时，值会与产品同时收集，但这要求数据出现在同一页面上。 某些情况下，在与产品相关的转换或兴趣事件之前，数据会出现在页面上。 例如，考虑“产品查找方法”报告用例。

1. 用户对“winter hat”执行内部搜索，将启用“转换语法”的“销售eVar6”设置为“内部搜索：winter hat”
2. 用户单击“华夫饼”并登录到产品详细信息页面。\
   a.在这里登陆，就 `Product View` 会以12.99美元的价格，为“华夫饼豆”卖事件。\
   b.由于 `Product View` 被配置为绑定事件，因此产品“华夫饼”现在绑定到“internal search:winter hat”的eVar6值。 收集“华夫饼”产品后，它将与“内部搜索：温特帽”关联，直到(1)达到到期设置或(2)设置新的eVar6值并再次与该产品发生绑定事件。
3. 用户将产品添加到其购物车，并触发 `Cart Add` 事件。
4. 用户对“夏季衬衫”执行另一次内部搜索，该搜索将启用“转换语法”的“销售eVar6”设置为“内部搜索：夏季衬衫”
5. 用户单击“sporty t-shirt”并登录到产品详细信息页面。\
   a.在这里登陆， `Product View` 事件上写着“运动T恤，售价19.99美元”。\
   b.该事件 `Product View` 仍是我们的绑定事件，因此现在，产品“sporty t-shirt”与“internal search:summer shirt”的eVar6值绑定，而先前产品“华夫饼”仍与“internal search:waffle beanie”的eVar6值绑定。
6. 用户将产品添加到其购物车，并触发 `Cart Add` 事件。
7. 用户将注销这两个产品。

在报告中，订单、收入、产品视图和购物车加货将针对eVar6进行报告，并与绑定产品的活动保持一致。

| eVar6（产品查找方法） | 收入 | 订单 | 产品视图 | 购物车加货 |
|---|---|---|---|---|
| 内部搜索：夏季衬衫 | 19.99 | 1 | 1 | 1 |
| 内部搜索：冬帽 | 12.99 | 1 | 1 | 1 |

以下是在Analytics数据集中生成“转换语法”的XDM字段：

### eVar

```
_experience.analytics.customDimensions.evars.evar#
```

其中 `evar#` 是特定eVar变量。

### 产品

```
productListItems[#].sku
```

其中 `[#]` 是数组索引。

### 示例查询

此处是将值绑定到特定产品和事件对的示例查询，在此示例中为产品视图事件。

```sql
SELECT
  endUserIds._experience.aaid.id AS AAID,
  timestamp,
  CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
  OVER(PARTITION BY endUserIds._experience.aaid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
  END AS eVar1Bind,
  EXPLODE(productListItems) AS Product_List,
  commerce.productViews.value AS prodView,
  commerce.purchases.value AS purchase
FROM adobe_analytics_midvalues
WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
LIMIT 100
```

下面是一个示例查询，它将绑定值保持到相应产品的后续出现。 最低子查询在所声明的绑定事件上建立与产品的值关系。 下一个子查询在与相应产品的后续交互中执行该绑定值的归因。 顶级选择聚合结果以生成报告。

```sql
SELECT
  Product_List.SKU,
  eVar1101ConversionSyntax,
  SUM(prodView) AS Product_Views,
  SUM(purchase) AS Purchases
FROM
(
  SELECT
    Product_List,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'ConversionSyntax_eVar1', eVar1Bind)
      OVER(PARTITION BY AAID, Product_List.SKU
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
    AS eVar1ConversionSyntax,
    prodView,
    purchase
  FROM
  (
    SELECT
      endUserIds._experience.aaid.id AS AAID,
      timestamp,
      CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
      END AS eVar1Bind,
      EXPLODE(productListItems) AS Product_List,
      commerce.productViews.value AS prodView,
      commerce.purchases.value AS purchase
    FROM adobe_analytics_midvalues
    WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
  )
)
WHERE eVar1ConversionSyntax IS NOT NULL
GROUP BY 1, 2
ORDER BY 3 DESC
LIMIT 100
```

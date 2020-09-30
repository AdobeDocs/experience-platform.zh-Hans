---
keywords: Experience Platform;home;popular topics;query service;Query service;sample queries;sample query;adobe analytics;
solution: Experience Platform
title: 示例查询
topic: queries
description: 来自选定Adobe Analytics报告套件的数据将转换为XDM ExperienceEvents并作为数据集引入Adobe Experience Platform。 此文档概括了Adobe Experience Platform查询服务利用此数据的许多用例，其中包含的示例查询应与您的Adobe Analytics数据集配合使用。
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 1%

---


# Adobe Analytics数据查询示例

来自选定Adobe Analytics报告套件的数据将转换为XDM [!DNL ExperienceEvents] 并作为数据集引入Adobe Experience Platform。 此文档概括了Adobe Experience Platform利用此数据的 [!DNL Query Service] 许多用例，其中包含的示例查询应与您的Adobe Analytics数据集配合使用。 有关映射 [到XDM的更多信息](../../sources/connectors/adobe-applications/mapping/analytics.md) ，请参阅Analytics字段映射文档 [!DNL ExperienceEvents]。

## 入门指南

此文档中的SQL示例要求您编辑SQL，并根据您想要评估的数据集、eVar、事件或时间范围为查询填写预期参数。 在后面的SQL示例 `{ }` 中提供参数。

## 常用SQL示例

### 给定日的每小时访客计数

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### 给定一天内查看的前10个页面

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### 最活跃的10大用户

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### 按用户划分的十大城市活动

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
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
            WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
              AND commerce.productviews.value IS NOT NULL) 
GROUP BY Product_SKU 
ORDER BY Total_Product_Views DESC
LIMIT  10;
```

### 前10个订单总收入

```sql
SELECT Purchase_ID, 
       Round(Sum(Product_Items.priceTotal * Product_Items.quantity), 2) AS Total_Order_Revenue 
FROM   (SELECT commerce.`order`.purchaseid AS Purchase_ID, 
               Explode(productlistitems)   AS Product_Items 
        FROM   {target_table} 
        WHERE  commerce.`order`.purchaseid IS NOT NULL 
                AND TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')

GROUP BY Purchase_ID 
ORDER BY total_order_revenue DESC 
LIMIT  10;
```

### 事件数（按日）

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{target_event}.value) AS Event_Count
FROM   {target_table}
WHERE  _experience.analytics.event1to100.{target_event}.value IS NOT NULL 
        AND TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY Day, Hour
ORDER BY Hour;
```

## 销售变量（产品语法）

在Adobe Analytics，可通过称为“销售变量”的特殊配置变量收集定制产品级数据。 这些eVar或自定义事件。 这些变量与其标准用途的不同之处在于它们代表在点击中找到的每个产品的单独值，而不是只代表点击的单个值。 这些变量称为产品语法推销变量。 这允许在客户的搜索结果中收集每个产品的“折扣额”或产品的“页面位置”等信息。

以下是用于访问数据集中销售变量的XDM [!DNL Analytics] 字段：

### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

其中 `[#]` 是数组索引， `evar#` 是特定的eVar变量。

### 自定义事件

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

其中 `[#]` 是数组索引， `event#` 是特定的自定义事件变量。

### 示例查询

以下是示例查询，返回在中找到的第一个产品的销售eVar和事件 `productListItems`。

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE timestamp = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

下一个查询“爆炸” `productListItems` 并返回每个产品的销售eVar和事件。 该 `_id` 字段用于显示与原始点击的关系。 该 `_id` 值是数据集中唯一的主键 [!DNL ExperienceEvent] 。

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
  WHERE TIMESTAMP = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

### 实施示例查询时的常见错误

当您尝试检索当前数据集中不存在的字段时，会遇到“无此类结构字段”错误。 评估错误消息中返回的原因以标识可用字段，然后更新查询并重新运行。

```console
ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
```

## 销售变量（转换语法）

在Adobe Analytics找到的另一种类型推销变量是转换语法。 使用产品语法时，值会与产品同时收集，但这要求数据出现在同一页面上。 在转换或事件与产品相关的兴趣之前，会在页面上发生数据。 例如，考虑“产品查找方法”报告用例。

1. 用户执行“winter hat”的内部搜索，将启用“转换语法”的“推销eVar6”设置为“内部搜索：winter hat”
2. 用户单击“华夫饼”并登录产品详细信息页面。\
   a.在这里登陆， `Product View` 以12.99美元的价格事件“华夫饼豆”。\
   b.由于 `Product View` 已配置为绑定事件，因此产品“华夫饼”现在绑定到“内部搜索：冬季帽”的eVar6值。 收集“华夫饼”产品后，它将与“内部搜索：冬季帽子”关联，直到(1)达到到期设置或(2)设置新eVar6值，并再次对该产品发生绑定事件。
3. 用户将产品添加到购物车，并触发 `Cart Add` 事件。
4. 用户对“夏季衬衫”执行另一个内部搜索，该搜索将启用“转换语法”的“推销eVar6”设置为“内部搜索：夏季衬衫”
5. 用户单击“sporty t-shirt”并登录产品详细信息页面。\
   a.登陆这里， `Product View` 事件上的T恤售价19.99美元。\
   b.事件 `Product View` 仍是我们的有约束力的事件，因此现在，产品“sporty T-shirt”与“内部搜索：夏季衬衫”的eVar6价值相绑定，而前一产品“华夫燕”仍与“内部搜索：华夫燕”的eVar6价值相绑定。
6. 用户将产品添加到购物车，并触发 `Cart Add` 事件。
7. 用户签出这两种产品。

在报告中，订单、收入、产品视图和购物车添加将根据eVar6进行报告，并与绑定产品的活动保持一致。

| eVar6（产品查找方法） | 收入 | 订单 | 产品视图 | 购物车 |
|---|---|---|---|---|
| 内部搜索：夏季衬衫 | 19.99 | 1 | 1 | 1 |
| 内部搜索：冬季帽 | 12.99 | 1 | 1 | 1 |

以下是要在数据集中生成“转换语法”的XDM [!DNL Analytics] 字段：

### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

其中 `evar#` 是特定eVar变量。

### 产品

```console
productListItems[#].sku
```

数组 `[#]` 索引的位置。

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

以下是将绑定值保持到相应产品后续出现的示例查询。 最低子查询在所声明的绑定事件上建立与产品的值关系。 下一个子查询在与相应产品的后续交互中执行该绑定值的归因。 顶层选择聚合结果以生成报告。

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

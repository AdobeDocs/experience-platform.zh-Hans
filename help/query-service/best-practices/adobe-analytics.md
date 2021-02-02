---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；示例查询；示例查询;adobe分析；
solution: Experience Platform
title: 示例查询
topic: queries
description: 来自选定Adobe Analytics报告套件的数据将转换为XDM ExperienceEvents并作为数据集引入Adobe Experience Platform。 此文档概括了Adobe Experience Platform查询服务利用此数据的许多用例，其中包含的示例查询应与您的Adobe Analytics数据集配合使用。
translation-type: tm+mt
source-git-commit: e2c648829bb3268ab319da934f5cc6cc811290b3
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 1%

---


# Adobe Analytics数据查询示例

来自选定Adobe Analytics报告套组的数据被转换为符合[!DNL XDM ExperienceEvent]类的数据，并作为数据集被引入Adobe Experience Platform。

此文档概括了Adobe Experience Platform[!DNL Query Service]利用此数据的许多用例，包括示例查询应使用您的Adobe Analytics数据集。 有关映射到[!DNL Experience Events]的详细信息，请参阅[分析字段映射](../../sources/connectors/adobe-applications/mapping/analytics.md)上的文档。

## 入门指南

此文档中的SQL示例要求您编辑SQL，并根据您想要评估的数据集、eVar、事件或时间范围为查询填写预期参数。 在后面的SQL示例中，提供您看到`{ }`的任何位置的参数。

## 常用SQL示例

以下示例显示了常用的SQL查询来分析您的Adobe Analytics数据。

### 给定日的每小时访客计数

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day,
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Count(DISTINCT enduserids._experience.aaid.id) AS Visitor_Count 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

### 给定一天内查看的前10个页面

```sql
SELECT web.webpagedetails.name AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY web.webpagedetails.name 
ORDER BY page_views DESC 
LIMIT  10;
```

### 最活跃的10大用户

```sql
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY enduserids._experience.aaid.id
ORDER BY Count DESC
LIMIT  10;
```

### 按用户划分的十大城市活动

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
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
       FROM   {TARGET_TABLE}
            WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
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
        FROM   {TARGET_TABLE} 
        WHERE  commerce.`order`.purchaseid IS NOT NULL 
                AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')

GROUP BY Purchase_ID 
ORDER BY total_order_revenue DESC 
LIMIT  10;
```

### 事件数（按日）

```sql
SELECT Substring(from_utc_timestamp(timestamp, 'America/New_York'), 1, 10) AS Day, 
       Substring(from_utc_timestamp(timestamp, 'America/New_York'), 12, 2) AS Hour, 
       Sum(_experience.analytics.event1to100.{TARGET_EVENT}.value) AS Event_Count
FROM   {TARGET_TABLE}
WHERE  _experience.analytics.event1to100.{TARGET_EVENT}.value IS NOT NULL 
        AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY Day, Hour
ORDER BY Hour;
```

## 销售变量（产品语法）


### 产品语法

在Adobe Analytics，可通过称为销售变量的专门配置变量收集定制产品级数据。 这些eVar或自定义事件。 这些变量与其标准用途的不同之处在于它们代表在点击中找到的每个产品的单独值，而不是只代表点击的单个值。

这些变量称为产品语法推销变量。 这允许收集信息，如每个产品的“折扣额”或客户搜索结果中有关产品“页面位置”的信息。

要了解有关使用产品语法的更多信息，请阅读有关使用产品语法](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax)实现eVar的Adobe Analytics文档。[

以下各节概述访问[!DNL Analytics]数据集中的销售变量所需的XDM字段：

#### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`:您访问的数组的索引。
- `evar#`:您正在访问的特定eVar变量。

#### 自定义事件

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`:您访问的数组的索引。
- `event#`:您正在访问的特定自定义事件变量。

#### 示例查询

以下是示例查询，返回`productListItems`中第一个产品的销售eVar和事件。

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

下一个查询将爆炸`productListItems`阵列，并返回每个产品的每个销售eVar和事件。 包含`_id`字段以显示与原始点击的关系。 `_id`值是数据集的唯一主键。

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

>[!NOTE]
>
> 如果尝试检索当前数据集中不存在的字段，将发生“No suck struct field”（无此类结构字段）错误。 评估错误消息中返回的原因以标识可用字段，然后更新查询并重新运行。
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### 转换语法

在Adobe Analytics找到的另一种推销变量是转换语法。 使用产品语法时，值会与产品同时收集，但这要求数据出现在同一页面上。 在转换或事件与产品相关的兴趣之前，会在页面上发生数据。 例如，考虑产品查找方法的用例。

1. 用户执行“winter hat”的内部搜索，将启用“转换语法”的“推销eVar6”设置为“内部搜索：winter hat”
2. 用户单击“华夫饼”并登录产品详细信息页面。\
   a.降落在这里，以12.99美元的价格点燃了一个`Product View`的“华夫饼”事件。\
   b.由于`Product View`被配置为绑定事件，因此产品“华夫饼”现在绑定到“internal search:winter hat”的eVar6值。 收集“华夫饼”产品后，它将与“内部搜索：冬季帽子”关联，直到(1)达到到期设置或(2)设置新eVar6值，并再次对该产品发生绑定事件。
3. 用户将产品添加到购物车中，并触发`Cart Add`事件。
4. 用户对“夏季衬衫”执行另一个内部搜索，该搜索将启用“转换语法”的“推销eVar6”设置为“内部搜索：夏季衬衫”
5. 用户单击“sporty t-shirt”并登录产品详细信息页面。\
   a.登陆此处将以每件19.99美元的“运动T恤”的`Product View`事件点燃。\
   b.`Product View`事件仍是我们的绑定事件，因此现在产品“sporty t-shirt”与“internal search:summer shirt”的eVar6值绑定，而先前产品“华夫饼”仍与“internal search:waffle beanie”的eVar6值绑定。
6. 用户将产品添加到购物车中，并触发`Cart Add`事件。
7. 用户签出这两种产品。

在报告中，订单、收入、产品视图和购物车添加将根据eVar6进行报告，并与绑定产品的活动保持一致。

| eVar6（产品查找方法） | 收入 | 订单 | 产品视图 | 购物车 |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| 内部搜索：夏季衬衫 | 19.99 | 1 | 3 | 1 |
| 内部搜索：冬季帽 | 12.99 | 1 | 1 | 1 |

要进一步了解如何使用转换语法，请阅读有关使用转换语法](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax)实现eVar的Adobe Analytics文档。[

以下是要在[!DNL Analytics]数据集中生成转换语法的XDM字段：

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`:您正在访问的特定eVar变量。

#### 产品

```console
productListItems[#].sku
```

- `#`:您访问的数组的索引。

#### 示例查询

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

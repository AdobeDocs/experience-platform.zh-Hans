---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；示例查询；示例查询;adobe analytics;
solution: Experience Platform
title: Adobe Analytics数据查询示例
topic-legacy: queries
description: 来自选定Adobe Analytics报表包的数据将转换为XDM ExperienceEvents并作为数据集引入Adobe Experience Platform。 本文档概述了Adobe Experience Platform 查询 Service利用此数据的许多用例，其中包含的示例查询应与您的Adobe Analytics数据集一起使用。
exl-id: 96da3713-c7ab-41b3-9a9d-397756d9dd07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 1%

---

# Adobe Analytics数据的示例查询

来自选定Adobe Analytics报表包的数据将转换为符合[!DNL XDM ExperienceEvent]类的数据并作为数据集引入Adobe Experience Platform。

本文档概述了Adobe Experience Platform [!DNL Query Service]利用此数据(包括示例查询应使用您的Adobe Analytics数据集)的许多用例。 有关映射到[!DNL Experience Events]的详细信息，请参阅[分析字段映射](../../sources/connectors/adobe-applications/mapping/analytics.md)上的文档。

## 入门指南

本文档中的SQL示例要求您编辑SQL，并根据您有兴趣评估的数据集、eVar、事件或时间范围，为查询填写预期参数。 在后面的SQL示例中显示`{ }`时提供参数。

## 常用SQL示例

以下示例显示了分析Adobe Analytics数据时常用的SQL查询。

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

### 指定日期前10个查看页面

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

### 按用户划分的10大城市活动

```sql
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp) AS Count
FROM   {TARGET_TABLE}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
GROUP BY state_city
ORDER BY Count DESC
LIMIT  10;
```

### 查看次数最多的10种产品

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

### 前10大订单收入

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

### 事件数

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

在Adobe Analytics中，可通过称为促销变量的专门配置变量来收集自定义产品级别数据。 这些属性基于eVar或自定义事件。 这些变量与其标准用途的不同之处在于它们代表点击上找到的每个产品的单独值，而不是仅代表点击的单个值。

这些变量称为产品语法促销变量。 这允许收集信息，例如每个产品的“折扣额”或客户搜索结果中有关产品“页面位置”的信息。

要了解有关使用产品语法的更多信息，请阅读有关使用产品语法](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax)实现eVar的Adobe Analytics文档。[

以下各节概述了访问[!DNL Analytics]数据集中的促销变量所需的XDM字段：

#### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`:您访问的数组的索引。
- `evar#`:您访问的特定eVar变量。

#### 自定义事件

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`:您访问的数组的索引。
- `event#`:您访问的特定自定义事件变量。

#### 示例查询

以下是一个示例查询，它返回`productListItems`中找到的第一个产品的销售eVar和事件。

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

下一个查询将分解`productListItems`阵列，并返回每个产品的每个销售eVar和事件。 包含`_id`字段以显示与原始点击的关系。 `_id`值是数据集的唯一主键。

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
> 如果尝试检索当前数据集中不存在的字段，将出现“No suck struct field”（无此类结构字段）错误。 评估错误消息中返回的原因以标识可用字段，然后更新查询并重新运行。
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### 转换语法

在Adobe Analytics中找到的另一种类型的促销变量是转换语法。 对于产品语法，值是在收集产品的同时收集的，但这要求数据在同一页面上存在。 在转换或事件与产品相关的兴趣之前，会在页面上发生数据。 例如，考虑产品查找方法的用例。

1. 用户对“winter hat”执行内部搜索，将启用“转换语法”的“促销eVar6”设置为“内部搜索：winter hat”
2. 用户单击“华夫饼”，然后进入产品详细信息页面。\
   a.Landing here以12.99美元的价格，在`Product View`事件上放“华夫饼”。\
   b.由于`Product View`配置为绑定事件，因此产品“waffle beanie”现在绑定到“internal search:winter hat”的eVar6值。 无论何时收集“华夫饼豆”产品，它都将与“内部搜索：冬天帽子”关联，直到(1)达到过期设置或(2)设置新eVar6值并再次对该产品发生绑定事件。
3. 用户将产品添加到其购物车中，并触发`Cart Add`事件。
4. 用户对“夏季衬衫”执行另一个内部搜索，将启用“转换语法”的“促销eVar6”设置为“内部搜索：夏季衬衫”
5. 用户单击“sporty t-shirt”，然后进入产品详细信息页面。\
   a.Landing here将一个`Product View`事件的“sporty T-shirt，售价19.99美元。\
   b.`Product View`事件仍是我们的有约束力的事件，因此现在，产品“sporty t-shirt”与“internal search:summer shirt”的eVar6值相绑定，而上一产品“华夫饼”仍与“internal search:waffle beanie”的eVar6值相绑定。
6. 用户将产品添加到其购物车中，并触发`Cart Add`事件。
7. 用户签出这两个产品。

在报告中，订单、收入、产品视图和购物车添加将针对eVar6进行报告，并与绑定产品的活动一致。

| eVar6（产品查找方法） | 收入 | 订单 | 产品视图 | 购物 |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| 内部搜索：夏令时衬衫 | 19.99 | 1 | 1 | 3 |
| 内部搜索：冬帽 | 12.99 | 1 | 1 | 1 |

要了解有关使用转换语法的更多信息，请阅读有关使用转换语法](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax)实现eVar的Adobe Analytics文档。[

以下是用于在[!DNL Analytics]数据集中生成转换语法的XDM字段：

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`:您访问的特定eVar变量。

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

以下是将绑定值保持到相应产品后续出现的示例查询。 最低子查询在所声明的绑定事件上建立与产品的值关系。 下一个子查询在后续与相应产品的交互中执行该绑定值的归因。 顶层选择聚合结果以生成报告。

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

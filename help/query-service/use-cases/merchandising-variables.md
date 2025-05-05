---
title: 从Analytics数据返回和使用促销变量
description: 了解如何提供XDM字段和示例查询来访问Analytics数据集中的促销变量。
exl-id: 1e2ae095-4152-446f-8b66-dae5512d690e
source-git-commit: 7cde32f841497edca7de0c995cc4c14501206b1a
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 1%

---

# 从Analytics数据返回和使用促销变量

使用查询服务可将从Adobe Analytics引入到Adobe Experience Platform的数据作为数据集进行管理。 以下部分提供了可用于访问Analytics数据集中的促销变量的示例查询。 请参阅文档，了解有关[如何通过Analytics源摄取和映射Adobe Analytics数据](../../sources/connectors/adobe-applications/mapping/analytics.md)的更多信息

## 促销变量 {#merchandising-variables}

促销变量可以遵循以下两种语法之一：

* **产品语法**：将eVar值与产品关联。 
* **转化变量语法**：仅在发生捆绑事件时才将eVar与产品关联。 您可以选择充当捆绑事件的事件。

## 产品语法 {#product-syntax}

在Adobe Analytics中，可通过专门配置的变量（称为促销变量）收集自定义产品级数据。 这些事件基于eVar或自定义事件。 这些变量及其典型用法的区别在于，它们表示在点击中找到的每个产品的单独值，而不是点击的单个值。

这些变量称为产品语法促销变量。 这允许收集信息，如按产品“折扣金额”或有关客户搜索结果中产品“页面位置”的信息。

要了解有关使用产品语法的更多信息，请阅读有关[使用产品语法实施eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=zh-Hans#implement-using-product-syntax)的Adobe Analytics文档。

以下部分概述了访问[!DNL Analytics]数据集中的促销变量所需的XDM字段：

### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#`：您正在访问的数组的索引。
* `evar#`：您正在访问的特定eVar变量。

### 自定义事件

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#`：您正在访问的数组的索引。
* `event#`：您正在访问的特定自定义事件变量。

## 产品语法用例 {#product-use-cases}

以下用例侧重于使用SQL从`productListItems`数组返回推销eVar。

### 返回推销eVar和活动

以下查询返回在`productListItems`数组中找到的第一个产品的促销eVar和事件。

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

### 分解productListItems数组并返回每个产品的促销eVar和事件。

下一个查询将展开`productListItems`数组并返回每个产品的每个推销eVar和事件。 包含`_id`字段以显示与原始点击的关系。 `_id`值是数据集的唯一主键。

>[!NOTE]
>
>explode函数将一个数组的元素分成多行。 它不包括null值。

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
> 如果尝试检索的字段在当前数据集中不存在，则会出现“无此类结构字段”错误。 评估错误消息中返回的原因以确定可用字段，然后更新查询并重新运行它。
>
>```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### 转化变量语法 {#conversion-variable-syntax}

在Adobe Analytics中找到的另一种促销变量类型是转化变量语法。 当在products变量中无法设置eVar值时，可使用转化变量语法。 这种情况通常意味着您的页面没有促销渠道的上下文或查找方法。 在这些情况下，您应在用户到达产品页面之前设置促销变量，该值会持续到捆绑事件发生为止。

例如，下面的产品查找场景说明了在发生与产品相关的转化或事件之前，页面上如何显示所需的数据。

1. 用户执行“winter hat”的内部搜索，该搜索将启用推销eVar6的转化语法设置为“internal search：winter hat”。
2. 用户点击“华夫饼豆豆”并登陆产品详细信息页面。\
   a.登陆此处时为“华夫饼套头”触发了`Product View`活动，价格为$12.99美元。\
   b.由于`Product View`被配置为捆绑事件，产品“华夫饼套头”现在已捆绑到“内部搜索：冬季帽子”的eVar6值。 无论何时收集“华夫饼套头帽”产品，它都会与“内部搜索：冬季帽子”相关联。 此过程直到达到eVar到期设置为止，或者直到设置了新的eVar6值并且捆绑事件再次与该产品发生为止。
3. 用户将产品添加到购物车，并触发`Cart Add`事件。
4. 用户再次执行“summer shirt”的内部搜索，这将启用推销eVar6的转化语法设置为“internal search：summer shirt”。
5. 用户选择“运动T恤”并登陆产品详细信息页面。\
   a.登陆此处引发了`Product View`活动，“运动衫”售价19.99美元。\
   b.由于`Product View`事件是捆绑事件，产品“运动衫”现在捆绑到“内部搜索：夏季衬衫”的eVar6值。 先前产品“华夫饼套头”仍与“内部搜索：华夫饼套头”的eVar6值绑定。
6. 用户将产品添加到购物车，并触发`Cart Add`事件。
7. 用户会同时签出这两个产品。

在报表中，订单、收入、产品查看和购物车添加可根据eVar6报告，并与捆绑产品的活动一致。

| eVar6（产品查找方法） | 收入 | 订单 | 产品查看次数 | 购物车添加次数 |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| 内部搜索：summer shirt | 19.99 | 1 | 1 | 1 |
| 内部搜索：冬季帽子 | 12.99 | 1 | 1 | 1 |

要了解有关使用转化变量语法的更多信息，请阅读有关[使用转化变量语法实施eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=zh-Hans#implement-using-conversion-variable-syntax)的Adobe Analytics文档。

下面显示了在您的[!DNL Analytics]数据集中生成转化变量语法的XDM字段：

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#`：您正在访问的特定eVar变量。

#### 产品

```console
productListItems[#].sku
```

* `#`：您正在访问的数组的索引。

## 转化变量用例 {#conversion-variable-use-cases}

以下用例反映了需要转化变量语法的场景。

### 将值捆绑到特定的产品和事件对

下面的查询将该值捆绑到特定的产品和事件对。 在此示例中，值将捆绑到产品查看事件。

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

### 将捆绑值保留到相应产品的后续发生次数

下面的示例查询将绑定值保留到相应产品的后续发生次数。 最低子查询建立值与声明的捆绑事件上的产品的关系。 下一个子查询在与相应产品的后续交互中执行该绑定值的归因。 顶级SELECT将聚合结果以生成报表。

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

## 后续步骤

通过阅读本文档，您应该更好地了解如何使用产品语法返回推销eVar，并使用转化变量语法将值捆绑到特定产品。

如果您尚未这样做，则应该阅读下面的[Analytics Insights for Web and Mobile Interactions文档](./analytics-insights.md)。 它提供了常见用例，并演示了如何使用查询服务根据Web和移动Adobe Analytics数据创建切实可行的见解。

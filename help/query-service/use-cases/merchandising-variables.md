---
title: 从分析数据返回和使用促销变量
description: 了解如何提供XDM字段和示例查询以访问Analytics数据集中的促销变量。
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 4%

---

# 从分析数据返回并使用促销变量

使用查询服务管理从Adobe Analytics摄取到Adobe Experience Platform的数据，将这些数据作为数据集进行管理。 以下部分提供了可用于访问Analytics数据集中促销变量的示例查询。 有关 [如何摄取和映射Adobe Analytics数据](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/analytics.html?lang=zh-Hans) 通过Analytics源

## 促销变量 {#merchandising-variables}

促销变量可遵循以下两种语法之一：

* **产品语法**:将eVar值与产品关联。 
* **转化变量语法**:仅当发生捆绑事件时，才将eVar与产品关联。 您可以选择充当捆绑事件的事件。

## 产品语法 {#product-syntax}

在Adobe Analytics中，可通过专门配置的变量（称为促销变量）来收集自定义产品级数据。 这些事件基于eVar或自定义事件。 这些变量与其典型用法的不同之处在于，它们表示在点击中找到的每个产品的单独值，而不是仅表示点击的单个值。

这些变量称为产品语法推销变量。 这允许收集信息，如每个产品的“折扣金额”或客户搜索结果中有关产品“页面位置”的信息。

要了解有关使用产品语法的更多信息，请阅读Adobe Analytics文档(位于 [使用产品语法实施eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-product-syntax).

以下各节概述了访问 [!DNL Analytics] 数据集：

### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#`:要访问的数组的索引。
* `evar#`:您正在访问的特定eVar变量。

### 自定义事件

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#`:要访问的数组的索引。
* `event#`:您正在访问的特定自定义事件变量。

## 产品语法用例 {#product-use-cases}

以下用例重点介绍如何从 `productListItems` 数组。

### 返回促销eVar和事件

以下查询会返回在 `productListItems` 数组。

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

### 展开productListItems数组并返回每个产品的促销eVar和事件。

下一个查询将展开 `productListItems` 数组，并为每个产品返回每个促销eVar和事件。 的 `_id` 字段来显示与原始点击的关系。 的 `_id` 值是数据集的唯一主键。

>[!NOTE]
>
>分解函数将数组的元素分成多行。 它排除null值。

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
> 如果尝试检索当前数据集中不存在的字段，则会出现“无此类结构字段”错误。 评估错误消息中返回的原因以标识可用字段，然后更新查询并重新运行该查询。
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### 转化变量语法 {#conversion-variable-syntax}

在Adobe Analytics中找到的另一种类型的推销变量是转化变量语法。 当无法在产品变量中设置eVar值时，应使用转化变量语法。 这种情况通常意味着您的页面没有推销渠道的任何上下文或查找方法。在这些情况下，您应在用户到达产品页面之前设置推销变量，该值会一直保留到捆绑事件发生为止。

例如，下面的产品查找方案说明了在发生与产品相关的转化或事件之前，页面上如何显示所需数据。

1. 用户对“冬帽”执行内部搜索，该搜索将启用促销eVar6的转化语法设置为“内部搜索：冬帽”。
2. 用户单击“华夫饼”，然后登陆产品详细信息页面。\
   a.这里着陆会 `Product View` 花12.99美元举办“华夫饼豆”活动。\
   b.自 `Product View` 配置为捆绑事件，产品“华夫饼”现在绑定到“内部搜索：winter hat”的eVar6值。 无论何时收集“华夫饼豆”产品，都会与“内部搜索：冬帽”相关联。 在达到eVar过期设置或设置新eVar6值并再次与该产品发生捆绑事件之前，会一直执行此操作。
3. 用户将产品添加到购物车，并触发 `Cart Add` 事件。
4. 用户对“夏季衬衫”执行另一次内部搜索，该搜索将启用促销eVar6的转化语法设置为“内部搜索：夏季衬衫”。
5. 用户选择“sporty t-shirt”并登陆产品详细信息页面。\
   a.这里着陆会 `Product View` “sporty t-t-thirt”活动，售价19.99美元。\
   b.作为 `Product View` 事件是捆绑事件，产品“sporty t-shirt”现在绑定到“internal search:summer shirt”的eVar6值。 以前的产品“华夫饼”仍绑定到“内部搜索：华夫饼”的eVar6值。
6. 用户将产品添加到购物车，并触发 `Cart Add` 事件。
7. 用户签出了这两个产品。

在报表中，订单、收入、产品查看和购物车加货将根据eVar6进行报告，并与绑定产品的活动保持一致。

| eVar6（产品查找方法） | 收入 | 订购 | 产品查看 | 购物车加货 |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| 内部搜索：夏季衬衫 | 19.99 | 1 | 1 | 1 |
| 内部搜索：冬帽 | 12.99 | 1 | 1 | 1 |

要了解有关使用转化变量语法的更多信息，请阅读Adobe Analytics文档(位于 [使用转化变量语法实施eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-conversion-variable-syntax).

下面显示了用于在 [!DNL Analytics] 数据集：

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#`:您正在访问的特定eVar变量。

#### 产品

```console
productListItems[#].sku
```

* `#`:要访问的数组的索引。

## 转化变量用例 {#conversion-variable-use-cases}

以下用例反映了需要转化变量语法的情景。

### 将值绑定到特定的产品和事件对

以下查询将值绑定到特定的产品和事件对。 在此示例中，值绑定到产品查看事件。

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

### 将绑定值保留到相应产品的后续出现次数

下面的示例查询会将绑定值保留到相应产品的后续出现。 最低的子查询在声明的捆绑事件上建立值与产品的关系。 下一个子查询在与相应产品的后续交互中执行该绑定值的归因。 顶级SELECT汇总结果以生成报表。

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

通过阅读本文档，您应该更好地了解如何使用产品语法返回促销eVar，以及如何使用转化变量语法将值绑定到特定产品。

如果您尚未执行此操作，则应阅读 [针对Web和移动设备交互的分析文档](./analytics-insights.md) 下一个。 它提供了常见用例，并演示了如何使用查询服务从Web和移动Adobe Analytics数据创建可操作的分析。

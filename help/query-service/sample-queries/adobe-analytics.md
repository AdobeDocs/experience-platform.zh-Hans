---
keywords: Experience Platform；主页；热门主题；查询服务；查询服务；示例查询；示例查询；Adobe Analytics;
solution: Experience Platform
title: Adobe Analytics数据的查询示例
description: 来自选定Adobe Analytics报表包的数据将转换为XDM ExperienceEvents，并作为数据集摄取到Adobe Experience Platform。 本文档概述了查询服务利用此数据的许多用例，其中包括旨在与Adobe Analytics数据集结合使用的示例查询。
exl-id: 96da3713-c7ab-41b3-9a9d-397756d9dd07
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 1%

---

# Adobe Analytics数据查询示例

来自选定Adobe Analytics报表包的数据将转换为符合 [!DNL XDM ExperienceEvent] 类并作为数据集摄取到Adobe Experience Platform中。

本文档概述了Adobe Experience Platform [!DNL Query Service] 利用此数据。 请参阅 [Analytics字段映射](../../sources/connectors/adobe-applications/mapping/analytics.md) 有关映射到的详细信息 [!DNL Experience Events].

请参阅 [analytics用例文档](../use-cases/analytics-insights.md) 了解如何使用查询服务从摄取的Adobe Analytics数据创建可操作的分析。

## 重复数据删除

[!DNL Query Service] 支持重复数据删除。 请参阅 [中的重复数据删除 [!DNL Query Service] 文档](../best-practices/deduplication.md) 有关在查询时如何生成新值的信息 [!DNL Experience Event] 数据集。

## 促销变量（产品语法）

以下部分提供了XDM字段和示例查询，您可以使用它们来访问 [!DNL Analytics] 数据集。

### 产品语法

在Adobe Analytics中，可通过专门配置的变量（称为促销变量）来收集自定义产品级数据。 这些事件基于eVar或自定义事件。 这些变量与其典型用法的不同之处在于，它们表示在点击中找到的每个产品的单独值，而不是仅表示点击的单个值。

这些变量称为产品语法推销变量。 这允许收集信息，例如每个产品的“折扣金额”或客户搜索结果中有关产品“页面位置”的信息。

要了解有关使用产品语法的更多信息，请阅读Adobe Analytics文档(位于 [使用产品语法实施eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-product-syntax).

以下各节概述了访问 [!DNL Analytics] 数据集：

#### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

- `#`:要访问的数组的索引。
- `evar#`:您正在访问的特定eVar变量。

#### 自定义事件

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

- `#`:要访问的数组的索引。
- `event#`:您正在访问的特定自定义事件变量。

#### 示例查询

以下是一个示例查询，用于返回在 `productListItems`.

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

下一个查询将展开 `productListItems` 数组，并为每个产品返回每个促销eVar和事件。 的 `_id` 字段来显示与原始点击的关系。 的 `_id` 值是数据集的唯一主键。

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
> 如果尝试检索当前数据集中不存在的字段，则会出现“无此类结构字段”错误。 评估错误消息中返回的原因以标识可用字段，然后更新查询并重新运行。
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### 转化语法

在Adobe Analytics中找到的另一种类型的推销变量是转化语法。 使用产品语法时，会在收集值的同时收集产品，但这要求数据显示在同一页面上。 在某些情况下，数据会在与产品相关的转化或关注事件之前发生在页面上。 例如，请考虑产品查找方法的用例。

1. 用户执行和内部搜索“winter hat”，以将启用“转化语法”的促销eVar6设置为“内部搜索：winter hat”
2. 用户单击“华夫饼”，然后登陆产品详细信息页面。\
   a.这里着陆会 `Product View` 花12.99美元举办“华夫饼豆”活动。\
   b.自 `Product View` 配置为捆绑事件，产品“华夫饼”现在绑定到“内部搜索：winter hat”的eVar6值。 无论何时收集“华夫饼豆”产品，都会将其与“内部搜索：冬天帽”关联，直到(1)达到过期设置或(2)设置了新eVar6值，并且该产品再次发生捆绑事件。
3. 用户将产品添加到购物车，并触发 `Cart Add` 事件。
4. 用户对“夏季衬衫”执行另一次内部搜索，该搜索会将启用“转化语法”的促销eVar6设置为“内部搜索：夏季衬衫”
5. 用户单击“sporty t-shirt”，然后登陆产品详细信息页面。\
   a.这里着陆会 `Product View` “sporty t-t-thirt”活动，售价19.99美元。\
   b.的 `Product View` 事件仍是我们的捆绑事件，因此现在产品“sporty t-shirt”已绑定到“internal search:summer shirt”的eVar6值，而上一产品“华夫饼燕”仍绑定到“internal search:waffle beanie”的eVar6值。
6. 用户将产品添加到购物车，并触发 `Cart Add` 事件。
7. 用户签出了这两个产品。

在报表中，订单、收入、产品查看和购物车加货将针对eVar6进行报告，并与绑定产品的活动保持一致。

| eVar6（产品查找方法） | 收入 | 订购 | 产品查看 | 购物车加货 |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| 内部搜索：夏季衬衫 | 19.99 | 1 | 1 | 1 |
| 内部搜索：冬帽 | 12.99 | 1 | 1 | 1 |

要了解有关使用转化语法的更多信息，请阅读Adobe Analytics文档(位于 [使用转化语法实施eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html?lang=en#implement-using-conversion-variable-syntax).

以下是用于在 [!DNL Analytics] 数据集：

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

- `evar#`:您正在访问的特定eVar变量。

#### 产品

```console
productListItems[#].sku
```

- `#`:要访问的数组的索引。

#### 示例查询

以下是一个将值绑定到特定产品和事件对（在此例中为产品查看事件）的示例查询。

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

以下是一个示例查询，用于将绑定值保留到相应产品的后续发生次数。 最低的子查询在声明的捆绑事件上与产品建立值关系。 下一个子查询在与相应产品的后续交互中执行该绑定值的归因。 而顶级选择会聚合结果以生成报表。

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

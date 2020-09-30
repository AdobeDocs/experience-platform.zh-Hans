---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;aggregation functions;aggregation;
solution: Experience Platform
title: 聚合函数
topic: developer guide
description: '聚合函数用于将用户档案查询语言(PQL)阵列中的多个值组合在一起，以形成单个摘要值。 '
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 5%

---


# 聚合函数

聚合函数用于将(PQL)阵列中的多个 [!DNL Profile Query Language] 值组合在一起，以形成单个摘要值。 有关其他PQL功能的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md)。

## 计数

该函 `count` 数返回给定数组中的元素数。

**Format**

```sql
{ARRAY}.count()
```

**示例**

以下PQL查询返回阵列中的订单数。

```sql
orders.count()
```

## 总和

函 `sum` 数返回数组中所有选定值的和。

**Format**

```sql
{ARRAY}.sum()
```

**示例**

以下PQL查询返回所有订单价格的总和。

```sql
orders.sum(order.price)
```

## 平均

该函 `average` 数返回数组中所有选定值的算术平均值。

**Format**

```sql
{ARRAY}.average()
```

**示例**

以下PQL查询返回所有订单的平均价格。

```sql
orders.average(order.price)
```

## 最低

该函 `min` 数返回数组中所有选定值的最小值。

**Format**

```sql
{ARRAY}.min()
```

**示例**

以下PQL查询返回所有订单的最低价格。

```sql
orders.min(order.price)
```

## 最大值

该函 `max` 数返回数组中所有选定值中的最大值。

**Format**

```sql
{ARRAY}.max()
```

**示例**

以下PQL查询返回所有订单的最高价格。

```sql
orders.max(order.price)
```

## 后续步骤

您已经了解了聚合函数，现在可以在PQL查询中使用它们。 有关其他PQL功能的详细信息，请阅读 [用户档案查询语概述](./overview.md)。

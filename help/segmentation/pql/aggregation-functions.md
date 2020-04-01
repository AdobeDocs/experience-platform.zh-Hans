---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 聚合函数
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# 聚合函数

聚合函数用于将用户档案查询语言(PQL)数组中的多个值组合在一起，以形成单个摘要值。 有关其他PQL函数的更多信息，请参阅 [用户档案查询语言概述](./overview.md)。

## 计数

该函 `count` 数返回给定数组中的元素数。

**格式**

```sql
{ARRAY}.count()
```

**示例**

以下PQL查询返回数组中的订单数。

```sql
orders.count()
```

## 总和

该函 `sum` 数返回数组中所有选定值的总和。

**格式**

```sql
{ARRAY}.sum()
```

**示例**

以下PQL查询返回所有订单的价格总和。

```sql
orders.sum(order.price)
```

## 平均

该函 `average` 数返回数组中所有选定值的算术平均值。

**格式**

```sql
{ARRAY}.average()
```

**示例**

以下PQL查询返回所有订单的平均价格。

```sql
orders.average(order.price)
```

## 最低

该函 `min` 数返回数组中所有选定值中最小的值。

**格式**

```sql
{ARRAY}.min()
```

**示例**

以下PQL查询返回所有订单的最低价格。

```sql
orders.min(order.price)
```

## 最大值

该函 `max` 数返回数组中所有选定值中最大的值。

**格式**

```sql
{ARRAY}.max()
```

**示例**

以下PQL查询返回所有订单的最高价格。

```sql
orders.max(order.price)
```

## 后续步骤

现在您已经了解了聚合函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语概述](./overview.md)。

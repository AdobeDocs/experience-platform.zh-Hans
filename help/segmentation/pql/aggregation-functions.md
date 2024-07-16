---
solution: Experience Platform
title: PQL聚合函数
description: 聚合函数用于将Profile Query Language (PQL)数组中的多个值组合在一起，形成一个汇总值。
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 6%

---

# 聚合函数

聚合函数用于将[!DNL Profile Query Language] (PQL)数组中的多个值组合在一起，以形成单个摘要值。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## 计数

`count`函数返回给定数组中的元素数。

**格式**

```sql
{ARRAY}.count()
```

**示例**

以下PQL查询返回数组中的订单数。

```sql
orders.count()
```

## Sum

`sum`函数返回数组中所有选定值的总和。

**格式**

```sql
{ARRAY}.sum()
```

**示例**

以下PQL查询返回所有订单价格的总和。

```sql
orders.sum(order.price)
```

## 平均

`average`函数返回数组中所有选定值的算术平均值。

**格式**

```sql
{ARRAY}.average()
```

**示例**

以下PQL查询返回所有订单的平均价格。

```sql
orders.average(order.price)
```

## Minimum

`min`函数返回数组中所有选定值中的最小值。

**格式**

```sql
{ARRAY}.min()
```

**示例**

以下PQL查询返回所有订单的最低价格。

```sql
orders.min(order.price)
```

## Maximum

`max`函数返回数组中所有选定值中的最大值。

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

现在，您已了解聚合函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读[Profile Query Language概述](./overview.md)。

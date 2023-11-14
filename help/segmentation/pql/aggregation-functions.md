---
solution: Experience Platform
title: PQL聚合函数
description: 聚合函数用于将配置文件查询语言(PQL)数组中的多个值组合在一起，以形成单个摘要值。
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 6%

---

# 聚合函数

聚合函数用于将多个值分组到一起， [!DNL Profile Query Language] (PQL)数组以形成单个摘要值。 有关其他PQL函数的更多信息，请参见 [[!DNL Profile Query Language] 概述](./overview.md).

## 计数

此 `count` 函数返回给定数组中元素的数量。

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

此 `sum` 函数返回数组中所有选定值的总和。

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

此 `average` 函数返回数组中所有选定值的算术平均值。

**格式**

```sql
{ARRAY}.average()
```

**示例**

以下PQL查询返回所有订单的平均价格。

```sql
orders.average(order.price)
```

## 最小值

此 `min` 函数返回数组中所有选定值中的最小值。

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

此 `max` 函数返回数组中所有选定值中的最大值。

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

现在，您已了解聚合函数，可以在PQL查询中使用它们。 有关其他PQL功能的详细信息，请参阅 [配置文件查询语言概述](./overview.md).

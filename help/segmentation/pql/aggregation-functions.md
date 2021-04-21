---
keywords: Experience Platform；主题；热门主题；分段；分段；分段服务；pql;PQL;用户档案查询语；聚合函数；聚合；
solution: Experience Platform
title: PQL聚合函数
topic-legacy: developer guide
description: 聚合函数用于将用户档案查询语言(PQL)数组中的多个值组合在一起，以形成单个摘要值。
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 5%

---

# 聚合函数

聚合函数用于将[!DNL Profile Query Language](PQL)数组中的多个值组合在一起，以形成单个摘要值。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] overview](./overview.md)。

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

`sum`函数返回数组中所有选定值的和。

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

## 最低

`min`函数返回数组中所有选定值中最小值。

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

`max`函数返回数组中所有选定值中最大值。

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

现在，您已经了解了聚合函数，可以在PQL查询中使用它们。 有关其他PQL函数的详细信息，请阅读[用户档案查询语言概述](./overview.md)。

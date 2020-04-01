---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 算术函数
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# 算术函数

算术函数用于对用户档案查询语(PQL)中的值执行基本计算。 有关其他PQL函数的更多信息，请参阅 [用户档案查询语言概述](./overview.md)。

## Add

(addition) `+` 函数用于查找两个参数表达式的和。

**格式**

```sql
{NUMBER} + {NUMBER}
```

**示例**

以下PQL查询为两种不同产品的价格总和。

```sql
product1.price + product2.price
```

## 乘

( `*` 乘法)函数用于查找两个参数表达式的乘积。

**格式**

```sql
{NUMBER} * {NUMBER}
```

**示例**

以下PQL查询会查找库存产品和产品价格，以查找产品的总价值。

```sql
product.inventory * product.price
```

## 相减

用 `-` （减法）函数求两个参数表达式的差。

**格式**

```sql
{NUMBER} - {NUMBER}
```

**示例**

以下PQL查询可找出两个不同产品之间的价格差异。

```sql
product1.price - product2.price
```

## 除法

用 `/` （除）函数求两个参数表达式的商。

**格式**

```sql
{NUMBER} / {NUMBER}
```

**示例**

以下PQL查询将查找销售产品总数与收入总额之间的商数，以查看每个项目的平均成本。

```sql
totalProduct.price / totalProduct.sold
```

## 剩余

(modulo/ `%` remeard)函数用于在将两个参数表达式除以后查找余数。

**格式**

```sql
{NUMBER} % {NUMBER}
```

**示例**

以下PQL查询检查该人的年龄是否可被5整除。

```sql
person.age % 5 = 0
```

## 后续步骤

现在您已经学习了算术函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语概述](./overview.md)。

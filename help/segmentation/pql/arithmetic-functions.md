---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;arithmetic functions;arithmetic;
solution: Experience Platform
title: 算术函数
topic: developer guide
description: 算术函数用于对用户档案查询语言(PQL)中的值执行基本计算。
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 5%

---


# 算术函数

算术函数用于对(PQL)中的值执 [!DNL Profile Query Language] 行基本计算。 有关其他PQL功能的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md)。

## Add

( `+` addition)函数用于查找两个参数表达式的和。

**Format**

```sql
{NUMBER} + {NUMBER}
```

**示例**

以下PQL查询概括了两种不同产品的价格。

```sql
product1.price + product2.price
```

## 乘

( `*` multiplication)函数用于查找两个参数表达式的乘积。

**Format**

```sql
{NUMBER} * {NUMBER}
```

**示例**

以下PQL查询会查找库存的产品和产品的价格，以查找产品的总价值。

```sql
product.inventory * product.price
```

## 相减

利用 `-` （减法）函数来寻找两个参数表达式的差值。

**Format**

```sql
{NUMBER} - {NUMBER}
```

**示例**

以下PQL查询会查找两个不同产品之间的价格差异。

```sql
product1.price - product2.price
```

## 除法

用 `/` （除法）函数求两个参数表达式的商。

**Format**

```sql
{NUMBER} / {NUMBER}
```

**示例**

以下PQL查询将查找销售产品总额与收入总额之间的商数，以查看每个项目的平均成本。

```sql
totalProduct.price / totalProduct.sold
```

## 剩余

( `%` modulo/remainder)函数用于在将两个参数表达式除以后查找余数。

**Format**

```sql
{NUMBER} % {NUMBER}
```

**示例**

以下PQL查询检查人员的年龄是否可被五个人整除。

```sql
person.age % 5 = 0
```

## 后续步骤

您已经学习了算术函数，现在可以在PQL查询中使用它们。 有关其他PQL功能的详细信息，请阅读 [用户档案查询语概述](./overview.md)。

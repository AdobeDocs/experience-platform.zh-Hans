---
solution: Experience Platform
title: PAL算术函数
description: 算术函数用于对Profile Query Language (PQL)中的值执行基本计算。
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 3%

---

# 算术函数

算术函数用于对[!DNL Profile Query Language] (PQL)中的值执行基本计算。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## Add

`+` （相加）函数用于将两个参数表达式求和为数字。

**格式**

```sql
{NUMBER} + {NUMBER}
```

**示例**

下面的PQL查询汇总了两个不同产品的价格。

```sql
product1.price + product2.price
```

## 乘

`*` （乘法）函数用于将两个参数表达式的乘积作为数字。

**格式**

```sql
{NUMBER} * {NUMBER}
```

**示例**

以下PQL查询查找库存的产品和产品价格，以查找产品的总值。

```sql
product.inventory * product.price
```

## 减

`-`（减法）函数用于将两个参数表达式作为数字求差。

**格式**

```sql
{NUMBER} - {NUMBER}
```

**示例**

以下PQL查询查找两个不同产品之间的价格差异。

```sql
product1.price - product2.price
```

## 除

`/` （除法）函数用于将两个参数表达式的商作为数字进行查找。

**格式**

```sql
{NUMBER} / {NUMBER}
```

**示例**

以下PQL查询查找已售产品总数与已挣总金额之间的商数，以查看每个项目的平均成本。

```sql
totalProduct.price / totalProduct.sold
```

## 余数

`%` （模/余数）函数用于将两个参数表达式除以一个数字后求余数。

**格式**

```sql
{NUMBER} % {NUMBER}
```

**示例**

以下PQL查询检查人员的年龄是否可被5整除。

```sql
person.age % 5 = 0
```

## 后续步骤

现在，您已了解算术函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读[Profile Query Language概述](./overview.md)。

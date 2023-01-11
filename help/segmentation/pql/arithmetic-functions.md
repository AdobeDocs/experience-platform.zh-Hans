---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；PQL;PQL；用户档案查询语言；算术函数；算术；
solution: Experience Platform
title: PAL算术函数
description: 算术函数用于对用户档案查询语言(PQL)中的值执行基本计算。
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 5%

---

# 算术函数

算术函数用于对 [!DNL Profile Query Language] (PQL)。 有关其他PQL函数的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md).

## Add

的 `+` (addition)函数用于查找两个参数表达式的和。

**格式**

```sql
{NUMBER} + {NUMBER}
```

**示例**

以下PQL查询汇总了两个不同产品的价格。

```sql
product1.price + product2.price
```

## 乘

的 `*` （乘法）函数用于查找两个参数表达式的乘积。

**格式**

```sql
{NUMBER} * {NUMBER}
```

**示例**

以下PQL查询可查找库存产品和产品价格，以查找产品的总值。

```sql
product.inventory * product.price
```

## 减

的 `-` （减法）函数用于查找两个参数表达式的差。

**格式**

```sql
{NUMBER} - {NUMBER}
```

**示例**

以下PQL查询可查找两个不同产品之间的价格差异。

```sql
product1.price - product2.price
```

## 除数

的 `/` （除法）函数用于查找两个参数表达式的商。

**格式**

```sql
{NUMBER} / {NUMBER}
```

**示例**

以下PQL查询会查找已销售产品总数与所得总金额之间的商，以查看每项的平均成本。

```sql
totalProduct.price / totalProduct.sold
```

## 余数

的 `%` （模/余数）函数用于在将两个参数表达式除以后查找余数。

**格式**

```sql
{NUMBER} % {NUMBER}
```

**示例**

以下PQL查询检查人员的年龄是否可以被5除。

```sql
person.age % 5 = 0
```

## 后续步骤

现在，您已经了解了算术函数，接下来可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语言概述](./overview.md).

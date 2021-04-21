---
keywords: Experience Platform；主题；热门主题；分段；分段；分段服务；pql;PQL;用户档案查询语言；算术函数；算术；
solution: Experience Platform
title: PAL算术函数
topic-legacy: developer guide
description: 算术函数用于对用户档案查询语言(PQL)中的值执行基本计算。
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 5%

---

# 算术函数

算术函数用于对[!DNL Profile Query Language](PQL)中的值执行基本计算。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] overview](./overview.md)。

## Add

`+`(addition)函数用于查找两个参数表达式的和。

**格式**

```sql
{NUMBER} + {NUMBER}
```

**示例**

以下PQL查询概括了两种不同产品的价格。

```sql
product1.price + product2.price
```

## 乘

`*`（乘法）函数用于查找两个参数表达式的乘积。

**格式**

```sql
{NUMBER} * {NUMBER}
```

**示例**

以下PQL查询查找库存产品和产品价格以查找产品的总价值。

```sql
product.inventory * product.price
```

## 减

`-`（减法）函数用于查找两个参数表达式的差值。

**格式**

```sql
{NUMBER} - {NUMBER}
```

**示例**

以下PQL查询会查找两种不同产品之间的价格差异。

```sql
product1.price - product2.price
```

## 除法

`/`(division)函数用于查找两个参数表达式的商。

**格式**

```sql
{NUMBER} / {NUMBER}
```

**示例**

以下PQL查询将查找销售产品总数与查看每个项目的平均成本所赚总金额之间的商。

```sql
totalProduct.price / totalProduct.sold
```

## 剩余

`%`(modulo/remainer)函数用于在将两个参数表达式除以后查找余数。

**格式**

```sql
{NUMBER} % {NUMBER}
```

**示例**

以下PQL查询检查人员的年龄是否可被五个人整除。

```sql
person.age % 5 = 0
```

## 后续步骤

现在，您已经了解了算术函数，可以在PQL查询中使用它们。 有关其他PQL函数的详细信息，请阅读[用户档案查询语言概述](./overview.md)。

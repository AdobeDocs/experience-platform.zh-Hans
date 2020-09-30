---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;comparison functions;comparison;
solution: Experience Platform
title: 比较函数
topic: developer guide
description: 比较函数用于比较不同的表达式和值，并相应地返回“true”或“false”。
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 10%

---


# 比较函数

比较函数用于比较不同的表达式和值、返回或相 `true` 应的 `false` 值。 有关其他PQL功能的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md)。

## 等于

( `=` 等于)函数检查一个值或表达式是否等于另一个值或表达式。

**Format**

```sql
{EXPRESSION} = {VALUE}
```

**示例**

以下PQL查询检查主地址国家／地区是否位于加拿大。

```sql
homeAddress.countryISO = "CA"
```

## 不等于

( `!=` 不相等)函数检查一个值或表达式是否 **不等** 于另一个值或表达式。

**Format**

```sql
{EXPRESSION} != {VALUE}
```

**示例**

以下PQL查询检查主地址国家／地区是否不在加拿大。

```sql
homeAddress.countryISO != "CA"
```

## 大于

( `>` 大于)函数用于检查第一值是否大于第二值。

**Format**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**示例**

以下PQL查询定义生日不在1月或2月的人。

```sql
person.birthMonth > 2
```

## 大于或等于

( `>=` 大于或等于)函数用于检查第一值是否大于或等于第二值。

**Format**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**示例**

以下PQL查询定义生日不在1月或2月的人。

```sql
person.birthMonth >= 3
```

## 小于

比 `<` 较函数（小于）用于检查第一值是否小于第二值。

**Format**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**示例**

以下PQL查询定义生日在1月的人。

```sql
person.birthMonth < 2
```

## 小于或等于

比 `<=` 较函数（小于或等于）用于检查第一值是否小于或等于第二值。

**Format**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**示例**

以下PQL查询定义生日在1月或2月的人。

```sql
person.birthMonth <= 2
```

## 后续步骤

现在您已经了解了比较功能，可以在PQL查询中使用它们。 有关其他PQL功能的详细信息，请阅读 [用户档案查询语概述](./overview.md)。

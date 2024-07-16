---
solution: Experience Platform
title: PQL比较函数
description: 比较函数用于比较不同表达式和值之间的差异，并相应地返回“true”或“false”。
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 7%

---

# 比较函数

比较函数用于比较不同的表达式和值，相应地返回`true`或`false`。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## 等于

`=` （等于）函数检查一个值或表达式是否等于另一个值或表达式。

**格式**

```sql
{EXPRESSION} = {VALUE}
```

**示例**

以下PQL查询检查家庭地址国家/地区是否位于加拿大。

```sql
homeAddress.countryISO = "CA"
```

## 不等于

`!=` （不等于）函数检查一个值或表达式是&#x200B;**不是**&#x200B;等于另一个值或表达式。

**格式**

```sql
{EXPRESSION} != {VALUE}
```

**示例**

以下PQL查询检查家庭地址国家/地区是否不在加拿大。

```sql
homeAddress.countryISO != "CA"
```

## 大于

`>` （大于）函数用于检查第一个值是否大于第二个值。

**格式**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**示例**

以下PQL查询定义出生日期在1月或2月以下的人员。

```sql
person.birthMonth > 2
```

## 大于或等于

`>=` （大于或等于）函数用于检查第一个值是否大于或等于第二个值。

**格式**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**示例**

以下PQL查询定义出生日期在1月或2月以下的人员。

```sql
person.birthMonth >= 3
```

## 小于

`<` （小于）比较函数用于检查第一个值是否小于第二个值。

**格式**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**示例**

以下PQL查询定义生日在一月的人员。

```sql
person.birthMonth < 2
```

## 小于或等于

`<=` （小于或等于）比较函数用于检查第一个值是否小于或等于第二个值。

**格式**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**示例**

以下PQL查询定义生日在一月或二月的人员。

```sql
person.birthMonth <= 2
```

## 后续步骤

现在，您已了解比较函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读[Profile Query Language概述](./overview.md)。

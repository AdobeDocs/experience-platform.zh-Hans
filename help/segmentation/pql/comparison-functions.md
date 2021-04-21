---
keywords: Experience Platform；主题；热门主题；分段；分段；分段服务；pql;PQL;用户档案查询语言；比较功能；
solution: Experience Platform
title: PQL比较函数
topic-legacy: developer guide
description: 比较函数用于比较不同的表达式和值，并相应地返回“true”或“false”。
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 9%

---

# 比较函数

比较函数用于比较不同的表达式和值，并相应地返回`true`或`false`。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] overview](./overview.md)。

## 等于

`=`(equals)函数检查一个值或表达式是否等于另一个值或表达式。

**格式**

```sql
{EXPRESSION} = {VALUE}
```

**示例**

以下PQL查询检查主地址国家/地区是否位于加拿大。

```sql
homeAddress.countryISO = "CA"
```

## 不等于

`!=`（不相等）函数检查一个值或表达式是否&#x200B;**不**&#x200B;等于另一个值或表达式。

**格式**

```sql
{EXPRESSION} != {VALUE}
```

**示例**

以下PQL查询检查主地址国家/地区是否不在加拿大。

```sql
homeAddress.countryISO != "CA"
```

## 大于

`>`（大于）函数用于检查第一值是否大于第二值。

**格式**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**示例**

以下PQL查询定义生日不在1月或2月的人。

```sql
person.birthMonth > 2
```

## 大于或等于

`>=`（大于或等于）函数用于检查第一值是否大于或等于第二值。

**格式**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**示例**

以下PQL查询定义生日不在1月或2月的人。

```sql
person.birthMonth >= 3
```

## 小于

使用`<`（小于）比较函数检查第一值是否小于第二值。

**格式**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**示例**

以下PQL查询定义生日在1月的人。

```sql
person.birthMonth < 2
```

## 小于或等于

使用`<=`（小于或等于）比较函数检查第一值是否小于或等于第二值。

**格式**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**示例**

以下PQL查询定义生日在1月或2月的人。

```sql
person.birthMonth <= 2
```

## 后续步骤

现在，您已经了解了比较功能，可以在PQL查询中使用它们。 有关其他PQL函数的详细信息，请阅读[用户档案查询语言概述](./overview.md)。

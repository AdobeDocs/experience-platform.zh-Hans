---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；PQL;PQL；配置文件查询语言；比较函数；比较；
solution: Experience Platform
title: PQL比较函数
description: 比较函数用于比较不同表达式和值，并相应地返回“true”或“false”。
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 9%

---

# 比较函数

比较函数用于比较不同表达式和值之间的差异，返回 `true` 或 `false` 因此。 有关其他PQL函数的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md).

## 等于

的 `=` （等于）函数检查一个值或表达式是否等于另一个值或表达式。

**格式**

```sql
{EXPRESSION} = {VALUE}
```

**示例**

以下PQL查询会检查家庭地址国家/地区是否位于加拿大。

```sql
homeAddress.countryISO = "CA"
```

## 不等于

的 `!=` （不等于）函数检查一个值或表达式是否为 **not** 等于其他值或表达式。

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

的 `>` （大于）函数用于检查第一个值是否大于第二个值。

**格式**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**示例**

以下PQL查询可定义生日不在1月或2月的人员。

```sql
person.birthMonth > 2
```

## 大于或等于

的 `>=` （大于或等于）函数用于检查第一个值是否大于或等于第二个值。

**格式**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**示例**

以下PQL查询可定义生日不在1月或2月的人员。

```sql
person.birthMonth >= 3
```

## 小于

的 `<` （小于）比较函数用于检查第一值是否小于第二值。

**格式**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**示例**

以下PQL查询定义生日在1月的人员。

```sql
person.birthMonth < 2
```

## 小于或等于

的 `<=` （小于或等于）比较函数用于检查第一值是否小于或等于第二值。

**格式**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**示例**

以下PQL查询定义生日在1月或2月的人员。

```sql
person.birthMonth <= 2
```

## 后续步骤

现在，您已经了解了比较函数，接下来可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语言概述](./overview.md).

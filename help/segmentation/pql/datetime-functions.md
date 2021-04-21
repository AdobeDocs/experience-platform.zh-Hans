---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；pql;PQL;用户档案查询语言；日期和时间函数；日期时间函数；日期时间；时间；时间；
solution: Experience Platform
title: PQL日期和时间函数
topic-legacy: developer guide
description: 日期和时间函数用于对用户档案查询语言(PQL)中的值执行日期和时间操作。
exl-id: 8cbffcb6-1c25-454f-8f02-eca602318e5e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 3%

---

# 日期和时间函数

日期和时间函数用于对[!DNL Profile Query Language](PQL)中的值执行日期和时间操作。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] overview](./overview.md)。

## 当月

`currentMonth`函数将当前月份返回为整数。

**格式**

```sql
currentMonth()
```

**示例**

以下PQL查询检查人员的出生月是否为当月。

```sql
person.birthMonth = currentMonth()
```

## 获得月

`getMonth`函数根据给定的时间戳以整数形式返回月份。

**格式**

```sql
{TIMESTAMP}.getMonth()
```

**示例**

以下PQL查询检查人员的出生月是否在6月。

```sql
person.birthdate.getMonth() = 6
```

## 本年度

`currentYear`函数将当前年份作为整数返回。

**格式**

```sql
currentYear()
```

**示例**

以下PQL查询会检查产品是否在当年销售。

```sql
product.saleYear = currentYear()
```

## 获取年份

`getYear`函数根据给定的时间戳以整数形式返回年份。

**格式**

```sql
{TIMESTAMP}.getYear()
```

**示例**

以下PQL查询检查该人的出生年度是否在1991、1992、1993、1994或1995年。

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## 当月当天

`currentDayOfMonth`函数以整数形式返回当月的当天。

**格式**

```sql
currentDayOfMonth()
```

**示例**

以下PQL查询检查人员的出生日是否与当月的当天匹配。

```sql
person.birthDay = currentDayOfMonth()
```

## 获取月份

`getDayOfMonth`函数根据给定的时间戳以整数形式返回该日。

**格式**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**示例**

以下PQL查询将检查该物料是否在当月的前15天内销售。

```sql
product.sale.getDayOfMonth() <= 15
```

## 发生

`occurs`函数将给定时间戳函数与固定时间段进行比较。

**格式**

`occurs`函数可以使用以下任一格式编写：

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{COMPARISON}` | 比较运算符。 可以是下列任何运算符：`>`、`>=`、`<`、`<=`、`=`、`!=`。 有关比较函数的详细信息，请参阅[比较函数文档](./comparison-functions.md)。 |
| `{INTEGER}` | 非负整数。 |
| `{TIME_UNIT}` | 时间单位。 可以是以下任意单词：`millisecond(s)`、`second(s)`、`minute(s)`、`hour(s)`、`day(s)`、`week(s)`、`month(s)`、`year(s)`、`decade(s)`、`century`、`centuries`、`millennium`、`millennia`。 |
| `{DIRECTION}` | 描述何时将日期进行比较的预置。 可以是以下任意单词：`before`、`after`、`from`。 |
| `{TIME}` | 可以是时间戳文本(`today`、`now`、`yesterday`、`tomorrow`)、相对时间单位（`this`、`last`或`next`之一，后跟时间单位）或时间戳属性。 |

>[!NOTE]
>
>使用单词`on`是可选的。 它可以提高某些组合（如`timestamp occurs on date(2019,12,31)`）的可读性。

**示例**

以下PQL查询将检查该物料是否在上周出售。

```sql
product.saleDate occurs last week
```

以下PQL查询将检查2015年1月8日至2017年7月1日之间是否销售了某个项目。

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## 现在

`now` 是表示PQL执行的时间戳的保留字。

**示例**

以下PQL查询会检查物料是否在三小时前售出。

```sql
product.saleDate occurs = 3 hours before now
```

## 今天

`today` 是一个保留字，表示PQL执行当日开始的时间戳。

**示例**

以下PQL查询会检查某人的生日是否在三天前。

```sql
person.birthday occurs = 3 days before today
```

## 后续步骤

现在，您已经了解了日期和时间功能，可以在PQL查询中使用它们。 有关其他PQL函数的详细信息，请阅读[用户档案查询语言概述](./overview.md)。

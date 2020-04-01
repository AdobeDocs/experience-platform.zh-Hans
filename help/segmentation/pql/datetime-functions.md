---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 日期和时间函数
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# 日期和时间函数

日期和时间函数用于对用户档案查询语言(PQL)中的值执行日期和时间操作。 有关其他PQL函数的更多信息，请参阅 [用户档案查询语言概述](./overview.md)。

## 当月

该函 `currentMonth` 数将当月返回为整数。

**格式**

```sql
currentMonth()
```

**示例**

以下PQL查询检查人员的出生月份是否为当月。

```sql
person.birthMonth = currentMonth()
```

## 获得月

该函 `getMonth` 数基于给定的时间戳以整数形式返回月份。

**格式**

```sql
{TIMESTAMP}.getMonth()
```

**示例**

以下PQL查询检查人员的出生月份是否在6月。

```sql
person.birthdate.getMonth() = 6
```

## 本年度

该函 `currentYear` 数将当前年份返回为整数。

**格式**

```sql
currentYear()
```

**示例**

以下PQL查询检查产品是否在当年销售。

```sql
product.saleYear = currentYear()
```

## 获得年份

该函 `getYear` 数基于给定的时间戳以整数形式返回年份。

**格式**

```sql
{TIMESTAMP}.getYear()
```

**示例**

以下PQL查询检查该人的出生年是否在1991、1992、1993、1994或1995年。

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## 当月当天

该函 `currentDayOfMonth` 数以整数形式返回当月的当天。

**格式**

```sql
currentDayOfMonth()
```

**示例**

以下PQL查询检查人员的出生日是否与当月的当天匹配。

```sql
person.birthDay = currentDayOfMonth()
```

## 获取月份日

该函 `getDayOfMonth` 数基于给定的时间戳，以整数形式返回该日。

**格式**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**示例**

以下PQL查询检查该物料是否在月的前15天内销售。

```sql
product.sale.getDayOfMonth() <= 15
```

## 发生

该函 `occurs` 数将给定时间戳函数与固定时间段进行比较。

**格式**

函 `occurs` 数可以使用以下任意格式编写：

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{COMPARISON}` | 比较运算符。 可以是下列任何运算符： `>`, `>=``<`, `<=`, `=`, `!=`. 有关比较函数的更多信息可在比较函数 [文档中找到](./comparison-functions.md)。 |
| `{INTEGER}` | 非负整数。 |
| `{TIME_UNIT}` | 时间单位。 可以是以下任意单词： `millisecond(s)`、 `second(s)`、、、 `minute(s)`、、 `hour(s)`、 `day(s)`、、 `week(s)``month(s)``year(s)``decade(s)``century``centuries``millennium``millennia`。 |
| `{DIRECTION}` | 描述何时比较日期的预置。 可以是以下任意单词： `before`, `after`, `from`。 |
| `{TIME}` | 可以是时间戳文本(`today`、 `now`、 `yesterday`、)、相对时间单位(时间单位之一、 `tomorrow`或 `this``last``next` 后跟时间单位)或时间戳属性。 |

>[!NOTE] 使用单词是可选 `on` 的。 它可以提高某些组合的可读性，例如 `timestamp occurs on date(2019,12,31)`。

**示例**

以下PQL查询检查该物品是否于上周出售。

```sql
product.saleDate occurs last week
```

以下PQL查询检查2015年1月8日至2017年7月1日之间是否销售了某个物品。

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## 现在

`now` 是表示PQL执行的时间戳的保留字。

**示例**

以下PQL查询检查某个物品在三小时前是否售出。

```sql
product.saleDate occurs = 3 hours before now
```

## 今天

`today` 是表示PQL执行日期开始的时间戳的保留字。

**示例**

以下PQL查询检查某人的生日是否在三天前。

```sql
person.birthday occurs = 3 days before today
```

## 后续步骤

现在您已经了解了日期和时间功能，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语概述](./overview.md)。

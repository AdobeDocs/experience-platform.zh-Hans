---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;date and time functions;datetime functions;datetime;date;time;
solution: Experience Platform
title: 日期和时间函数
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 4%

---


# 日期和时间函数

日期和时间函数用于对(PQL)中的值执行日期和 [!DNL Profile Query Language] 时间操作。 有关其他PQL功能的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md)。

## 当月

该函 `currentMonth` 数将当月返回为整数。

**Format**

```sql
currentMonth()
```

**示例**

以下PQL查询检查人员的出生月是否为当月。

```sql
person.birthMonth = currentMonth()
```

## 获取月份

该函 `getMonth` 数根据给定的时间戳以整数形式返回月份。

**Format**

```sql
{TIMESTAMP}.getMonth()
```

**示例**

以下PQL查询检查人员的出生月份是否在6月。

```sql
person.birthdate.getMonth() = 6
```

## 本年度

该函 `currentYear` 数以整数形式返回当前年份。

**Format**

```sql
currentYear()
```

**示例**

以下PQL查询检查产品是否在当年销售。

```sql
product.saleYear = currentYear()
```

## 获取年份

该函 `getYear` 数根据给定的时间戳以整数形式返回年份。

**Format**

```sql
{TIMESTAMP}.getYear()
```

**示例**

以下PQL查询检查该人的出生年数是否在1991、1992、1993、1994或1995年。

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## 当月当天

函 `currentDayOfMonth` 数以整数形式返回当月的当天。

**Format**

```sql
currentDayOfMonth()
```

**示例**

以下PQL查询检查人员的出生日是否与当月的当天匹配。

```sql
person.birthDay = currentDayOfMonth()
```

## 获取月份

该函 `getDayOfMonth` 数根据给定的时间戳以整数形式返回该日。

**Format**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**示例**

以下PQL查询检查该物料是否在当月的前15天内销售。

```sql
product.sale.getDayOfMonth() <= 15
```

## 发生

该 `occurs` 函数将给定时间戳函数与固定时间段进行比较。

**Format**

函 `occurs` 数可以使用以下任一格式编写：

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{COMPARISON}` | 比较运算符。 可以是下列任何运算符： `>`、 `>=`、 `<`、 `<=`、 `=`、 `!=`。 在比较函数文档中可以找到有关比较函 [数的更多信息](./comparison-functions.md)。 |
| `{INTEGER}` | 非负整数。 |
| `{TIME_UNIT}` | 时间单位。 可以是以下任意单词： `millisecond(s)`、 `second(s)`、 `minute(s)`、、 `hour(s)`、、 `day(s)`、、 `week(s)`、、 `month(s)``year(s)``decade(s)``century``centuries``millennium``millennia`、、、。 |
| `{DIRECTION}` | 描述何时将日期与之进行比较的预置。 可以是以下任意单词： `before`, `after`, `from` |
| `{TIME}` | 可以是时间戳文`today`本( `now`、、 `yesterday`、 `tomorrow`)、相对时间单位(时间单 `this`元之一、 `last`或 `next` 后跟时间单元)或时间戳属性。 |

>[!NOTE]
>
>单词的使用是 `on` 可选的。 它可以提高某些组合的可读性，例如 `timestamp occurs on date(2019,12,31)`。

**示例**

以下PQL查询检查该物料是否上周售出。

```sql
product.saleDate occurs last week
```

以下PQL查询检查2015年1月8日至2017年7月1日之间是否销售了某个项目。

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## 现在

`now` 是表示PQL执行时间戳的保留字。

**示例**

以下PQL查询会检查物料是否在三小时前才售出。

```sql
product.saleDate occurs = 3 hours before now
```

## 今天

`today` 是一个保留字，表示PQL执行日开始的时间戳。

**示例**

以下PQL查询检查人员的生日是否在三天前。

```sql
person.birthday occurs = 3 days before today
```

## 后续步骤

现在您已经了解了日期和时间功能，可以在PQL查询中使用它们。 有关其他PQL功能的详细信息，请阅读 [用户档案查询语概述](./overview.md)。

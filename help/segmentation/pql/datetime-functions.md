---
solution: Experience Platform
title: PQL日期和时间函数
description: 日期和时间函数用于对配置文件查询语言(PQL)中的值执行日期和时间操作。
exl-id: 8cbffcb6-1c25-454f-8f02-eca602318e5e
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 4%

---

# 日期和时间函数

日期和时间函数用于对以下范围内的值执行日期和时间操作 [!DNL Profile Query Language] (PQL)。 有关其他PQL函数的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md).

## 当前月份

此 `currentMonth` 函数以整数形式返回当前月份。

**格式**

```sql
currentMonth()
```

**示例**

以下PQL查询检查个人的出生月是否为当月。

```sql
person.birthMonth = currentMonth()
```

## 获取月份

此 `getMonth` 函数根据给定的时间戳以整数的形式返回月份。

**格式**

```sql
{TIMESTAMP}.getMonth()
```

**示例**

以下PQL查询检查个人的出生月份是否为6月。

```sql
person.birthdate.getMonth() = 6
```

## 当前年份

此 `currentYear` 函数以整数形式返回当前年份。

**格式**

```sql
currentYear()
```

**示例**

以下PQL查询检查产品是否在本年度销售。

```sql
product.saleYear = currentYear()
```

## 获取年份

此 `getYear` 函数根据给定的时间戳以整数的形式返回年份。

**格式**

```sql
{TIMESTAMP}.getYear()
```

**示例**

以下PQL查询检查个人的出生年份是1991、1992、1993、1994还是1995年。

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## 当月日期

此 `currentDayOfMonth` 函数以整数形式返回月份的当前日期。

**格式**

```sql
currentDayOfMonth()
```

**示例**

以下PQL查询检查人员的出生日期是否与当月的当天匹配。

```sql
person.birthDay = currentDayOfMonth()
```

## 获取月中的日

此 `getDayOfMonth` 函数会根据给定的时间戳以整数的形式返回日。

**格式**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**示例**

以下PQL查询检查该项是否在一个月的最初15天内售出。

```sql
product.sale.getDayOfMonth() <= 15
```

## 发生

此 `occurs` 函数将给定的时间戳函数与固定时间段进行比较。

**格式**

此 `occurs` 函数可使用以下任意格式进行编写：

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{COMPARISON}` | 比较运算符。 可以是以下任意运算符： `>`， `>=`， `<`， `<=`， `=`， `!=`. 有关比较函数的更多信息，请参阅 [比较函数文档](./comparison-functions.md). |
| `{INTEGER}` | 非负整数。 |
| `{TIME_UNIT}` | 时间单位。 可以是以下任一单词： `millisecond(s)`， `second(s)`， `minute(s)`， `hour(s)`， `day(s)`， `week(s)`， `month(s)`， `year(s)`， `decade(s)`， `century`， `centuries`， `millennium`， `millennia`. |
| `{DIRECTION}` | 描述何时将日期与进行比较的前置词。 可以是以下任一单词： `before`， `after`， `from`. |
| `{TIME}` | 可以是时间戳文字(`today`， `now`， `yesterday`， `tomorrow`)，相对时间单位(以下项之一 `this`， `last`，或 `next` 后跟一个时间单位)或时间戳属性。 |

>[!NOTE]
>
>单词的用法 `on` 是可选的。 它可以提高某些组合的可读性，例如 `timestamp occurs on date(2019,12,31)`.

**示例**

以下PQL查询检查该项上周是否售出。

```sql
product.saleDate occurs last week
```

以下PQL查询检查某个项目是否在2015年1月8日至2017年7月1日期间售出。

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## 现在

`now` 是一个保留字，表示PQL执行的时间戳。

**示例**

以下PQL查询检查项目是否刚好在三小时前售出。

```sql
product.saleDate occurs = 3 hours before now
```

## 今天

`today` 是一个保留字，表示PQL执行之日开始的时间戳。

**示例**

以下PQL查询检查个人的生日是否为三天前。

```sql
person.birthday occurs = 3 days before today
```

## 后续步骤

现在您已了解日期和时间函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [配置文件查询语言概述](./overview.md).

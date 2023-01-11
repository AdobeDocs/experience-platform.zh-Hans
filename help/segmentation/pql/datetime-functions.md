---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；PQL;PQL；配置文件查询语言；日期和时间函数；日期时间函数；日期时间；日期时间；时间；
solution: Experience Platform
title: PQL日期和时间函数
description: 日期和时间函数用于对配置文件查询语言(PQL)中的值执行日期和时间操作。
exl-id: 8cbffcb6-1c25-454f-8f02-eca602318e5e
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 3%

---

# 日期和时间函数

日期和时间函数用于对 [!DNL Profile Query Language] (PQL)。 有关其他PQL函数的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md).

## 当月

的 `currentMonth` 函数将当前月份作为整数返回。

**格式**

```sql
currentMonth()
```

**示例**

以下PQL查询检查人员的出生月份是否为当月。

```sql
person.birthMonth = currentMonth()
```

## 获取月份

的 `getMonth` 函数根据给定的时间戳以整数形式返回月份。

**格式**

```sql
{TIMESTAMP}.getMonth()
```

**示例**

以下PQL查询检查人员的出生月份是否在6月。

```sql
person.birthdate.getMonth() = 6
```

## 当年

的 `currentYear` 函数将当前年份作为整数返回。

**格式**

```sql
currentYear()
```

**示例**

以下PQL查询检查产品是否在当年销售。

```sql
product.saleYear = currentYear()
```

## 获取年份

的 `getYear` 函数根据给定的时间戳以整数形式返回年。

**格式**

```sql
{TIMESTAMP}.getYear()
```

**示例**

以下PQL查询检查人员的出生年是在1991、1992、1993、1994或1995年。

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## 当天

的 `currentDayOfMonth` 函数会以整数形式返回当月的当天。

**格式**

```sql
currentDayOfMonth()
```

**示例**

以下PQL查询检查人员的出生日期是否与当月的当天匹配。

```sql
person.birthDay = currentDayOfMonth()
```

## 获取日期

的 `getDayOfMonth` 函数根据给定的时间戳以整数形式返回日。

**格式**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**示例**

以下PQL查询会检查该物料是否在当月前15天内售出。

```sql
product.sale.getDayOfMonth() <= 15
```

## 发生

的 `occurs` 函数会将给定的时间戳函数与固定时间段进行比较。

**格式**

的 `occurs` 函数可使用以下任何格式写入：

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{COMPARISON}` | 比较运算符。 可以是以下任意运算符： `>`, `>=`, `<`, `<=`, `=`, `!=`. 有关比较函数的更多信息，请参阅 [比较函数文档](./comparison-functions.md). |
| `{INTEGER}` | 非负整数。 |
| `{TIME_UNIT}` | 时间单位。 可以是以下任意词语： `millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `month(s)`, `year(s)`, `decade(s)`, `century`, `centuries`, `millennium`, `millennia`. |
| `{DIRECTION}` | 描述何时比较日期的预置。 可以是以下任意词语： `before`, `after`, `from`. |
| `{TIME}` | 可以是时间戳文字(`today`, `now`, `yesterday`, `tomorrow`)，相对时间单位( `this`, `last`或 `next` 后跟时间单位)或时间戳属性。 |

>[!NOTE]
>
>单词的用法 `on` 为可选。 对于某些组合(例如， `timestamp occurs on date(2019,12,31)`.

**示例**

以下PQL查询检查该项目是否在上周售出。

```sql
product.saleDate occurs last week
```

以下PQL查询检查2015年1月8日至2017年7月1日期间是否销售了某个项目。

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## 现在

`now` 是表示PQL执行的时间戳的保留字。

**示例**

以下PQL查询会检查某个项目是否在三小时前才售出。

```sql
product.saleDate occurs = 3 hours before now
```

## 今天

`today` 是一个保留字，表示PQL执行当天开始的时间戳。

**示例**

以下PQL查询检查人员的生日是否在三天前。

```sql
person.birthday occurs = 3 days before today
```

## 后续步骤

现在，您已经了解了日期和时间函数，接下来可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语言概述](./overview.md).

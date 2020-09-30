---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;boolean functions;boolean;
solution: Experience Platform
title: 布尔函数
topic: developer guide
description: 布尔函数用于对用户档案查询语言(PQL)中的不同元素执行布尔逻辑。
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 6%

---


# 布尔函数

布尔函数用于对(PQL)中的不同元素执行 [!DNL Profile Query Language] 布尔逻辑。  有关其他PQL功能的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md)。

## 和

函数 `and` 用于创建逻辑连接。

**Format**

```sql
{QUERY} and {QUERY}
```

**示例**

以下PQL查询将返回所有在加拿大和1985年出生的人。

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## 或

函 `or` 数用于创建逻辑分离。

**Format**

```sql
{QUERY} or {QUERY}
```

**示例**

以下PQL查询将返回所有在加拿大或1985年出生的人。

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## 非

( `not` 或) `!`函数用于创建逻辑取反。

**Format**

```sql
not ({QUERY})
!({QUERY})
```

**示例**

以下PQL查询将返回所有没有加拿大作为母国的人员。

```sql
not (homeAddress.countryISO = "CA")
```

## 如果

函 `if` 数用于根据指定的条件是否为真来解析表达式。

**Format**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | 正在测试的布尔表达式。 |
| `{TRUE_EXPRESSION}` | 值为true时将使用的 `{TEST_EXPRESSION}` 表达式。 |
| `{FALSE_EXPRESSION}` | 如果为false，则使用其 `{TEST_EXPRESSION}` 值的表达式。 |

**示例**

以下PQL查询将设置此值， `1` 如果母国是加拿大， `2` 如果母国不是加拿大。

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## 后续步骤

现在您已经了解了布尔函数，可以在PQL查询中使用它们。 有关其他PQL功能的详细信息，请阅读 [用户档案查询语概述](./overview.md)。

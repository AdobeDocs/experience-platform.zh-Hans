---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 布尔函数
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# 布尔函数

Boolean函数用于对用户档案查询语言(PQL)中的不同元素执行布尔逻辑。  有关其他PQL函数的更多信息，请参阅 [用户档案查询语言概述](./overview.md)。

## 和

函数 `and` 用于创建逻辑连接。

**格式**

```sql
{QUERY} and {QUERY}
```

**示例**

以下PQL查询将返回所有以加拿大为母国的人和1985年出生年。

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## 或

函数 `or` 用于创建逻辑分离。

**格式**

```sql
{QUERY} or {QUERY}
```

**示例**

以下PQL查询将返回所有在加拿大或1985年出生的人。

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## 非

( `not` 或 `!`)函数用于创建逻辑取反。

**格式**

```sql
not ({QUERY})
!({QUERY})
```

**示例**

以下PQL查询将返回所有没有加拿大作为其祖国的人。

```sql
not (homeAddress.countryISO = "CA")
```

## 如果

函 `if` 数用于根据指定的条件是否为真解析表达式。

**格式**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | 正在测试的布尔表达式。 |
| `{TRUE_EXPRESSION}` | 如果为true，则使用其值 `{TEST_EXPRESSION}` 的表达式。 |
| `{FALSE_EXPRESSION}` | 如果为false，则使用其值 `{TEST_EXPRESSION}` 的表达式。 |

**示例**

以下PQL查询将设置该值，如 `1` 果母国是加拿大，而 `2` 如果母国不是加拿大。

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## 后续步骤

现在您已经学习了布尔函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语概述](./overview.md)。

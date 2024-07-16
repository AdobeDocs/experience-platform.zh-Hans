---
solution: Experience Platform
title: PQL布尔函数
description: 布尔函数用于对Profile Query Language (PQL)中的不同元素执行布尔逻辑。
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 4%

---

# 布尔函数

布尔函数用于对[!DNL Profile Query Language] (PQL)中的其他元素执行布尔逻辑。  有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## 和

`and`函数用于创建逻辑连接。

**格式**

```sql
{QUERY} and {QUERY}
```

**示例**

以下PQL查询将返回所有原籍国为加拿大且出生年份为1985的人。

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## 或

`or`函数用于创建逻辑分离。

**格式**

```sql
{QUERY} or {QUERY}
```

**示例**

以下PQL查询将返回所有原籍国为加拿大或1985年出生年份的人。

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## 非

`not` （或`!`）函数用于创建逻辑否定。

**格式**

```sql
not ({QUERY})
!({QUERY})
```

**示例**

以下PQL查询将返回所有没有祖国作为加拿大的人。

```sql
not (homeAddress.countryISO = "CA")
```

## 如果

`if`函数用于解析表达式，具体取决于指定的条件是否为true。

**格式**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | 正在测试的布尔表达式。 |
| `{TRUE_EXPRESSION}` | 如果`{TEST_EXPRESSION}`为true，将使用其值的表达式。 |
| `{FALSE_EXPRESSION}` | 如果`{TEST_EXPRESSION}`为false，将使用其值的表达式。 |

**示例**

如果母国是加拿大，以下PQL查询将值设置为`1`；如果母国不是加拿大，则将值设置为`2`。

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## 后续步骤

现在，您已了解布尔函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读[Profile Query Language概述](./overview.md)。

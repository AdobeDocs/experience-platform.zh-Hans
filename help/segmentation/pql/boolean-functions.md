---
keywords: Experience Platform；主题；热门主题；分段；分段；分段服务；pql;PQL;用户档案查询语；布尔函数；
solution: Experience Platform
title: PQL布尔函数
topic: developer guide
description: 布尔函数用于对用户档案查询语言(PQL)中的不同元素执行布尔逻辑。
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 5%

---


# 布尔函数

布尔函数用于对[!DNL Profile Query Language](PQL)中的不同元素执行布尔逻辑。  有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## 和

`and`函数用于创建逻辑连接。

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

`or`函数用于创建逻辑分离。

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

`not`（或`!`）函数用于创建逻辑取反。

**格式**

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

`if`函数用于根据指定的条件是否为真来解析表达式。

**格式**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | 正在测试的布尔表达式。 |
| `{TRUE_EXPRESSION}` | 如果`{TEST_EXPRESSION}`为true，将使用其值的表达式。 |
| `{FALSE_EXPRESSION}` | `{TEST_EXPRESSION}`为false时将使用其值的表达式。 |

**示例**

如果主国为加拿大，以下PQL查询将该值设置为`1`；如果主国不是加拿大，则将该值设置为`2`。

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## 后续步骤

现在您已经了解了布尔函数，可以在PQL查询中使用它们。 有关其他PQL函数的详细信息，请阅读[用户档案查询语语言概述](./overview.md)。

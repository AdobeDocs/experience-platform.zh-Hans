---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；pql；PQL；配置文件查询语言；布尔函数；布尔值；
solution: Experience Platform
title: PQL布尔函数
description: 布尔函数用于对配置文件查询语言(PQL)中的不同元素执行布尔逻辑。
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 5%

---

# 布尔函数

布尔函数用于对中的不同元素执行布尔逻辑 [!DNL Profile Query Language] (PQL)。  有关其他PQL函数的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md).

## 和

此 `and` 函数用于创建逻辑连接。

**格式**

```sql
{QUERY} and {QUERY}
```

**示例**

以下PQL查询将返回所有其原籍国为加拿大且出生年份为1985年的人员。

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## 或

此 `or` 函数用于创建逻辑分离。

**格式**

```sql
{QUERY} or {QUERY}
```

**示例**

以下PQL查询将返回所有原籍国为加拿大或1985年出生年份的人。

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## 不为

此 `not` (或 `!`)函数用于创建逻辑否定。

**格式**

```sql
not ({QUERY})
!({QUERY})
```

**示例**

以下PQL查询将返回所有没有其母国为加拿大的人。

```sql
not (homeAddress.countryISO = "CA")
```

## 如果

此 `if` 函数用于解析表达式，具体取决于指定的条件是否为true。

**格式**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | 正在测试的布尔表达式。 |
| `{TRUE_EXPRESSION}` | 在以下情况下将使用其值的表达式： `{TEST_EXPRESSION}` 为true。 |
| `{FALSE_EXPRESSION}` | 在以下情况下将使用其值的表达式： `{TEST_EXPRESSION}` 为假。 |

**示例**

以下PQL查询会将值设置为 `1` 如果母国是加拿大和 `2` 如果祖国不是加拿大。

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## 后续步骤

现在，您已了解布尔函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [配置文件查询语言概述](./overview.md).

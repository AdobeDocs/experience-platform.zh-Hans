---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；PQL;PQL；配置文件查询语言；布尔函数；布尔值；
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

的 `and` 函数创建逻辑连接。

**格式**

```sql
{QUERY} and {QUERY}
```

**示例**

以下PQL查询将返回以加拿大为原籍国和出生年为1985年的所有人。

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## 或

的 `or` 函数创建逻辑分离。

**格式**

```sql
{QUERY} or {QUERY}
```

**示例**

以下PQL查询将返回所有在加拿大或出生年为1985年的原籍国的人。

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## 不为

的 `not` (或 `!`)函数创建逻辑求反。

**格式**

```sql
not ({QUERY})
!({QUERY})
```

**示例**

以下PQL查询将返回所有未将其祖国/地区作为加拿大的人员。

```sql
not (homeAddress.countryISO = "CA")
```

## 如果

的 `if` 函数用于根据指定条件是否为true来解析表达式。

**格式**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | 正在测试的布尔表达式。 |
| `{TRUE_EXPRESSION}` | 值将在 `{TEST_EXPRESSION}` 是真的。 |
| `{FALSE_EXPRESSION}` | 值将在 `{TEST_EXPRESSION}` 为false。 |

**示例**

以下PQL查询会将值设置为 `1` 如果祖国是加拿大和 `2` 如果祖国不是加拿大。

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## 后续步骤

现在，您已经了解了布尔函数，接下来可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语言概述](./overview.md).

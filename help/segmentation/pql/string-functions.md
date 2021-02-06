---
keywords: Experience Platform；主题；热门主题；分段；分段；分段服务；pql;PQL;用户档案查询语；字符串函数；字符串；
solution: Experience Platform
title: PQL字符串函数
topic: developer guide
description: 用户档案查询语言(PQL)优惠函数可简化与字符串的交互。
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 6%

---


# 字符串函数

[!DNL Profile Query Language] (PQL)优惠函数可简化与字符串的交互。有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## 喜欢

`like`函数用于确定字符串是否与指定的模式匹配。

**Format**

```sql
{STRING_1} like {STRING_2}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要与第一个字符串匹配的表达式。 有两个支持的特殊字符用于创建表达式:`%`和`_`。 <ul><li>`%` 用于表示零个或多个字符。</li><li>`_` 用于表示一个字符。</li></ul> |

**示例**

以下PQL查询检索包含模式“es”的所有城市。

```sql
city like "%es%"
```

## 开始于

`startsWith`函数用于确定字符串是否开始指定的子字符串。

**格式**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写的可选参数。 默认情况下，此值设置为true。 |

**示例**

以下PQL查询区分大小写确定人员的姓名开始是否为“Joe”。

```sql
person.name.startsWith("Joe")
```

## 不开始

`doesNotStartWith`函数用于确定字符串是否不与指定的子字符串开始。

**格式**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写的可选参数。 默认情况下，此值设置为true。 |

**示例**

以下PQL查询区分大小写确定人员的姓名不与“Joe”开始。

```sql
person.name.doesNotStartWith("Joe")
```

## 结束于

`endsWith`函数用于确定字符串是否以指定的子字符串结尾。

**格式**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写的可选参数。 默认情况下，此值设置为true。 |

**示例**

以下PQL查询区域根据大小写确定人员的电子邮件地址是否以“.com”结尾。

```sql
person.emailAddress.endsWith(".com")
```

## 不以

`doesNotEndWith`函数用于确定字符串是否以指定的子字符串结尾。

**格式**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写的可选参数。 默认情况下，此值设置为true。 |

**示例**

以下PQL查询区域根据大小写确定人员的电子邮件地址以“.com”结尾。

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Contains

`contains`函数用于确定字符串是否包含指定的子字符串。

**格式**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写的可选参数。 默认情况下，此值设置为true。 |

**示例**

以下PQL查询区分大小写确定人员的电子邮件地址是否包含字符串“2010@gm”。

```sql
person.emailAddress.contains("2010@gm")
```

## 不包含

`doesNotContain`函数用于确定字符串是否不包含指定的子字符串。

**格式**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写的可选参数。 默认情况下，此值设置为true。 |

**示例**

以下PQL查询区分大小写确定人员的电子邮件地址不包含字符串“2010@gm”。

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## 等于

`equals`函数用于确定字符串是否等于指定的字符串。

**格式**

```sql
{STRING_1}.equals({STRING_2})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要与第一个字符串进行比较的字符串。 |

**示例**

以下PQL查询根据大小写确定人员的姓名是否为“John”。

```sql
person.name.equals("John")
```

## 不等于

`notEqualTo`函数用于确定字符串是否不等于指定的字符串。

**格式**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要与第一个字符串进行比较的字符串。 |

**示例**

以下PQL查询区分大小写确定人员的姓名不是“John”。

```sql
person.name.notEqualTo("John")
```

## 匹配

`matches`函数用于确定字符串是否与特定常规表达式匹配。 请参阅[此文档](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html)以了解有关常规表达式中匹配模式的更多信息。

**格式**

```sql
{STRING_1}.matches(STRING_2})
```

**示例**

以下PQL查询将确定人员的姓名开始是否带有“John”，但不区分大小写。

```sql
person.name.matches("(?i)^John")
```

## 常规表达式组

`regexGroup`函数用于根据提供的常规表达式提取特定信息。

**格式**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**示例**

以下PQL查询用于从电子邮件地址提取域名。

```sql
emailAddress.regexGroup("@(\w+)", 1)
```

## 后续步骤

现在您已经了解了字符串函数，可以在PQL查询中使用它们。 有关其他PQL函数的详细信息，请阅读[用户档案查询语语言概述](./overview.md)。


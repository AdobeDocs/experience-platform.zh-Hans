---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 字符串函数
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# 字符串函数

用户档案查询语(PQL)优惠函数，可简化与字符串的交互。 有关其他PQL函数的更多信息，请参阅 [用户档案查询语言概述](./overview.md)。

## 喜欢

该函 `like` 数用于确定字符串是否与指定的模式匹配。

**格式**

```sql
{STRING_1} like {STRING_2}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要与第一个字符串匹配的表达式。 有两个支持的特殊字符用于创建表达式: `%` 和 `_`。 <ul><li>`%` 用于表示零个或多个字符。</li><li>`_` 仅用于表示一个字符。</li></ul> |

**示例**

以下PQL查询检索包含模式“es”的所有城市。

```sql
city like "%es%"
```

## 开始于

该函 `startsWith` 数用于确定字符串是否与指定的子字符串开始。

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

函 `doesNotStartWith` 数用于确定字符串是否不与指定的子字符串开始。

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

该函 `endsWith` 数用于确定字符串是否以指定的子字符串结尾。

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

以下PQL查询区分大小写确定此人的电子邮件地址是否以“.com”结尾。

```sql
person.emailAddress.endsWith(".com")
```

## 不以

函 `doesNotEndWith` 数用于确定字符串是否以指定的子字符串结尾。

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

以下PQL查询根据大小写区分确定人员的电子邮件地址是否以“.com”结尾。

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Contains

函数 `contains` 用于确定字符串是否包含指定的子字符串。

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

函 `doesNotContain` 数用于确定字符串是否不包含指定的子字符串。

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

函 `equals` 数用于确定字符串是否等于指定的字符串。

**格式**

```sql
{STRING_1}.equals({STRING_2})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要与第一个字符串进行比较的字符串。 |

**示例**

以下PQL查询根据大小写区分确定此人的姓名是否为“John”。

```sql
person.name.equals("John")
```

## 不等于

函 `notEqualTo` 数用于确定字符串是否不等于指定的字符串。

**格式**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要与第一个字符串进行比较的字符串。 |

**示例**

以下PQL查询根据大小写区分确定此人的姓名不是“John”。

```sql
person.name.notEqualTo("John")
```

## 匹配

该函 `matches` 数用于确定字符串是否与特定常规表达式匹配。 请参阅本 [文档](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) ，了解有关常规表达式中匹配模式的更多信息。

**格式**

```sql
{STRING_1}.matches(STRING_2})
```

**示例**

以下PQL查询在不区分大小写的情况下确定此人的姓名开始是否为“John”。

```sql
person.name.matches("(?i)^John")
```

## 常规表达式组

该函 `regexGroup` 数用于基于所提供的常规表达式提取特定信息。

**格式**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**示例**

以下PQL查询用于从电子邮件地址中提取域名。

```sql
emailAddress.regexGroup("@(\w+)", 1)
```

## 后续步骤

现在您已经学习了字符串函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语概述](./overview.md)。


---
solution: Experience Platform
title: PQL字符串函数
description: Profile Query Language (PQL)提供了一些函数，可简化与字符串的交互。
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 5%

---

# 字符串函数

[!DNL Profile Query Language] (PQL)提供了一些函数，可简化与字符串的交互。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## 喜欢

`like`函数用于确定一个字符串是否与作为布尔值的指定模式匹配。

**格式**

```sql
{STRING_1} like {STRING_2}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要检查的字符串。 |
| `{STRING_2}` | 要与第一个字符串匹配的表达式。 创建表达式时支持使用两个特殊字符： `%`和`_`。 <ul><li>`%`用于表示零个或更多字符。</li><li>`_`只用于表示一个字符。</li></ul> |

**示例**

以下PQL查询检索包含模式“es”的所有城市。

```sql
city like "%es%"
```

## 开始于

`startsWith`函数用于确定一个字符串是否以指定的子字符串作为布尔值开头。

**格式**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写，的可选参数。 默认情况下，该参数设置为true。 |

**示例**

以下PQL查询区分大小写确定人员姓名是否以“Joe”开头。

```sql
person.name.startsWith("Joe")
```

## Does not start with

`doesNotStartWith`函数用于确定一个字符串是否不以指定的子字符串作为布尔值开头。

**格式**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写，的可选参数。 默认情况下，该参数设置为true。 |

**示例**

以下PQL查询以区分大小写的方式确定人员的姓名是否不以“Joe”开头。

```sql
person.name.doesNotStartWith("Joe")
```

## 结束于

`endsWith`函数用于确定一个字符串是否以指定的子字符串作为布尔值结尾。

**格式**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写，的可选参数。 默认情况下，该参数设置为true。 |

**示例**

以下PQL查询会区分大小写确定人员的电子邮件地址是否以“.com”结尾。

```sql
person.emailAddress.endsWith(".com")
```

## Does not end with

`doesNotEndWith`函数用于确定一个字符串是否不以指定的子字符串作为布尔值结尾。

**格式**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写，的可选参数。 默认情况下，该参数设置为true。 |

**示例**

以下PQL查询区分大小写确定人员的电子邮件地址是否不以“.com”结尾。

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Contains

`contains`函数用于确定一个字符串是否包含作为布尔值的指定子字符串。

**格式**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写，的可选参数。 默认情况下，该参数设置为true。 |

**示例**

以下PQL查询区分大小写确定人员的电子邮件地址是否包含字符串“2010@gm”。

```sql
person.emailAddress.contains("2010@gm")
```

## 不包含

`doesNotContain`函数用于确定一个字符串是否不包含作为布尔值的指定子字符串。

**格式**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写，的可选参数。 默认情况下，该参数设置为true。 |

**示例**

以下PQL查询区分大小写确定人员的电子邮件地址是否不包含字符串“2010@gm”。

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## 等于

`equals`函数用于确定一个字符串是否等于作为布尔值的指定字符串。

**格式**

```sql
{STRING_1}.equals({STRING_2})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要检查的字符串。 |
| `{STRING_2}` | 要与第一个字符串进行比较的字符串。 |

**示例**

以下PQL查询会区分大小写确定人员姓名是否为“John”。

```sql
person.name.equals("John")
```

## 不等于

`notEqualTo`函数用于确定一个字符串是否不等于作为布尔值的指定字符串。

**格式**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要检查的字符串。 |
| `{STRING_2}` | 要与第一个字符串进行比较的字符串。 |

**示例**

以下PQL查询区分大小写确定人员姓名是否为“John”。

```sql
person.name.notEqualTo("John")
```

## Matches

`matches`函数用于确定一个字符串是否与特定的正则表达式匹配。 请参阅[本文档](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html)，了解有关正则表达式中匹配模式作为布尔值的详细信息。

**格式**

```sql
{STRING_1}.matches(STRING_2})
```

**示例**

以下PQL查询在不区分大小写的情况下确定人员的姓名是否以“John”开头。

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>如果使用正则表达式函数（如`\w`），则&#x200B;**必须**&#x200B;对反斜杠字符进行转义。 因此，您必须包含额外的反斜杠并写入`\\w`，而不是只写入`\w`。

## 正则表达式组

`regexGroup`函数用于根据作为字符串提供的正则表达式提取特定信息。

**格式**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**示例**

以下PQL查询用于从电子邮件地址中提取域名。

```sql
emailAddress.regexGroup("@(\\w+)", 1)
```

>[!NOTE]
>
>如果使用正则表达式函数（如`\w`），则&#x200B;**必须**&#x200B;对反斜杠字符进行转义。 因此，您必须包含额外的反斜杠并写入`\\w`，而不是只写入`\w`。

## 后续步骤

现在，您已了解字符串函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读[Profile Query Language概述](./overview.md)。

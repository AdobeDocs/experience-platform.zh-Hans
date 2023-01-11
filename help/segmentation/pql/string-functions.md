---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；PQL;PQL；配置文件查询语言；字符串函数；字符串；
solution: Experience Platform
title: PQL字符串函数
description: 配置文件查询语言(PQL)提供了一些函数，可简化与字符串的交互。
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 6%

---

# 字符串函数

[!DNL Profile Query Language] (PQL)提供了一些函数，可简化与字符串的交互。 有关其他PQL函数的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md).

## 赞

的 `like` 函数来确定字符串是否与指定的模式匹配。

**格式**

```sql
{STRING_1} like {STRING_2}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要与第一个字符串匹配的表达式。 创建表达式时，有两个受支持的特殊字符： `%` 和 `_`. <ul><li>`%` 用于表示零个或多个字符。</li><li>`_` 仅用于表示一个字符。</li></ul> |

**示例**

以下PQL查询可检索包含模式“es”的所有城市。

```sql
city like "%es%"
```

## 开始于

的 `startsWith` 函数来确定字符串是否以指定的子字符串开头。

**格式**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写的可选参数。 默认情况下，此参数设置为true。 |

**示例**

以下PQL查询区分大小写，确定人员姓名以“Joe”开头。

```sql
person.name.startsWith("Joe")
```

## 开头不为

的 `doesNotStartWith` 函数来确定字符串是否不以指定的子字符串开头。

**格式**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写的可选参数。 默认情况下，此参数设置为true。 |

**示例**

以下PQL查询会区分大小写地确定人员姓名不以“Joe”开头。

```sql
person.name.doesNotStartWith("Joe")
```

## 结束于

的 `endsWith` 函数来确定字符串是否以指定的子字符串结尾。

**格式**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写的可选参数。 默认情况下，此参数设置为true。 |

**示例**

以下PQL查询会区分大小写地确定人员的电子邮件地址是否以“.com”结尾。

```sql
person.emailAddress.endsWith(".com")
```

## 不以结尾

的 `doesNotEndWith` 函数来确定字符串是否不以指定的子字符串结尾。

**格式**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写的可选参数。 默认情况下，此参数设置为true。 |

**示例**

以下PQL查询会区分大小写地确定人员的电子邮件地址是否以“.com”结尾。

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Contains

的 `contains` 函数来确定字符串是否包含指定的子字符串。

**格式**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写的可选参数。 默认情况下，此参数设置为true。 |

**示例**

以下PQL查询区分大小写地确定人员的电子邮件地址是否包含字符串“2010@gm”。

```sql
person.emailAddress.contains("2010@gm")
```

## 不包含

的 `doesNotContain` 函数来确定字符串是否不包含指定的子字符串。

**格式**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要在第一个字符串中搜索的字符串。 |
| `{BOOLEAN}` | 用于确定检查是否区分大小写的可选参数。 默认情况下，此参数设置为true。 |

**示例**

以下PQL查询会区分大小写地确定人员的电子邮件地址不包含字符串“2010@gm”。

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## 等于

的 `equals` 函数来确定字符串是否等于指定的字符串。

**格式**

```sql
{STRING_1}.equals({STRING_2})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要与第一个字符串比较的字符串。 |

**示例**

以下PQL查询会区分大小写地确定人员的姓名是否为“John”。

```sql
person.name.equals("John")
```

## 不等于

的 `notEqualTo` 函数来确定字符串是否不等于指定的字符串。

**格式**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 要执行检查的字符串。 |
| `{STRING_2}` | 要与第一个字符串比较的字符串。 |

**示例**

以下PQL查询会区分大小写地确定人员姓名不是“John”。

```sql
person.name.notEqualTo("John")
```

## 匹配

的 `matches` 函数来确定字符串是否与特定正则表达式匹配。 请参阅 [本文档](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) 有关正则表达式中匹配模式的更多信息。

**格式**

```sql
{STRING_1}.matches(STRING_2})
```

**示例**

以下PQL查询可确定人员姓名以“John”开头（不区分大小写），不区分大小写。

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>如果您使用的是正则表达式函数，例如 `\w`，您 **必须** 对反斜线字符进行转义。 所以，不要只写 `\w`，则必须包含额外的反斜杠和写入 `\\w`.

## 正则表达式组

的 `regexGroup` 函数用于根据提供的正则表达式提取特定信息。

**格式**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**示例**

以下PQL查询用于从电子邮件地址提取域名。

```sql
emailAddress.regexGroup("@(\\w+)", 1)
```

>[!NOTE]
>
>如果您使用的是正则表达式函数，例如 `\w`，您 **必须** 对反斜线字符进行转义。 所以，不要只写 `\w`，则必须包含额外的反斜杠和写入 `\\w`.

## 后续步骤

现在，您已经了解了字符串函数，接下来可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语言概述](./overview.md).

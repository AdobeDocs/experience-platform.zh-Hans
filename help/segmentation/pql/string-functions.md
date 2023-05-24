---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；pql；PQL；設定檔查詢語言；字串函式；字串；
solution: Experience Platform
title: PQL字串函式
description: 設定檔查詢語言(PQL)提供函式，讓使用者更輕鬆地與字串互動。
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 6%

---

# 字符串函数

[!DNL Profile Query Language] (PQL)提供可讓您更輕鬆與字串互動的函式。 如需其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概觀](./overview.md).

## 按讚

此 `like` 函式來判斷字串是否符合指定的模式。

**格式**

```sql
{STRING_1} like {STRING_2}
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 比對第一個字串的運算式。 建立運算式有兩個支援的特殊字元： `%` 和 `_`. <ul><li>`%` 用於表示零個或多個字元。</li><li>`_` 用於表示正好一個字元。</li></ul> |

**示例**

以下PQL查詢會擷取包含模式「es」的所有城市。

```sql
city like "%es%"
```

## 开始于

此 `startsWith` 函式來決定字串的開頭是否為指定的子字串。

**格式**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串中搜尋的字串。 |
| `{BOOLEAN}` | 選擇性引數，用來判斷檢查是否區分大小寫。 預設情況下，此項設為true。 |

**示例**

下列PQL查詢會區分大小寫，判斷個人的名稱是否以「Joe」開頭。

```sql
person.name.startsWith("Joe")
```

## 開頭不是

此 `doesNotStartWith` 函式來決定字串的開頭是否不是指定的子字串。

**格式**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串中搜尋的字串。 |
| `{BOOLEAN}` | 選擇性引數，用來判斷檢查是否區分大小寫。 預設情況下，此項設為true。 |

**示例**

下列PQL查詢會區分大小寫，判斷人員名稱是否以「Joe」開頭。

```sql
person.name.doesNotStartWith("Joe")
```

## 结束于

此 `endsWith` 函式用來決定字串的結尾是否為指定的子字串。

**格式**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串中搜尋的字串。 |
| `{BOOLEAN}` | 選擇性引數，用來判斷檢查是否區分大小寫。 預設情況下，此項設為true。 |

**示例**

下列PQL查詢會區分大小寫，判斷個人的電子郵件地址是否以「.com」結尾。

```sql
person.emailAddress.endsWith(".com")
```

## 結尾不是

此 `doesNotEndWith` 函式來決定字串的結尾是否不是指定的子字串。

**格式**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串中搜尋的字串。 |
| `{BOOLEAN}` | 選擇性引數，用來判斷檢查是否區分大小寫。 預設情況下，此項設為true。 |

**示例**

下列PQL查詢會區分大小寫，判斷個人的電子郵件地址是否不是以「.com」結尾。

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Contains

此 `contains` 函式來決定字串是否包含指定的子字串。

**格式**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串中搜尋的字串。 |
| `{BOOLEAN}` | 選擇性引數，用來判斷檢查是否區分大小寫。 預設情況下，此項設為true。 |

**示例**

下列PQL查詢會區分大小寫，判斷個人的電子郵件地址是否包含「2010@gm」字串。

```sql
person.emailAddress.contains("2010@gm")
```

## 不包含

此 `doesNotContain` 函式來決定字串是否不包含指定的子字串。

**格式**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 要在第一個字串中搜尋的字串。 |
| `{BOOLEAN}` | 選擇性引數，用來判斷檢查是否區分大小寫。 預設情況下，此項設為true。 |

**示例**

下列PQL查詢會區分大小寫，判斷個人的電子郵件地址是否不包含字串「2010@gm」。

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## 等于

此 `equals` 函式來判斷字串是否等於指定的字串。

**格式**

```sql
{STRING_1}.equals({STRING_2})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 要與第一個字串進行比較的字串。 |

**示例**

下列PQL查詢會區分大小寫來判斷個人的姓名是否為「John」。

```sql
person.name.equals("John")
```

## 不等於

此 `notEqualTo` 函式來判斷字串是否不等於指定的字串。

**格式**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{STRING_1}` | 執行檢查的字串。 |
| `{STRING_2}` | 要與第一個字串進行比較的字串。 |

**示例**

下列PQL查詢會區分大小寫來判斷個人的姓名是否為「John」。

```sql
person.name.notEqualTo("John")
```

## 匹配

此 `matches` 函式來判斷字串是否符合特定的規則運算式。 請參閱 [本檔案](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) 以取得規則運算式中比對模式的詳細資訊。

**格式**

```sql
{STRING_1}.matches(STRING_2})
```

**示例**

下列PQL查詢會在不區分大小寫的情況下，判斷個人的名字是否以「John」開頭。

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>如果您使用規則運算式函式，例如 `\w`，您 **必須** 逸出反斜線字元。 因此，與其直接撰寫 `\w`，您必須加入額外的反斜線並寫入 `\\w`.

## 規則運算式群組

此 `regexGroup` 函式是根據提供的規則運算式來擷取特定資訊。

**格式**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**示例**

以下PQL查詢用於從電子郵件地址中擷取網域名稱。

```sql
emailAddress.regexGroup("@(\\w+)", 1)
```

>[!NOTE]
>
>如果您使用規則運算式函式，例如 `\w`，您 **必須** 逸出反斜線字元。 因此，與其直接撰寫 `\w`，您必須加入額外的反斜線並寫入 `\\w`.

## 后续步骤

現在您已瞭解字串函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱 [設定檔查詢語言概觀](./overview.md).

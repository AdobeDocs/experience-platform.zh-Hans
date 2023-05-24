---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；pql；PQL；設定檔查詢語言；布林函式；布林值；
solution: Experience Platform
title: PQL布林函式
description: 布林函式可用來針對設定檔查詢語言(PQL)中的不同元素執行布林邏輯。
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 5%

---

# 布林函式

布林函式是用來對中的不同元素執行布林邏輯 [!DNL Profile Query Language] (PQL)。  如需其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概觀](./overview.md).

## 和

此 `and` 函式用來建立邏輯結合。

**格式**

```sql
{QUERY} and {QUERY}
```

**示例**

以下PQL查詢將傳回所有以加拿大為母國且出生年份為1985年的人。

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## 或

此 `or` 函式用來建立邏輯分離。

**格式**

```sql
{QUERY} or {QUERY}
```

**示例**

以下PQL查詢將傳回所有以加拿大為母國或1985年出生年份為出生地的人。

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## 不为

此 `not` (或 `!`)函式來建立邏輯否定。

**格式**

```sql
not ({QUERY})
!({QUERY})
```

**示例**

以下PQL查詢將傳回所有沒有其母國為加拿大的人。

```sql
not (homeAddress.countryISO = "CA")
```

## 如果

此 `if` 函式用於解析運算式，具體取決於指定的條件是否為true。

**格式**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | 正在測試的布林運算式。 |
| `{TRUE_EXPRESSION}` | 其值將用於下列情況的運算式： `{TEST_EXPRESSION}` 為true。 |
| `{FALSE_EXPRESSION}` | 其值將用於下列情況的運算式： `{TEST_EXPRESSION}` 為false。 |

**示例**

下列PQL查詢會將值設為 `1` 如果母國為加拿大，且 `2` 如果母國不是加拿大。

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## 后续步骤

現在您已瞭解布林函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱 [設定檔查詢語言概觀](./overview.md).

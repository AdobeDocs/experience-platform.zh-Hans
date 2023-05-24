---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；pql；PQL；設定檔查詢語言；比較函式；比較；
solution: Experience Platform
title: PQL比較函式
description: 比較函式可用來比較不同運算式和值之間的差異，並據此傳回「true」或「false」。
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 9%

---

# 比較函式

比較函式可用來比較不同運算式和值之間的差異，並傳回 `true` 或 `false` 因此， 如需其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概觀](./overview.md).

## 等于

此 `=` （等於）函式檢查一個值或運算式是否等於另一個值或運算式。

**格式**

```sql
{EXPRESSION} = {VALUE}
```

**示例**

下列PQL查詢會檢查住家地址所在的國家/地區是否位於加拿大。

```sql
homeAddress.countryISO = "CA"
```

## 不等于

此 `!=` （不等於）函式檢查一個值或運算式是否為 **not** 等於另一個值或運算式。

**格式**

```sql
{EXPRESSION} != {VALUE}
```

**示例**

下列PQL查詢會檢查住家地址所在的國家/地區是否不在加拿大。

```sql
homeAddress.countryISO != "CA"
```

## 大于

此 `>` （大於）函式來檢查第一個值是否大於第二個值。

**格式**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**示例**

以下PQL查詢定義生日未在1月或2月的人。

```sql
person.birthMonth > 2
```

## 大于或等于

此 `>=` （大於或等於）函式來檢查第一個值是否大於或等於第二個值。

**格式**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**示例**

以下PQL查詢定義生日未在1月或2月的人。

```sql
person.birthMonth >= 3
```

## 小于

此 `<` （小於）比較函式用於檢查第一個值是否小於第二個值。

**格式**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**示例**

以下PQL查詢定義生日在一月的人員。

```sql
person.birthMonth < 2
```

## 小于或等于

此 `<=` （小於或等於）比較函式用於檢查第一個值是否小於或等於第二個值。

**格式**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**示例**

以下PQL查詢定義生日在一月或二月的人員。

```sql
person.birthMonth <= 2
```

## 后续步骤

現在您已瞭解比較函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱 [設定檔查詢語言概觀](./overview.md).

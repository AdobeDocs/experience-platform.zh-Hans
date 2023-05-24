---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；pql；PQL；設定檔查詢語言；算術函式；算術；
solution: Experience Platform
title: PAL算術函式
description: 算術函式用於對設定檔查詢語言(PQL)中的值執行基本計算。
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 5%

---

# 算术函数

算術函式用於對中的值進行基本計算 [!DNL Profile Query Language] (PQL)。 如需其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概觀](./overview.md).

## Add

此 `+` （加法）函式用於找出兩個引數運算式的總和。

**格式**

```sql
{NUMBER} + {NUMBER}
```

**示例**

下列PQL查詢會加總兩個不同產品的價格。

```sql
product1.price + product2.price
```

## 乘

此 `*` （乘法）函式用於尋找兩個引數運算式的乘積。

**格式**

```sql
{NUMBER} * {NUMBER}
```

**示例**

下列PQL查詢會尋找存貨的產品與產品價格，以尋找產品的總值。

```sql
product.inventory * product.price
```

## 減法

此 `-` （減法）函式可用來找出兩個引數運算式的差異。

**格式**

```sql
{NUMBER} - {NUMBER}
```

**示例**

下列PQL查詢會找出兩個不同產品之間的價格差異。

```sql
product1.price - product2.price
```

## 除

此 `/` (division)函式用於尋找兩個引數運算式的商。

**格式**

```sql
{NUMBER} / {NUMBER}
```

**示例**

下列PQL查詢會找出已售出產品總數與已賺取金額總數之間的商數，以檢視每個專案的平均成本。

```sql
totalProduct.price / totalProduct.sold
```

## 餘數

此 `%` （模數/餘數）函式用來找出兩個引數運算式相除後的餘數。

**格式**

```sql
{NUMBER} % {NUMBER}
```

**示例**

以下PQL查詢會檢查個人的年齡是否可被5歲整除。

```sql
person.age % 5 = 0
```

## 后续步骤

現在您已了解算術函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱 [設定檔查詢語言概觀](./overview.md).

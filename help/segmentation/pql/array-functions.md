---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；pql；PQL；設定檔查詢語言；陣列函式；陣列；
solution: Experience Platform
title: 陣列、清單和設定PQL函式
description: 設定檔查詢語言(PQL)提供的功能可讓您更輕鬆地與陣列、清單和字串互動。
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 5%

---

# 陣列、清單和設定函式

[!DNL Profile Query Language] (PQL)提供的功能可讓您更輕鬆地與陣列、清單和字串互動。 如需其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概觀](./overview.md).

## 在

此 `in` 函式用來判斷專案是否為陣列或清單的成員。

**格式**

```sql
{VALUE} in {ARRAY}
```

**示例**

以下PQL查詢定義在3月、6月或9月有生日的人。

```sql
person.birthMonth in [3, 6, 9]
```

## 不在……之內

此 `notIn` 函式用來判斷專案是否不是陣列或清單的成員。

>[!NOTE]
>
>此 `notIn` 函式 *另外* 確保這兩個值都不等於null。 因此，結果並非完全否定 `in` 函式。

**格式**

```sql
{VALUE} notIn {ARRAY}
```

**示例**

以下PQL查詢定義生日不是3月、6月或9月的人。

```sql
person.birthMonth notIn [3, 6, 9]
```

## 相交

此 `intersects` 函式用來判斷兩個陣列或清單是否至少有一個通用成員。

**格式**

```sql
{ARRAY}.intersects({ARRAY})
```

**示例**

以下PQL查詢定義其最愛顏色至少包含紅色、藍色或綠色其中一種的人員。

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## 交集

此 `intersection` 函式用來決定兩個陣列或清單的一般成員。

**格式**

```sql
{ARRAY}.intersection({ARRAY})
```

**示例**

以下PQL查詢定義人員1和人員2是否都有最喜愛的紅色、藍色和綠色。

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## 子集：

此 `subsetOf` 函式來判斷特定陣列（陣列A）是否為另一個陣列（陣列B）的子集。 換句話說，陣列A中的所有元素都是陣列B的元素。

**格式**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**示例**

以下PQL查詢會定義造訪過其所有最喜愛城市的人。

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## 超集

此 `supersetOf` 函式來判斷特定陣列（陣列A）是否為另一個陣列（陣列B）的超集。 換句話說，陣列A包含陣列B中的所有元素。

**格式**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**示例**

以下PQL查詢會定義至少吃過一次壽司和比薩的人。

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## 包含

此 `includes` 函式用於確定陣列或清單是否包含給定專案。

**格式**

```sql
{ARRAY}.includes({ITEM})
```

**示例**

以下PQL查詢定義其最愛顏色包含紅色的人。

```sql
person.favoriteColors.includes("red")
```

## 相異

此 `distinct` 函式用於從陣列或清單中移除重複值。

**格式**

```sql
{ARRAY}.distinct()
```

**示例**

下列PQL查詢會指定在多個商店下訂單的人。

```sql
person.orders.storeId.distinct().count() > 1
```

## 分組依據

此 `groupBy` 函式用來根據運算式的值，將陣列或清單的值分割成群組。

**格式**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ARRAY}` | 要分組的陣列或清單。 |
| `{EXPRESSION}` | 對應陣列或傳回清單中每個專案的運算式。 |

**示例**

下列PQL查詢會將下訂單的存放庫所依據的所有訂單分組。

```sql
orders.groupBy(storeId)
```

## 过滤器

此 `filter` 函式用於根據運算式篩選陣列或清單。

**格式**

```sql
{ARRAY}.filter({EXPRESSION})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ARRAY}` | 要篩選的陣列或清單。 |
| `{EXPRESSION}` | 篩選依據的運算式。 |

**示例**

以下PQL查詢定義所有21歲或以上的人。

```sql
person.filter(age >= 21)
```

## 地图

此 `map` 函式用於將運算式套用至指定陣列中的每個專案，以建立新陣列。

**格式**

```sql
array.map(expression)
```

**示例**

下列PQL查詢會建立新的數字陣列，並對原始數字的值進行平方。

```sql
numbers.map(square)
```

## 第一個 `n` 在陣列中 {#first-n}

此 `topN` 函式用於傳回第一個 `N` 陣列中的專案（當根據給定的數值運算式依遞增順序排序時）。

**格式**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ARRAY}` | 要排序的陣列或清單。 |
| `{VALUE}` | 排序陣列或清單的屬性。 |
| `{AMOUNT}` | 要傳回的專案數。 |

**示例**

下列PQL查詢會傳回價格最高的前五個訂單。

```sql
orders.topN(price, 5)
```

## 上次 `n` 在陣列中

此 `bottomN` 函式用於傳回最後 `N` 陣列中的專案（當根據給定的數值運算式依遞增順序排序時）。

**格式**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| 参数 | 描述 |
| --------- | ----------- | 
| `{ARRAY}` | 要排序的陣列或清單。 |
| `{VALUE}` | 排序陣列或清單的屬性。 |
| `{AMOUNT}` | 要傳回的專案數。 |

**示例**

下列PQL查詢會傳回價格最低的前五個訂單。

```sql
orders.bottomN(price, 5)
```

## 第一個專案

此 `head` 函式用於傳回陣列或清單中的第一個專案。

**格式**

```sql
{ARRAY}.head()
```

**示例**

下列PQL查詢會傳回價格最高的前五個訂單中的第一個。 更多關於「 」的資訊 `topN` 函式位於 [第一個 `n` 在陣列中](#first-n) 區段。

```sql
orders.topN(price, 5).head()
```

## 后续步骤

現在您已瞭解陣列、清單和設定函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱 [設定檔查詢語言概觀](./overview.md).

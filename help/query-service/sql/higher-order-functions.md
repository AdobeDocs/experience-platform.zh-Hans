---
title: 使用高阶函数管理阵列和映射数据类型
description: 了解如何使用查询服务中的高位函数管理数组并映射数据类型。 示例与常见用例一起提供。
exl-id: dec4e4f6-ad6b-4482-ae8c-f10cc939a634
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# 使用高阶函数管理阵列和映射数据类型

使用本指南了解高阶函数如何处理复杂的数据类型，如数组和映射。 这些函数免除了分解数组、执行函数以及合并结果的需要。 高阶函数对于分析或处理时间序列数据集和分析特别有用，这些数据集通常具有复杂的嵌套结构、数组、映射和多种用例。

以下用例列表包含高阶数组和映射操作函数的示例。

## 使用转换按n调整总价 {#adjust-price-total}

`transform(array<T>, function<T, U>): array<U>`

上面的代码片段将一个函数应用于数组的每个元素，并返回一个新的转换元素数组。 具体来说，`transform`函数接受类型为T的数组，并将每个元素从类型T转换为类型U。然后返回U类型的数组。实际类型T和U取决于变换函数的具体用法。

`transform(array<T>, function<T, Int, U>): array<U>`

此数组转换函数与上一个示例类似，但此函数有两个参数。 此函数中的第二个参数除了被转换之外，还接收数组中元素的索引。

**示例**

下面的SQL示例演示了此用例。 查询从指定的表中检索有限的行集，通过将每个项的`productListItems`属性乘以73来转换`priceTotal`数组。 结果包括`_id`、`productListItems`和转换后的`price_in_inr`列。 选择基于特定的时间戳范围。

```sql
SELECT _id,
       productListItems,
       Transform(productListItems, value -> value.priceTotal * 73) AS
       price_in_inr
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**结果**

此SQL的结果将与下面所示的结果类似。

```console
 productListItems | price_in_inr
|-------------------+----------------
(8376, NULL, NULL) | 611448.0
{(Burbank Hills Jeans, NULL, NULL), (Thermomax Steel, NULL, NULL), (Bruin Point Shearling Boots, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL), (Timberline Survival Knife, NULL, NULL), (Thermomax Steel, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Lost Prospector Beanie, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL)} | {0.0,0.0.0.0,0,0,0,0,0,0,0,0,0,0,0,0,0.0}
(84763,NULL, NULL) | 6187699.0
(843765, NULL, NULL) | 6.1594845E7
(199684, NULL, NULL) | 1.4576932E7

(10 rows)
```

## 使用存在以发现是否存在具有特定SKU的产品 {#confirm-product-exists}

`exists(array<T>, function<T, boolean>): boolean`

在上面的代码片段中，`exists`函数应用于数组的每个元素并返回一个布尔值。 布尔值指示数组中是否存在满足指定条件的一个或多个元素。 在这种情况下，它确认是否存在具有特定SKU的产品。

**示例**

在以下SQL示例中，查询从`productListItems`表中提取`geometrixxx_999_xdm_pqs_1batch_10k_rows`，并评估`123679`数组中是否存在SKU等于`productListItems`的元素。 然后，它根据特定时间戳范围筛选结果，并将最终结果限制为10行。

```sql
SELECT productListItems
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE EXISTS( productListItems, value -> value.sku == 123679)
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')limit 10;
```

**结果**

此SQL的结果将与下面所示的结果类似。

```console
productListItems
|-----------------
{(123679, NULL,NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL,NULL)}
{(123679,NULL, NULL)}

(10 rows)
```

## 使用过滤器查找SKU > 100000的产品 {#find-specific-products}

`filter(array<T>, function<T, boolean>): array<T>`

此函数根据给定条件筛选元素数组，该条件将每个元素计算为一个布尔值。 然后，它返回一个新数组，该数组仅包含条件返回true值的元素。

**示例**

下面的查询选择`productListItems`列，应用过滤器以仅包含SKU大于100000的元素，并将结果集限制为特定时间戳范围内的行。 然后在输出中将筛选后的数组别名为`_filter`。

```sql
SELECT productListItems,
    Filter(productListItems, value -> value.sku > 100000) AS _filter
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**结果**

此SQL的结果将与下面所示的结果类似。

```console
productListItems | _filter
|-----------------+---------
(123679, NULL, NULL) (123679, NULL, NULL)
(1346, NULL, NULL) |
(98347, NULL, NULL) |
(176015, NULL, NULL) | (176015, NULL, NULL)

(10 rows)
```

## 使用聚合计算与特定ID关联的所有产品列表项的SKU总和，并将结果总计加倍 {#sum-specific-skus-and-double-the-resulting-total}

`aggregate(array<T>, A, function<A, T, A>[, function<A, R>]): R`

此聚合操作将二元运算符应用于初始状态和数组中的所有元素。 它还会将多个值降为单个状态。 经过此缩减之后，最终状态通过使用finish函数转换为最终结果。 finish函数将二元算符应用于所有数组元素后得到的最后一个状态取出来，并对它做一些处理以产生最终结果。

**示例**

此查询示例计算给定时间戳范围内`productListItems`数组的最大SKU值，并将结果加倍。 输出包括原始`productListItems`数组和计算的`max_value`。

```sql
SELECT productListItems,
aggregate(productListItems, 0, (acc, value) ->
case
WHEN (
value.sku > acc) THEN cast(value.sku AS int)
ELSE cast(acc AS int)
END, acc -> acc * 2) AS max_value
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 50;
```

**结果**

此SQL的结果将与下面所示的结果类似。

```console
productListItems | max_value
|-----------------+---------
(123679, NULL, NULL) | 247358
(1346,NULL, NULL) | 2692
(98347, NULL, NULL) | 196694
(176015, NULL, NULL) | 352030

(10 rows)
```

## 使用zip_with为产品列表中的所有项目分配序列号 {#assign-a-sequence-number}

`zip_with(array<T>, array<U>, function<T, U, R>): array<R>`

此代码片段将两个数组的元素组合为一个新数组。 该操作在阵列的每个元素上独立地执行，并产生值对。 如果一个数组较短，则添加空值以匹配较长数组的长度。 这发生在应用函数之前。

**示例**

以下查询使用`zip_with`函数从两个数组创建值对。 通过将`productListItems`数组中的SKU值添加到使用`Sequence`函数生成的整数序列来执行此操作。 该结果将与原始`productListItems`列一起选择，并根据时间戳范围进行限制。

```sql
SELECT productListItems,
zip_with(Sequence(1,5), Transform(productListItems, p -> p.sku), (x,y) -> struct(x, y)) AS zip_with
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**结果**

此SQL的结果将与下面所示的结果类似。

```console
productListItems     | zip_with
|---------------------+---------
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(123679, NULL, NULL) | {(1,123679), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3, NULL),(4,NULL), (5,NULL)}
(1346,NULL, NULL)    | {(1,1346), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(98347, NULL, NULL)  | {(1,98347), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
(176015, NULL, NULL) | {(1,176015),(2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}

(10 rows)
```

## 使用map_from_entries为产品列表中的每个项目分配序列号，并作为映射获取最终结果 {#assign-a-sequence-number-return-result-as-map}

`map_from_entries(array<struct<K, V>>): map<K, V>`

此代码片段将键值对数组转换为映射。 在处理键值对数据（可从更有条理、效率更高的结构中受益）时，此插件非常有用。

**示例**

以下查询从序列和productListItems数组创建值对，使用map_from_entries将这些值对转换为映射，然后选择原始productListItems列以及新创建的map_from_entries列。 系统会根据指定的时间戳范围对结果进行过滤和限制。

```sql
SELECT productListItems,      map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))) AS map_from_entries
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > to_timestamp('2017-11-01 00:00:00')
AND    timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**结果**

此SQL的结果将与下面所示的结果类似。

```console
productListItems     | map_from_entries
|---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## 使用map_form_arrays将序列号分配给产品列表中的项，并将结果作为映射返回 {#assign-sequence-numbers-to-items-return-the-result-as-a-map}

`map_form_arrays(array<K>, array<V>): map<K, V>`

`map_form_arrays`函数使用两个数组的配对值创建映射。

>[!IMPORTANT]
>
>键中应该没有空元素。

**示例**

下面的SQL创建了一个映射，其中键是使用`Sequence`函数生成的顺序数字，值是来自`productListItems`数组的元素。 查询选择`productListItems`列并使用`Map_from_arrays`函数根据生成的数字序列和数组的元素创建映射。 结果限制为10行，并根据时间戳范围进行筛选。

```sql
SELECT productListItems,
       Map_from_arrays(Sequence(1, Size(productListItems)), productListItems) AS
       map_from_arrays
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  Size(productListItems) > 0
       AND timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**结果**

此SQL的结果将与下面所示的结果类似。

```console
productListItems     | map_from_entries
|---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## 使用map_concat将两个映射串联为单个映射 {#concatenate-two-maps-into-as-single-map}

`map_concat(map<K, V>, ...): map<K, V>`

上述代码片段中的`map_concat`函数将多个映射作为参数，并返回一个新的映射，该映射将来自输入映射的所有键值对组合在一起。 该函数将多个映射串联为单个映射，并且生成的映射包括来自输入映射的所有键值对。

**示例**

下面的SQL创建一个映射，其中`productListItems`中的每个项都与一个序列号关联，该序列号随后与另一个映射关联，其中键在特定序列范围内生成。

```sql
SELECT productListItems,
      map_concat(           
         map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))),
         map_from_arrays(sequence(size(productListItems) + 1, size(productListItems) + size(productListItems)), productListItems) )
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE size(productListItems) > 0
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**结果**

此SQL的结果将与下面所示的结果类似。

```console
productListItems     | map_from_entries
|---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)",2 -> "(123679, NULL, NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)",2 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)",2 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)",2 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)",2 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)",2 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)",2 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)",2 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## 使用element_at在标识映射中检索与“AAID”对应的值以进行进一步计算 {#retrieve-a-corresponding-value}

`element_at(array<T>, Int): T / element_at(map<K, V>, K): V`

对于数组，此代码片段返回指定（从1开始）索引处的元素，或与映射中键关联的值。 如果索引小于0，则访问从最后一个到第一个的元素，如果索引超过数组的长度，则返回null。

对于映射，它会返回给定键的值，或者如果该键未包含在映射中，则返回null。

**示例**

查询从表`identitymap`中选择`geometrixxx_999_xdm_pqs_1batch_10k_rows`列，并为每一行提取与键`AAID`关联的值。 结果仅限于指定时间戳范围内的行，而查询将输出限制为10行。

```sql
SELECT identitymap,
              Element_at(identitymap, 'AAID')
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**结果**

此SQL的结果将与下面所示的结果类似。

```console
                                                                  identitymap                                            |  element_at(identitymap, AAID) 
|-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            | (3617FBB942466D79-5433F727AD6A0AD, false) 
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] | (533F56A682C059B1-396437F68879F61D, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             | (6A60527B9D66CCB9-29638A632B45E9, false) 
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           | (64FB4DC317E21B59-2A23602D234647E7, false) 
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           | (2E70E8CF6DB1DE86-270E55BBBA58B9C1, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           | (1CFB3297C3146F2F-28D6902A610BA3B1, false) 
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           | (533F56A682C059B1-396437F68879F61D, false) 
(10 rows)
```

## 使用基数查找标识映射中的标识数 {#find-the-number-of-identities-in-the-identity-map}

`cardinality(array<T>): Int / cardinality(map<K, V>): Int`

此代码片段返回给定数组或映射的大小并提供别名。 如果值为null，则返回–1。

**示例**

下面的查询检索`identitymap`列，`Cardinality`函数计算`identitymap`内每个映射中的元素数。 结果限制为10行，并根据指定的时间戳范围进行筛选。

```sql
SELECT identitymap,
       Cardinality(identitymap)
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**结果**

此SQL的结果将与下面所示的结果类似。

```console
                                                                  identitymap                                            |  size(identitymap) 
|-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            |      2  
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             |      2  
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           |      2  
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           |      2  
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           |      2  
(10 rows)
```

## 使用array_distinct查找productListItems中的不同元素 {#find-distinct-elements}

`array_distinct(array<T>): array<T>`

上面的代码片段会从给定的数组中删除重复的值。

**示例**

下面的查询选择`productListItems`列，从数组中移除任何重复项，并根据指定的时间戳范围将输出限制为10行。

```sql
SELECT productListItems,
              Array_distinct(productListItems)
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**结果**

此SQL的结果将与下面所示的结果类似。

```console
productListItems     | array_distinct(productListItems)
|---------------------+---------------------------------
                     |
(123679, NULL, NULL) | (123679, NULL, NULL)
                     |
                     |
(1346,NULL, NULL)    | (1346,NULL, NULL)
                     |
(98347, NULL, NULL)  | (98347, NULL, NULL)
                     |
(176015, NULL, NULL) | (176015, NULL, NULL)
                     |

(10 rows)
```

### 其他高阶函数 {#additional-higher-order-functions}

以下高阶函数的示例在“检索类似记录”用例中进行说明。 该文档的相关部分提供了每个函数用法的示例和说明。

[`transform`函数示例](../use-cases/retrieve-similar-records.md#length-adjustment)涵盖了产品列表的标记化。

[`filter`函数示例](../use-cases/retrieve-similar-records.md#filter-results)演示了从文本数据中更精细、更精确的相关信息提取。

[`reduce`函数](../use-cases/retrieve-similar-records.md#higher-order-function-solutions)提供了一种导出累计值或汇总的方法，这些值或汇总在各种分析和计划流程中可能至关重要。

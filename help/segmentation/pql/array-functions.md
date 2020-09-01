---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;array functions;array;
solution: Experience Platform
title: 数组、列表和设置函数
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 5%

---


# 数组、列表和设置函数

[!DNL Profile Query Language] (PQL)优惠函数可简化与数组、列表和字符串的交互。 有关其他PQL功能的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md)。

## 输入

函 `in` 数用于确定项是否为数组或列表的成员。

**Format**

```sql
{VALUE} in {ARRAY}
```

**示例**

以下PQL查询定义三月、六月或九月的生日人群。

```sql
person.birthMonth in [3, 6, 9]
```

## 不在

该 `notIn` 函数用于确定项是否不是数组或列表的成员。

>[!NOTE]
>
>函 `notIn` 数 *还确保* 两个值均不等于null。 因此，结果不是函数的精确取 `in` 反。

**Format**

```sql
{VALUE} notIn {ARRAY}
```

**示例**

以下PQL查询定义了不在3月、6月或9月的生日。

```sql
person.birthMonth notIn [3, 6, 9]
```

## Intersects

该函 `intersects` 数用于确定两个阵列或列表是否具有至少一个公共成员。

**Format**

```sql
{ARRAY}.intersects({ARRAY})
```

**示例**

以下PQL查询定义其喜爱的颜色至少包括红色、蓝色或绿色之一的人。

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## 交集

该函 `intersection` 数用于确定两个阵列或列表的公共成员。

**Format**

```sql
{ARRAY}.intersection({ARRAY})
```

**示例**

以下PQL查询定义人物1和人物2是否都具有最喜爱的红色、蓝色和绿色。

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## 子集

该函 `subsetOf` 数用于确定特定阵列（阵列A）是否是另一阵列（阵列B）的子集。 换言之，数组A中的所有元素都是数组B的元素。

**Format**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**示例**

以下PQL查询定义访问过其所有喜爱城市的人员。

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## 超集

该函 `supersetOf` 数用于确定特定阵列（阵列A）是否是另一阵列（阵列B）的超集。 换言之，数组A包含数组B中的所有元素。

**Format**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**示例**

以下PQL查询定义了至少吃过一次寿司和比萨的人。

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## 包括

函 `includes` 数用于确定数组或列表是否包含给定项。

**Format**

```sql
{ARRAY}.includes({ITEM})
```

**示例**

以下PQL查询定义其喜爱颜色包括红色的人。

```sql
person.favoriteColors.includes("red")
```

## Distinct

该函 `distinct` 数用于从数组或重复中删除列表值。

**Format**

```sql
{ARRAY}.distinct()
```

**示例**

以下PQL查询指定在多个商店下订单的人员。

```sql
person.orders.storeId.distinct().count() > 1
```

## 分组依据

该函 `groupBy` 数用于根据列表的值将数组或表达式的值划分成组。

**Format**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ARRAY}` | 要分组的数组或列表。 |
| `{EXPRESSION}` | 返回的表达式映射数组或列表中的每个项。 |

**示例**

以下PQL查询将存储订单的所有订单分组。

```sql
orders.groupBy(storeId)
```

## 过滤器

该函 `filter` 数用于根据列表来过滤数组或表达式。

**Format**

```sql
{ARRAY}.filter({EXPRESSION})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ARRAY}` | 要筛选的数组或列表。 |
| `{EXPRESSION}` | 要筛选的表达式。 |

**示例**

以下PQL查询定义所有21岁或以上的人。

```sql
person.filter(age >= 21)
```

## 地图

该函 `map` 数用于通过对给定数组中的每个项目应用表达式来创建新数组。

**Format**

```sql
array.map(expression)
```

**示例**

以下PQL查询将创建原始数字值的新数组和平方。

```sql
numbers.map(square)
```

## 阵列 `n` 中的第一个 {#first-n}

该函 `topN` 数用于返回数组中 `N` 的第一个项，当它基于给定的数字表达式按升序排序时。

**Format**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ARRAY}` | 要排序的数组或列表。 |
| `{VALUE}` | 要对数组或列表排序的属性。 |
| `{AMOUNT}` | 要返回的项目数。 |

**示例**

以下PQL查询返回价格最高的前五个订单。

```sql
orders.topN(price, 5)
```

## 阵列 `n` 中的最后一个

函数 `bottomN` 用于返回数组中的 `N` 最后一个项，当该项基于给定的数字表达式按升序排序时。

**Format**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| 参数 | 描述 |
| --------- | ----------- | 
| `{ARRAY}` | 要排序的数组或列表。 |
| `{VALUE}` | 要对数组或列表排序的属性。 |
| `{AMOUNT}` | 要返回的项目数。 |

**示例**

以下PQL查询返回价格最低的前五个订单。

```sql
orders.bottomN(price, 5)
```

## 第一项

函 `head` 数用于返回数组或列表中的第一个项。

**Format**

```sql
{ARRAY}.head()
```

**示例**

以下PQL查询返回价格最高的前五大订单中的第一个。 有关该函数的 `topN` 更多信息，请参 [阅 `n` 数组中的第一节](#first-n) 。

```sql
orders.topN(price, 5).head()
```

## 后续步骤

您已经了解了阵列、列表和设置功能，现在可以在PQL查询中使用它们。 有关其他PQL功能的详细信息，请阅读 [用户档案查询语概述](./overview.md)。

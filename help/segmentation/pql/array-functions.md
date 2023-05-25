---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；pql；PQL；配置文件查询语言；数组函数；数组；
solution: Experience Platform
title: 数组、列表和设置PQL函数
description: 配置文件查询语言(PQL)提供了一些功能，使与数组、列表和字符串的交互更轻松。
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 5%

---

# 数组、列表和设置函数

[!DNL Profile Query Language] (PQL)提供了一些功能，使与数组、列表和字符串的交互更轻松。 有关其他PQL函数的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md).

## In

此 `in` 函数用于确定一个项是否是一个数组或列表的成员。

**格式**

```sql
{VALUE} in {ARRAY}
```

**示例**

以下PQL查询定义3月、6月或9月生日的用户。

```sql
person.birthMonth in [3, 6, 9]
```

## 不在

此 `notIn` 函数用于确定一个项是否不是数组或列表的成员。

>[!NOTE]
>
>此 `notIn` 函数 *另外* 确保这两个值都不等于null。 因此，结果并不是完全否定 `in` 函数。

**格式**

```sql
{VALUE} notIn {ARRAY}
```

**示例**

以下PQL查询定义生日不在3月、6月或9月的人员。

```sql
person.birthMonth notIn [3, 6, 9]
```

## 相交

此 `intersects` 函数用于确定两个数组或列表是否至少有一个公共成员。

**格式**

```sql
{ARRAY}.intersects({ARRAY})
```

**示例**

以下PQL查询定义其最喜爱颜色至少包括红色、蓝色或绿色之一的人员。

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## 交集

此 `intersection` 函数用于确定两个数组或列表的常用成员。

**格式**

```sql
{ARRAY}.intersection({ARRAY})
```

**示例**

以下PQL查询定义人员1和人员2是否都具有最喜爱的红色、蓝色和绿色。

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## 子集

此 `subsetOf` 函数用于确定一个特定数组（数组A）是否是另一个数组（数组B）的子集。 换句话说，数组A中的所有元素都是数组B的元素。

**格式**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**示例**

以下PQL查询定义访问过其所有最喜爱城市的人。

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## 超集

此 `supersetOf` 函数用于确定一个特定数组（数组A）是否是另一个数组（数组B）的超集。 换句话说，该数组A包含数组B中的所有元素。

**格式**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**示例**

以下PQL查询定义至少吃过一次寿司和比萨的人。

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## 包括

此 `includes` 函数用于确定一个数组或列表是否包含给定项。

**格式**

```sql
{ARRAY}.includes({ITEM})
```

**示例**

以下PQL查询定义其最喜爱颜色包括红色的人员。

```sql
person.favoriteColors.includes("red")
```

## Distinct

此 `distinct` 函数用于从数组或列表中删除重复的值。

**格式**

```sql
{ARRAY}.distinct()
```

**示例**

以下PQL查询指定在多个商店下订单的人员。

```sql
person.orders.storeId.distinct().count() > 1
```

## 分组方式

此 `groupBy` 函数用于根据表达式的值将数组或列表的值分区为组。

**格式**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ARRAY}` | 要分组的数组或列表。 |
| `{EXPRESSION}` | 映射返回的数组或列表中的每个项的表达式。 |

**示例**

以下PQL查询将存储订单的所有订单分组。

```sql
orders.groupBy(storeId)
```

## 过滤器

此 `filter` 函数用于根据表达式筛选数组或列表。

**格式**

```sql
{ARRAY}.filter({EXPRESSION})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ARRAY}` | 要过滤的数组或列表。 |
| `{EXPRESSION}` | 筛选依据的表达式。 |

**示例**

以下PQL查询定义所有21岁或以上的人。

```sql
person.filter(age >= 21)
```

## 地图

此 `map` 函数用于通过将表达式应用于给定数组中的每个项来创建新数组。

**格式**

```sql
array.map(expression)
```

**示例**

以下PQL查询创建一个新的数字数组，并对原始数字的值进行平方。

```sql
numbers.map(square)
```

## 第一个 `n` 在数组中 {#first-n}

此 `topN` 函数用于返回第一个 `N` 数组中的项（当根据给定的数值表达式按升序排序时）。

**格式**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ARRAY}` | 要排序的数组或列表。 |
| `{VALUE}` | 用于对数组或列表进行排序的属性。 |
| `{AMOUNT}` | 要返回的项数。 |

**示例**

以下PQL查询返回价格最高的前五个订单。

```sql
orders.topN(price, 5)
```

## 最后 `n` 在数组中

此 `bottomN` 函数用于返回最后一个 `N` 数组中的项（当根据给定的数值表达式按升序排序时）。

**格式**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| 参数 | 描述 |
| --------- | ----------- | 
| `{ARRAY}` | 要排序的数组或列表。 |
| `{VALUE}` | 用于对数组或列表进行排序的属性。 |
| `{AMOUNT}` | 要返回的项数。 |

**示例**

以下PQL查询返回价格最低的前五张订单。

```sql
orders.bottomN(price, 5)
```

## 第一个项目

此 `head` 函数用于返回数组或列表中的第一项。

**格式**

```sql
{ARRAY}.head()
```

**示例**

以下PQL查询返回价格最高的前五个订单中的第一个。 欲知关于 `topN` 函数位于 [第一 `n` 在数组中](#first-n) 部分。

```sql
orders.topN(price, 5).head()
```

## 后续步骤

现在，您已了解数组、列表和设置函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [配置文件查询语言概述](./overview.md).

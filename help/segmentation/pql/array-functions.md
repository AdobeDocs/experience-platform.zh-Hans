---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；PQL;PQL；配置文件查询语言；数组函数；数组；
solution: Experience Platform
title: 数组、列表和设置PQL函数
description: 配置文件查询语言(PQL)提供了一些函数，可简化与数组、列表和字符串的交互。
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 5%

---

# 数组、列表和设置函数

[!DNL Profile Query Language] (PQL)提供了一些函数，可简化与数组、列表和字符串的交互。 有关其他PQL函数的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md).

## 在

的 `in` 函数来确定项目是否是数组或列表的成员。

**格式**

```sql
{VALUE} in {ARRAY}
```

**示例**

以下PQL查询定义了3月、6月或9月生日的用户。

```sql
person.birthMonth in [3, 6, 9]
```

## 不在

的 `notIn` 函数来确定项目是否不是数组或列表的成员。

>[!NOTE]
>
>的 `notIn` 函数 *也* 确保两个值均不等于null。 因此，结果不是 `in` 函数。

**格式**

```sql
{VALUE} notIn {ARRAY}
```

**示例**

以下PQL查询可定义生日不在3月、6月或9月的人员。

```sql
person.birthMonth notIn [3, 6, 9]
```

## Intersects

的 `intersects` 函数用于确定两个阵列或列表是否具有至少一个公共成员。

**格式**

```sql
{ARRAY}.intersects({ARRAY})
```

**示例**

以下PQL查询定义其喜爱颜色至少包含红色、蓝色或绿色之一的人员。

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## 交集

的 `intersection` 函数用于确定两个数组或列表的公共成员。

**格式**

```sql
{ARRAY}.intersection({ARRAY})
```

**示例**

以下PQL查询定义人员1和人员2是否均具有红色、蓝色和绿色的收藏颜色。

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## 子集

的 `subsetOf` 函数用于确定特定阵列（阵列A）是否是另一阵列（阵列B）的子集。 换句话说，数组A中的所有元素都是数组B的元素。

**格式**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**示例**

以下PQL查询定义访问了其所有喜爱城市的人员。

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## 超集

的 `supersetOf` 函数用于确定特定阵列（阵列A）是否是另一阵列（阵列B）的超集。 换言之，数组A包含数组B中的所有元素。

**格式**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**示例**

以下PQL查询定义至少吃过一次寿司和比萨的用户。

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## 包括

的 `includes` 函数来确定数组或列表是否包含给定项。

**格式**

```sql
{ARRAY}.includes({ITEM})
```

**示例**

以下PQL查询定义喜爱颜色包含红色的人员。

```sql
person.favoriteColors.includes("red")
```

## 非重复

的 `distinct` 函数从数组或列表中删除重复值。

**格式**

```sql
{ARRAY}.distinct()
```

**示例**

以下PQL查询指定在多个商店中下订单的人员。

```sql
person.orders.storeId.distinct().count() > 1
```

## 分组依据

的 `groupBy` 函数，用于将数组或列表的值根据表达式的值划分为组。

**格式**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ARRAY}` | 要分组的数组或列表。 |
| `{EXPRESSION}` | 返回的表达式可映射数组或列表中的每个项目。 |

**示例**

以下PQL查询将存储订单的所有订单分组到一起。

```sql
orders.groupBy(storeId)
```

## 过滤器

的 `filter` 函数，用于根据表达式筛选数组或列表。

**格式**

```sql
{ARRAY}.filter({EXPRESSION})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ARRAY}` | 要过滤的数组或列表。 |
| `{EXPRESSION}` | 要过滤的表达式。 |

**示例**

以下PQL查询定义所有21岁或21岁以上的人员。

```sql
person.filter(age >= 21)
```

## 地图

的 `map` 函数，以通过向给定数组中的每个项目应用表达式来创建新数组。

**格式**

```sql
array.map(expression)
```

**示例**

以下PQL查询会创建一个新的数字数组，并将原始数字的值用平方表示。

```sql
numbers.map(square)
```

## 第一个 `n` 在阵列中 {#first-n}

的 `topN` 函数返回 `N` 数组中的项目，当根据给定的数值表达式以升序排序时。

**格式**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ARRAY}` | 要排序的数组或列表。 |
| `{VALUE}` | 对数组或列表进行排序的属性。 |
| `{AMOUNT}` | 要返回的项目数。 |

**示例**

以下PQL查询返回价格最高的前五个订单。

```sql
orders.topN(price, 5)
```

## 最后 `n` 在阵列中

的 `bottomN` 函数返回 `N` 数组中的项目，当根据给定的数值表达式以升序排序时。

**格式**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| 参数 | 描述 |
| --------- | ----------- | 
| `{ARRAY}` | 要排序的数组或列表。 |
| `{VALUE}` | 对数组或列表进行排序的属性。 |
| `{AMOUNT}` | 要返回的项目数。 |

**示例**

以下PQL查询以最低价格返回前五个订单。

```sql
orders.bottomN(price, 5)
```

## 第一项

的 `head` 函数返回数组或列表中的第一个项目。

**格式**

```sql
{ARRAY}.head()
```

**示例**

以下PQL查询返回价格最高的前五个订单中的第一个。 有关 `topN` 函数 [第 `n` 在阵列中](#first-n) 中。

```sql
orders.topN(price, 5).head()
```

## 后续步骤

现在，您已经了解了数组、列表和设置函数，接下来可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语言概述](./overview.md).

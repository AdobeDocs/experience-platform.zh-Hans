---
solution: Experience Platform
title: 数组、列表和设置PQL函数
description: Profile Query Language (PQL)提供了一些功能，可简化与数组、列表和字符串的交互。
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 4%

---

# 数组、列表和集合函数

[!DNL Profile Query Language] (PQL)提供了一些功能，使与数组、列表和字符串的交互更容易。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## In

`in`函数用于确定一个项是数组的成员，还是作为布尔值列表的成员。

**格式**

```sql
{VALUE} in {ARRAY}
```

**示例**

以下PQL查询定义3月、6月或9月生日的用户。

```sql
person.birthMonth in [3, 6, 9]
```

## Not in

`notIn`函数用于确定一个项是否不是作为布尔值的数组或列表的成员。

>[!NOTE]
>
>`notIn`函数&#x200B;*还*&#x200B;确保这两个值都不等于null。 因此，结果不是`in`函数的完全否定。

**格式**

```sql
{VALUE} notIn {ARRAY}
```

**示例**

以下PQL查询定义生日不在3月、6月或9月的人员。

```sql
person.birthMonth notIn [3, 6, 9]
```

## Intersects

`intersects`函数用于确定两个数组或列表是否至少有一个公共成员作为布尔值。

**格式**

```sql
{ARRAY}.intersects({ARRAY})
```

**示例**

以下PQL查询定义其最喜爱的颜色至少包括红色、蓝色或绿色之一的人员。

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## 交集

`intersection`函数用于确定两个数组或列表作为列表的公用成员。

**格式**

```sql
{ARRAY}.intersection({ARRAY})
```

**示例**

以下PQL查询定义人员1和人员2是否同时具有最喜爱的红色、蓝色和绿色颜色。

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## Subset of

`subsetOf`函数用于确定一个特定数组（数组A）是否是另一个数组（数组B）的子集。 换句话说，数组A中的所有元素都是数组B的元素作为布尔值。

**格式**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**示例**

以下PQL查询定义访问过其所有最喜爱城市的人。

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## Superset of

`supersetOf`函数用于确定一个特定数组（数组A）是否是另一个数组（数组B）的超集。 换句话说，该数组A包含数组B中的所有元素作为布尔值。

**格式**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**示例**

以下PQL查询定义了至少吃过一次寿司和比萨的人。

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## Includes

`includes`函数用于确定一个数组或列表是否包含作为布尔值的给定项。

**格式**

```sql
{ARRAY}.includes({ITEM})
```

**示例**

以下PQL查询定义其最喜爱的颜色包括红色的人员。

```sql
person.favoriteColors.includes("red")
```

## Distinct

`distinct`函数用于从数组或作为数组的列表中删除重复的值。

**格式**

```sql
{ARRAY}.distinct()
```

**示例**

以下PQL查询指定在多个商店下订单的人员。

```sql
person.orders.storeId.distinct().count() > 1
```

## 分组依据

`groupBy`函数用于根据表达式的值将数组或列表的值分区为组，作为从分组表达式的唯一值到作为数组表达式值分区的数组的映射。

**格式**

```sql
{ARRAY}.groupBy({EXPRESSION})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ARRAY}` | 要分组的数组或列表。 |
| `{EXPRESSION}` | 映射返回的数组或列表中的每个项的表达式。 |

**示例**

以下PQL查询将存储下订单所依据的所有订单分组。

```sql
xEvent[type="order"].groupBy(storeId)
```

## 筛选条件

`filter`函数用于根据作为数组或列表的表达式筛选数组或列表，具体取决于输入。

**格式**

```sql
{ARRAY}.filter({EXPRESSION})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ARRAY}` | 要过滤的数组或列表。 |
| `{EXPRESSION}` | 作为筛选依据的表达式。 |

**示例**

以下PQL查询定义了21岁或以上的所有人员。

```sql
person.filter(age >= 21)
```

## 地图

`map`函数用于将表达式作为数组应用于给定数组中的每个项，从而创建新数组。

**格式**

```sql
array.map(expression)
```

**示例**

以下PQL查询创建一个新的数字数组，并平方原始数字的值。

```sql
numbers.map(square)
```

## 数组中的前`n` {#first-n}

`topN`函数用于返回数组中的前`N`项（当根据给定的数值表达式作为数组按升序排序时）。

**格式**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| 参数 | 描述 |
| --------- | ----------- |
| `{ARRAY}` | 要排序的数组或列表。 |
| `{VALUE}` | 要对数组或列表进行排序的属性。 |
| `{AMOUNT}` | 要返回的项目数。 |

**示例**

以下PQL查询返回具有最高价格的前5个订单。

```sql
orders.topN(price, 5)
```

## 数组中的最后`n`

`bottomN`函数用于返回数组中的最后`N`项（当根据给定的数值表达式作为数组按升序排序时）。

**格式**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| 参数 | 描述 |
| --------- | ----------- | 
| `{ARRAY}` | 要排序的数组或列表。 |
| `{VALUE}` | 要对数组或列表进行排序的属性。 |
| `{AMOUNT}` | 要返回的项目数。 |

**示例**

以下PQL查询返回价格最低的前五位订单。

```sql
orders.bottomN(price, 5)
```

## First item

`head`函数用于将数组或列表中的第一个项作为对象返回。

**格式**

```sql
{ARRAY}.head()
```

**示例**

以下PQL查询返回价格最高的前五位订单中的第一位。 有关`topN`函数的更多信息，请参见[数组](#first-n)中的第一个`n`。

```sql
orders.topN(price, 5).head()
```

## 后续步骤

现在您已了解数组、列表和设置函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读[Profile Query Language概述](./overview.md)。

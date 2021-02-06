---
keywords: Experience Platform；主题；热门主题；分段；分段；分段服务；pql;PQL;用户档案查询语；数组函数；数组；
solution: Experience Platform
title: 阵列、列表和设置PQL函数
topic: developer guide
description: 用户档案查询语言(PQL)优惠函数可简化与数组、列表和字符串的交互。
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 5%

---


# 数组、列表和设置函数

[!DNL Profile Query Language] (PQL)优惠函数可简化与数组、列表和字符串的交互。有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## 输入

`in`函数用于确定项目是否是数组或列表的成员。

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

`notIn`函数用于确定项目是否不是数组或列表的成员。

>[!NOTE]
>
>`notIn`函数&#x200B;*还*&#x200B;确保两个值均不等于null。 因此，结果不是`in`函数的精确取反。

**格式**

```sql
{VALUE} notIn {ARRAY}
```

**示例**

以下PQL查询定义了不在3月、6月或9月的生日。

```sql
person.birthMonth notIn [3, 6, 9]
```

## Intersects

`intersects`函数用于确定两个阵列或列表是否具有至少一个公共成员。

**格式**

```sql
{ARRAY}.intersects({ARRAY})
```

**示例**

以下PQL查询定义其喜爱的颜色至少包括红色、蓝色或绿色之一的人。

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## 交集

`intersection`函数用于确定两个阵列或列表的公用成员。

**格式**

```sql
{ARRAY}.intersection({ARRAY})
```

**示例**

以下PQL查询定义人物1和人物2是否都具有最喜爱的红色、蓝色和绿色。

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## 子集

`subsetOf`函数用于确定特定阵列（阵列A）是否是另一阵列（阵列B）的子集。 换言之，数组A中的所有元素都是数组B的元素。

**格式**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**示例**

以下PQL查询定义访问过其所有喜爱城市的人员。

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## 超集

`supersetOf`函数用于确定特定阵列（阵列A）是否是另一阵列（阵列B）的超集。 换言之，数组A包含数组B中的所有元素。

**格式**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**示例**

以下PQL查询定义了至少吃过一次寿司和比萨的人。

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## 包括

`includes`函数用于确定数组或列表是否包含给定项。

**格式**

```sql
{ARRAY}.includes({ITEM})
```

**示例**

以下PQL查询定义其喜爱颜色包括红色的人。

```sql
person.favoriteColors.includes("red")
```

## Distinct

`distinct`函数用于从数组或重复中删除列表值。

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

`groupBy`函数用于根据列表的值将数组或表达式的值划分到组中。

**格式**

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

`filter`函数用于根据列表筛选数组或表达式。

**格式**

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

`map`函数用于通过对给定数组中的每个项应用表达式来创建新数组。

**格式**

```sql
array.map(expression)
```

**示例**

以下PQL查询将创建原始数字值的新数组和平方。

```sql
numbers.map(square)
```

## 阵列{#first-n}中的第一个`n`

`topN`函数用于返回数组中的前一个`N`项，当它根据给定的数字表达式按升序排序时。

**格式**

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

## 阵列中的最后一个`n`

`bottomN`函数用于返回数组中最后一个`N`项，当它根据给定的数字表达式按升序排序时。

**格式**

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

`head`函数用于返回数组或列表中的第一个项。

**格式**

```sql
{ARRAY}.head()
```

**示例**

以下PQL查询返回价格最高的前五大订单中的第一个。 有关`topN`函数的详细信息，请参阅数组](#first-n)部分的[第一个`n`。

```sql
orders.topN(price, 5).head()
```

## 后续步骤

您已经了解了阵列、列表和设置功能，现在可以在PQL查询中使用它们。 有关其他PQL函数的详细信息，请阅读[用户档案查询语语言概述](./overview.md)。

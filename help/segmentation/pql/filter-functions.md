---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 滤镜函数
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# 滤镜函数

过滤器函数用于过滤用户档案查询语(PQL)中数组中的数据。 有关其他PQL函数的更多信息，请参阅 [用户档案查询语言概述](./overview.md)。

## 过滤器

该 `[]` （过滤器）函数允许将过滤器应用到数组并返回与指定条件匹配的数组子集。

**格式**

```sql
{ARRAY}[filter]
```

**示例**

以下PQL查询可获得至少包含一个SKU等于“PS”的产品项的所有事件。

```sql
xEvent[productListItems[SKU="PS"]]
```

## 向上运算符

( `^` up)运算符允许您引用过滤器的高级属性。

**格式**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| 参数 | 描述 |
| -------- | ----------- |
| `{ARRAY}` | 正在筛选的数组。 |
| `{FILTER_1}` | 外层过滤。 |
| `{FILTER_2}` | 过滤的内层 |
| `^{PROPERTY}` | 也正在筛选的属性。 由于这 `^`个原因，它正在检查基于filter1的属性。 |

**示例**

以下PQL查询可获取所有事件，其中至少有一个产品项目，其SKU等于“PS **** ”，或者其性别为女性。

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## 后续步骤

现在您已经了解过滤器功能，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语概述](./overview.md)。

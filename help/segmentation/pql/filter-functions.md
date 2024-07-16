---
solution: Experience Platform
title: PQL筛选器函数
description: 筛选器函数用于筛选Profile Query Language (PQL)中数组内的数据。
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 2%

---

# 筛选器函数

筛选器函数用于筛选[!DNL Profile Query Language] (PQL)中数组内的数据。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## 筛选条件

`[]` （过滤器）函数允许将过滤器应用于数组，并返回与指定条件匹配的数组子集。

**格式**

```sql
{ARRAY}[filter]
```

**示例**

以下PQL查询获取至少具有一个产品项目，且SKU等于“PS”的所有事件。

```sql
xEvent[productListItems[SKU="PS"]]
```

## Up运算符

`^` (up)运算符允许您引用上层筛选器中的属性。

**格式**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| 参数 | 描述 |
| -------- | ----------- |
| `{ARRAY}` | 正在过滤的数组。 |
| `{FILTER_1}` | 过滤的外层。 |
| `{FILTER_2}` | 过滤的内层 |
| `^{PROPERTY}` | 正在过滤的属性。 由于`^`，它正在检查基于filter1的属性。 |

**示例**

以下PQL查询获取的所有事件中，至少有一个产品项的SKU等于“PS”**或**&#x200B;具有女性性别的人员。

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## 后续步骤

现在您已了解筛选器函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读[Profile Query Language概述](./overview.md)。

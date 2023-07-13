---
solution: Experience Platform
title: PQL筛选函数
description: 筛选器函数用于筛选配置文件查询语言(PQL)数组内的数据。
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 4%

---

# 筛选器函数

筛选函数用于筛选数组中的数据。 [!DNL Profile Query Language] (PQL)。 有关其他PQL函数的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md).

## 过滤器

此 `[]` (filter)函数允许将过滤器应用于数组，并返回与指定条件匹配的数组子集。

**格式**

```sql
{ARRAY}[filter]
```

**示例**

以下PQL查询可获取至少具有一个产品项目且SKU等于“PS”的所有事件。

```sql
xEvent[productListItems[SKU="PS"]]
```

## Up运算符

此 `^` (up)运算符允许您引用过滤器较高层级的属性。

**格式**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| 参数 | 描述 |
| -------- | ----------- |
| `{ARRAY}` | 正在过滤的数组。 |
| `{FILTER_1}` | 过滤的外层。 |
| `{FILTER_2}` | 滤镜的内层 |
| `^{PROPERTY}` | 也正在被过滤的属性。 由于 `^`，它检查基于filter1的属性。 |

**示例**

以下PQL查询可获取至少具有一个产品项目（SKU等于“PS”）的所有事件 **或** 有一个性别为女性的人。

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## 后续步骤

现在，您已了解筛选器函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [配置文件查询语言概述](./overview.md).

---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;filter functions;filter;
solution: Experience Platform
title: 过滤器函数
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 4%

---


# 过滤器函数

过滤器函数用于过滤(PQL)中数组内 [!DNL Profile Query Language] 的数据。 有关其他PQL功能的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md)。

## 过滤器

该 `[]` （过滤器）函数允许将过滤器应用于数组并返回与指定条件匹配的数组子集。

**Format**

```sql
{ARRAY}[filter]
```

**示例**

以下PQL查询可获取至少有一个SKU等于“PS”的产品项的所有事件。

```sql
xEvent[productListItems[SKU="PS"]]
```

## 向上运算符

( `^` up)运算符允许您引用过滤器上层的属性。

**Format**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| 参数 | 描述 |
| -------- | ----------- |
| `{ARRAY}` | 正在筛选的数组。 |
| `{FILTER_1}` | 外层过滤。 |
| `{FILTER_2}` | 过滤的内层 |
| `^{PROPERTY}` | 正在筛选的属性。 由于这 `^`个原因，它正在检查基于filter1的属性。 |

**示例**

以下PQL查询可获取所有事件，这些至少具有一个SKU等于“PS”的产 **品项** ，或具有性别为女性的人员。

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## 后续步骤

现在您已经了解了过滤器功能，可以在PQL查询中使用它们。 有关其他PQL功能的详细信息，请阅读 [用户档案查询语概述](./overview.md)。

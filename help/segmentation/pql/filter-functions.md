---
keywords: Experience Platform；主题；热门主题；分段；分段；分段服务；pql;PQL;用户档案查询语；过滤功能；过滤；
solution: Experience Platform
title: PQL过滤器函数
topic: developer guide
description: 过滤器函数用于以用户档案查询语(PQL)筛选数组中的数据。
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 4%

---


# 过滤器函数

过滤器函数用于过滤[!DNL Profile Query Language](PQL)中阵列内的数据。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## 过滤器

`[]`（过滤器）函数允许将过滤器应用于数组并返回与指定条件匹配的数组子集。

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

`^`(up)运算符允许您引用过滤器的上级属性。

**格式**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| 参数 | 描述 |
| -------- | ----------- |
| `{ARRAY}` | 正在筛选的数组。 |
| `{FILTER_1}` | 外层过滤。 |
| `{FILTER_2}` | 过滤的内层 |
| `^{PROPERTY}` | 正在筛选的属性。 由于`^`，它正在检查基于filter1的属性。 |

**示例**

以下PQL查询可获取所有事件，其中至少有一个产品项目，其SKU等于“PS” **或**，且其性别为女性。

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## 后续步骤

现在您已经了解了过滤器功能，可以在PQL查询中使用它们。 有关其他PQL函数的详细信息，请阅读[用户档案查询语语言概述](./overview.md)。

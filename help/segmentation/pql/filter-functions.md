---
keywords: Experience Platform；主题；热门主题；分段；分段；分段服务；pql;PQL;用户档案查询语言；过滤功能；过滤器；
solution: Experience Platform
title: PQL筛选器函数
topic-legacy: developer guide
description: 筛选器函数用于以用户档案查询语言(PQL)筛选数组内的数据。
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 4%

---

# 滤镜函数

筛选器函数用于筛选[!DNL Profile Query Language](PQL)中数组内的数据。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] overview](./overview.md)。

## 过滤器

`[]`（过滤器）函数允许将过滤器应用于数组并返回与指定条件匹配的数组子集。

**格式**

```sql
{ARRAY}[filter]
```

**示例**

以下PQL查询可获取所有至少包含一个产品项且SKU等于“PS”的事件。

```sql
xEvent[productListItems[SKU="PS"]]
```

## 向上运算符

`^`(up)运算符允许您引用过滤器的高级属性。

**格式**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| 参数 | 描述 |
| -------- | ----------- |
| `{ARRAY}` | 正在筛选的数组。 |
| `{FILTER_1}` | 滤波的外层。 |
| `{FILTER_2}` | 过滤的内层 |
| `^{PROPERTY}` | 也正在筛选的属性。 由于`^`，它正在检查基于filter1的属性。 |

**示例**

以下PQL查询可获取所有事件，其中至少有一个SKU等于“PS” **或**&#x200B;的产品项目，其性别为女性。

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## 后续步骤

现在，您已经了解了过滤器功能，可以在PQL查询中使用它们。 有关其他PQL函数的详细信息，请阅读[用户档案查询语言概述](./overview.md)。

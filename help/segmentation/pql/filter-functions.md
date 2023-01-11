---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；PQL;PQL；配置文件查询语言；过滤器函数；过滤器；
solution: Experience Platform
title: PQL筛选器函数
description: 过滤器函数用于以配置文件查询语言(PQL)在数组内过滤数据。
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 4%

---

# 筛选函数

过滤器函数用于在 [!DNL Profile Query Language] (PQL)。 有关其他PQL函数的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md).

## 过滤器

的 `[]` (filter)函数允许将过滤器应用于数组并返回与指定条件匹配的数组子集。

**格式**

```sql
{ARRAY}[filter]
```

**示例**

以下PQL查询会获取所有事件，其中至少有一个产品项目的SKU等于“PS”。

```sql
xEvent[productListItems[SKU="PS"]]
```

## 向上运算符

的 `^` (up)运算符允许您引用过滤器上级别的属性。

**格式**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| 参数 | 描述 |
| -------- | ----------- |
| `{ARRAY}` | 正在过滤的数组。 |
| `{FILTER_1}` | 滤波的外层。 |
| `{FILTER_2}` | 过滤的内层 |
| `^{PROPERTY}` | 也正在筛选的属性。 由于 `^`，则会检查基于filter1的属性。 |

**示例**

以下PQL查询会获取所有事件，其中至少有一个产品项目的SKU等于“PS” **或** 有性别为女性的人。

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## 后续步骤

现在，您已经了解过滤器函数，接下来可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语言概述](./overview.md).

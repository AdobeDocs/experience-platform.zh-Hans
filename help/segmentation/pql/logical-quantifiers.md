---
solution: Experience Platform
title: PQL逻辑量化符
description: 逻辑量化符可用于断言Profile Query Language (PQL)中数组的条件。
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 3%

---

# 逻辑量化符函数

逻辑量化符可用于断言[!DNL Profile Query Language] (PQL)中数组的条件。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## 存在

`exists`函数确定数组中的项是否存在，前提是它满足所提供的条件。

**格式**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{VARIABLE}` | 变量的名称。 |
| `{EXPRESSION}` | 正在检查的数组。 |
| `{CONDITION}` | 筛选返回数组中的值的可选表达式。 |

**示例**

以下PQL查询获取价格大于$50或具有“PS”SKU的所有事件。

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 全部

`forall`函数确定数组中满足所有给定条件的所有项。

**格式**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{VARIABLE}` | 变量的名称。 |
| `{EXPRESSION}` | 正在检查的数组。 |
| `{CONDITION}` | 筛选返回数组中的值的可选表达式。 |

**示例**

以下PQL查询获取价格大于$50且SKU为“PS”的所有事件。

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 后续步骤

现在，您已了解逻辑量词，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读[Profile Query Language概述](./overview.md)。

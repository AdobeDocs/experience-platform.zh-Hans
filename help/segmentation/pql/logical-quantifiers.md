---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 逻辑量词
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# 逻辑量词函数

逻辑量化符可用于用用户档案查询语言(PQL)中的数组声明条件。 有关其他PQL函数的更多信息，请参阅 [用户档案查询语言概述](./overview.md)。

## 存在

该函 `exists` 数确定阵列中的项的存在，只要满足所提供的条件。

**格式**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{VARIABLE}` | 变量的名称。 |
| `{EXPRESSION}` | 正在检查的数组。 |
| `{CONDITION}` | 一个可选表达式，它过滤器数组中返回的值。 |

**示例**

以下PQL查询可获取所有价格高于50美元或SKU为“PS”的事件。

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 适用于所有人

该函 `forall` 数确定数组中满足所有给定条件的所有项。

**格式**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{VARIABLE}` | 变量的名称。 |
| `{EXPRESSION}` | 正在检查的数组。 |
| `{CONDITION}` | 一个可选表达式，它过滤器数组中返回的值。 |

**示例**

以下PQL查询可获取所有价格高于50美元且SKU为“PS”的事件。

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 后续步骤

现在您已经了解了逻辑量词，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语概述](./overview.md)。

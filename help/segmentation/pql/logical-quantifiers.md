---
keywords: Experience Platform；主题；热门主题；分段；分段；分段服务；pql;PQL;用户档案查询语；逻辑量词；逻辑量词；
solution: Experience Platform
title: PQL逻辑量化符
topic: developer guide
description: 逻辑量化器可用于用用户档案查询语言(PQL)中的数组声明条件。
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 4%

---


# 逻辑量词函数

逻辑量化符可用于用[!DNL Profile Query Language](PQL)中的阵列声明条件。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## 存在

`exists`函数确定数组中某一项的存在，前提是它满足所提供的条件。

**Format**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{VARIABLE}` | 变量的名称。 |
| `{EXPRESSION}` | 正在检查的数组。 |
| `{CONDITION}` | 一个可选表达式,过滤器数组中返回的值。 |

**示例**

以下PQL查询可获取价格高于50美元或SKU为“PS”的所有事件。

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 适用于所有人

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
| `{CONDITION}` | 一个可选表达式,过滤器数组中返回的值。 |

**示例**

以下PQL查询可获取所有价格高于$50且SKU为“PS”的事件。

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 后续步骤

现在您已经了解了逻辑量词，可以在PQL查询中使用它们。 有关其他PQL函数的详细信息，请阅读[用户档案查询语语言概述](./overview.md)。

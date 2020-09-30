---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;logical quantifiers;logical quantifier;
solution: Experience Platform
title: 逻辑量词
topic: developer guide
description: 逻辑量化器可用于用用户档案查询语言(PQL)中的数组声明条件。
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 5%

---


# 逻辑量词函数

逻辑量化器可用于在(PQL)中用数组 [!DNL Profile Query Language] 声明条件。 有关其他PQL功能的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md)。

## 存在

该函 `exists` 数确定在数组中的项的存在，只要它满足所提供的条件。

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

该函 `forall` 数确定数组中满足所有给定条件的所有项。

**Format**

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

现在您已经了解了逻辑量词，可以在PQL查询中使用它们。 有关其他PQL功能的详细信息，请阅读 [用户档案查询语概述](./overview.md)。

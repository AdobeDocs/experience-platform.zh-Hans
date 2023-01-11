---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；PQL;PQL；配置文件查询语言；逻辑量词；逻辑量词；
solution: Experience Platform
title: PQL逻辑量词
description: 逻辑量词可用于通过配置文件查询语言(PQL)中的数组声明条件。
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 4%

---

# 逻辑量词函数

逻辑量词可用于在中通过数组声明条件 [!DNL Profile Query Language] (PQL)。 有关其他PQL函数的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md).

## 存在

的 `exists` 函数确定数组中项的存在性，前提是它满足所提供的条件。

**格式**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{VARIABLE}` | 变量的名称。 |
| `{EXPRESSION}` | 正在检查的数组。 |
| `{CONDITION}` | 可选表达式，用于筛选返回数组中的值。 |

**示例**

以下PQL查询会获取价格超过$50或SKU为“PS”的所有事件。

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 适用于所有

的 `forall` 函数确定数组中满足所有给定条件的所有项目。

**格式**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| 参数 | 描述 |
| ---------- | ----------- |
| `{VARIABLE}` | 变量的名称。 |
| `{EXPRESSION}` | 正在检查的数组。 |
| `{CONDITION}` | 可选表达式，用于筛选返回数组中的值。 |

**示例**

以下PQL查询会获取价格超过$50且SKU为“PS”的所有事件。

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 后续步骤

现在，您已经了解了逻辑量词，接下来可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语言概述](./overview.md).

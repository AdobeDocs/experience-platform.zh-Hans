---
solution: Experience Platform
title: PQL其他函数
description: 以下函数是Profile Query Language (PQL)的一个其他函数。
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 3%

---

# 杂项函数

以下函数是[!DNL Profile Query Language] (PQL)的其他函数。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## Let

`let`函数允许将表达式存储为变量，以便稍后在查询中使用。

**格式**

```sql
let {VARIABLE} = {EXPRESSION}
```

**示例**

以下PQL查询获取该交易以美元表示的所有产品总计的总和，其中总计大于$100且小于$1000。

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## 后续步骤

现在，您已了解其他函数，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读[Profile Query Language概述](./overview.md)。

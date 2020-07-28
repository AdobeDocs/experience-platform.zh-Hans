---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 杂项函数
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 3%

---


# 杂项函数

The following function is a miscellaneous function for [!DNL Profile Query Language] (PQL). 有关其他PQL函数的更多信息，请参阅 [用户档案查询语概述](./overview.md)。

## Let

该 `let` 函数允许将表达式存储为变量，以便以后在查询中使用。

**Format**

```sql
let {VARIABLE} = {EXPRESSION}
```

**示例**

The following PQL query gets all sums of product totals with the transaction in USD where the sum is greater than $100 and less than $1000.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## 后续步骤

您已经了解了其他功能，现在可以在PQL查询中使用它们。 有关其他PQL功能的详细信息，请阅读 [用户档案查询语概述](./overview.md)。

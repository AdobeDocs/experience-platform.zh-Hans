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

以下函数是(PQL)的一 [!DNL Profile Query Language] 个杂项函数。 有关其他PQL函数的更多信息，请参阅 [用户档案查询语概述](./overview.md)。

## 让

该 `let` 函数允许将表达式存储为变量，以便以后在查询中使用。

**格式**

```sql
let {VARIABLE} = {EXPRESSION}
```

**示例**

以下PQL查询以美元表示，以下PQL客户获取交易的所有产品总额，其中总额大于100美元，小于1000美元。

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## 后续步骤

您已经了解了其他功能，现在可以在PQL查询中使用它们。 有关其他PQL功能的详细信息，请阅读 [用户档案查询语概述](./overview.md)。

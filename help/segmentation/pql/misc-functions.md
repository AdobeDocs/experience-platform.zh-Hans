---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 其他函数
topic: developer guide
translation-type: tm+mt
source-git-commit: d7ec6240864916d3b54db8bd641f4917a38f9480

---


# 其他函数

以下函数是用户档案查询语(PQL)的一个杂项函数。 有关其他PQL函数的更多信息，请参阅 [用户档案查询语言概述](./overview.md)。

## 让

该函 `let` 数允许将表达式存储为变量，以便以后在查询中使用。

**格式**

```sql
let {VARIABLE} = {EXPRESSION}
```

**示例**

以下PQL查询以美元为单位获取交易的所有产品总和，其中总和大于100美元且小于1000美元。

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## 后续步骤

现在您已经了解了其他功能，可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语概述](./overview.md)。

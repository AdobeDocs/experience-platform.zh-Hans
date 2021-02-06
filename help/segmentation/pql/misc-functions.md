---
keywords: Experience Platform；主题；热门主题；分段；分段；分段服务；pql;PQL;用户档案查询语；杂项功能；
solution: Experience Platform
title: PQL杂项函数
topic: developer guide
description: 以下函数是用户档案查询语言(PQL)的一个杂项函数。
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---


# 杂项函数

以下函数是[!DNL Profile Query Language](PQL)的一个杂项函数。 有关其他PQL函数的详细信息，请参阅[[!DNL Profile Query Language] 概述](./overview.md)。

## 让

`let`函数允许将表达式存储为变量，以后在查询中使用。

**Format**

```sql
let {VARIABLE} = {EXPRESSION}
```

**示例**

以下PQL查询以美元表示，以下PQL客户获取交易的所有产品总额，其中总额大于100美元，小于1000美元。

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## 后续步骤

您已经了解了其他功能，现在可以在PQL查询中使用它们。 有关其他PQL函数的详细信息，请阅读[用户档案查询语语言概述](./overview.md)。

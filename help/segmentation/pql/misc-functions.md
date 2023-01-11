---
keywords: Experience Platform；主页；热门主题；分段；分段；分段服务；PQL;PQL；配置文件查询语言；其他功能；杂项；
solution: Experience Platform
title: PQL其他函数
description: 以下函数是用于配置文件查询语言(PQL)的其他函数。
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# 其他函数

以下函数是 [!DNL Profile Query Language] (PQL)。 有关其他PQL函数的更多信息，请参阅 [[!DNL Profile Query Language] 概述](./overview.md).

## 让

的 `let` 函数允许将表达式存储为变量，以便稍后在查询中使用。

**格式**

```sql
let {VARIABLE} = {EXPRESSION}
```

**示例**

以下PQL查询以美元形式获取交易的所有产品合计总和，其中总和大于$100且小于$1000。

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## 后续步骤

现在，您已经了解了其他函数，接下来可以在PQL查询中使用它们。 有关其他PQL功能的更多信息，请阅读 [用户档案查询语言概述](./overview.md).

---
solution: Experience Platform
title: PQL杂项函数
description: 以下函数是配置文件查询语言(PQL)的杂项函数。
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 3%

---

# 杂项函数

以下函数是其他函数 [!DNL Profile Query Language] (PQL)。 有关其他PQL函数的更多信息，请参见 [[!DNL Profile Query Language] 概述](./overview.md).

## Let

此 `let` 函数允许将表达式存储为变量，以便稍后在查询中使用。

**格式**

```sql
let {VARIABLE} = {EXPRESSION}
```

**示例**

以下PQL查询获取该交易记录的总和大于$100且小于$1000的所有产品总和（以USD为单位）。

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## 后续步骤

现在，您已了解其他函数，可以在PQL查询中使用它们。 有关其他PQL功能的详细信息，请参阅 [配置文件查询语言概述](./overview.md).

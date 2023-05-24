---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；pql；PQL；設定檔查詢語言；雜項函式；雜項；
solution: Experience Platform
title: PQL雜項函式
description: 下列函式是「設定檔查詢語言(PQL)」的其他函式。
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# 其他函式

下列函式是其他函式 [!DNL Profile Query Language] (PQL)。 如需其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概觀](./overview.md).

## Let

此 `let` 函式可將運算式儲存為變數，以便稍後在查詢中使用。

**格式**

```sql
let {VARIABLE} = {EXPRESSION}
```

**示例**

下列PQL查詢會取得交易總和大於$100且小於$1000時以USD表示的所有產品總計總和。

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## 后续步骤

現在您已瞭解其他函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱 [設定檔查詢語言概觀](./overview.md).

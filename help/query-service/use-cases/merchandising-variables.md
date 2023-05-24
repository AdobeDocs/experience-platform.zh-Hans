---
title: 從Analytics資料傳回並使用銷售變數
description: 瞭解如何提供XDM欄位和範例查詢，以存取Analytics資料集中的銷售變數。
exl-id: 1e2ae095-4152-446f-8b66-dae5512d690e
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 4%

---

# 從Analytics資料傳回並使用銷售變數

使用查詢服務管理從Adobe Analytics擷取到Adobe Experience Platform的資料作為資料集。 以下幾節提供範例查詢，您可以使用這些查詢來存取Analytics資料集中的銷售變數。 如需有關的詳細資訊，請參閱檔案： [如何內嵌及對映Adobe Analytics資料](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/adobe-applications/mapping/analytics.html?lang=zh-Hans) 透過Analytics來源

## 促销变量 {#merchandising-variables}

促销变量可遵循以下两种语法之一：

* **產品語法**：建立eVar值與產品的關聯。 
* **轉換變數語法**：僅在發生捆綁事件時才會建立eVar與產品的關聯。 您可以選取當作捆綁事件的事件。

## 產品語法 {#product-syntax}

在Adobe Analytics中，自訂產品層級的資料可透過特殊設定的變數（稱為銷售變數）收集。 這些是根據eVar或自訂事件。 這些變數與其一般用途的差異在於，它們代表點選上找到之每個產品的個別值，而非只有點選的單一值。

這些變數稱為產品語法銷售變數。 如此可收集資訊，例如依產品區分的「折扣金額」或客戶搜尋結果中產品的「頁面位置」相關資訊。

若要進一步瞭解如何使用產品語法，請閱讀Adobe Analytics檔案： [使用產品語法實作eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-product-syntax).

以下各節概述存取中銷售變數所需的XDM欄位 [!DNL Analytics] 資料集：

### eVar

```console
productListItems[#]._experience.analytics.customDimensions.evars.evar#
```

* `#`：您存取的陣列索引。
* `evar#`：您存取的特定eVar變數。

### 自定义事件

```console
productListItems[#]._experience.analytics.event1to100.event#.value
```

* `#`：您存取的陣列索引。
* `event#`：您正在存取的特定自訂事件變數。

## 產品語法使用案例 {#product-use-cases}

以下使用案例著重於傳回的銷售eVar `productListItems` 陣列使用SQL。

### 傳回銷售eVar和事件

以下查詢會針對在下列找到的第一個產品傳回銷售eVar和事件： `productListItems` 陣列。

```sql
SELECT
  productListItems[0]._experience.analytics.customDimensions.evars.eVar1,
  productListItems[0]._experience.analytics.event1to100.event1.value
FROM adobe_analytics_midvalues
WHERE timestamp = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
LIMIT 10
```

### 爆炸productListItems陣列，並傳回每個產品的銷售eVar和事件。

此下一個查詢會解壓縮 `productListItems` 陣列，並依據產品傳回每個銷售eVar和事件。 此 `_id` 包含欄位以顯示與原始點選的關係。 此 `_id` 值是資料集的唯一主索引鍵。

>[!NOTE]
>
>explode函式將陣列元素分隔成多列。 它排除null值。

```sql
SELECT
  _id,
  productItem._experience.analytics.customDimensions.evars.eVar1,
  productItem._experience.analytics.event1to100.event1.value
FROM (
  SELECT
    _id,
    explode(productListItems) as productItem
  FROM adobe_analytics_midvalues
  WHERE TIMESTAMP = to_timestamp('2019-07-23')
  AND productListItems[0].SKU IS NOT NULL
  AND productListItems[0]._experience.analytics.customDimensions.evars.eVar1 IS NOT NULL
  AND productListItems[0]._experience.analytics.event1to100.event1.value IS NOT NULL
)
LIMIT 20
```

>[!NOTE]
>
> 如果您嘗試擷取目前資料集中不存在的欄位，會發生「沒有這樣的結構欄位」錯誤。 評估錯誤訊息中傳回的原因以識別可用的欄位，然後更新您的查詢並重新執行。
>
>
```console
>ERROR: ErrorCode: 08P01 sessionId: XXXX queryId: XXXX Unknown error encountered. Reason: [No such struct field evar1 in eVar10, eVar13, eVar62, eVar88, eVar2;]
>```

### 轉換變數語法 {#conversion-variable-syntax}

另一種可在Adobe Analytics中找到的銷售變數型別是轉換變數語法。 當無法在產品變數中設定eVar值時，可使用轉換變數語法。 这种情况通常意味着您的页面没有推销渠道的任何上下文或查找方法。在這些情況下，您應該在使用者到達產品頁面之前設定銷售變數，而值會持續到捆綁事件發生為止。

例如，下列產品尋找案例說明所需資料如何在與產品相關的轉換或事件發生前出現在頁面上。

1. 使用者執行「冬季帽子」的內部搜尋，該搜尋會將啟用銷售eVar6的轉換語法設定為「內部搜尋：冬季帽子」。
2. 使用者按一下「華夫餅豆」並登陸產品詳細資訊頁面。\
   a.在此降落會引發 `Product View` 12.99美元的「華夫餅豆」活動。\
   b.始自 `Product View` 已設定為捆綁事件，產品「華夫餅豆」現在已與「internal search：winter hat」的eVar6值繫結。 無論何時收集「華夫餅豆餅」產品，都會與「內部搜尋：冬季帽子」相關聯。 這種情況會一直發生，直到達到eVar到期設定，或設定了新的eVar6值，並且捆綁事件再次與該產品發生為止。
3. 使用者將產品新增到購物車，並觸發 `Cart Add` 事件。
4. 使用者對「夏日襯衫」執行另一個內部搜尋，這會將啟用轉換語法的銷售eVar6設定為「內部搜尋：夏日襯衫」。
5. 使用者選取「運動T恤」並登陸產品詳細資訊頁面。\
   a.在此降落會引發 `Product View` 「運動衫」活動，19.99美元。\
   b.作為 `Product View` 事件為捆綁事件，產品「運動衫」現在已捆綁到「內部搜尋：夏季襯衫」的eVar6值。 先前的產品「華夫餅豆餅」仍與「內部搜尋：華夫餅豆餅」的eVar6值繫結。
6. 使用者將產品新增到購物車，並觸發 `Cart Add` 事件。
7. 使用者會簽出兩個產品。

在報表中，訂單、收入、產品檢視和購物車新增可根據eVar6報告，並與已繫結產品的活動一致。

| eVar6 （產品尋找方法） | 收入 | 訂購 | 產品檢視 | 購物車新增次數 |
| ------------------------------ | ------- | ------ | ------------- | ----- |
| 內部搜尋：夏季襯衫 | 19.99 | 1 | 1 | 1 |
| 內部搜尋：冬季帽子 | 12.99 | 1 | 1 | 1 |

若要進一步瞭解使用轉換變數語法，請閱讀Adobe Analytics檔案，網址為 [使用轉換變數語法實作eVar](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar-merchandising.html#implement-using-conversion-variable-syntax).

以下顯示的XDM欄位可產生轉換變數語法，位於 [!DNL Analytics] 資料集：

#### eVar

```console
_experience.analytics.customDimensions.evars.evar#
```

* `evar#`：您存取的特定eVar變數。

#### 产品

```console
productListItems[#].sku
```

* `#`：您存取的陣列索引。

## 轉換變數使用案例 {#conversion-variable-use-cases}

以下使用案例反映需要轉換變數語法的情境。

### 將值繫結至特定產品和事件配對

以下查詢會將值與特定產品和事件配對繫結。 在此範例中，值會與產品檢視事件繫結。

```sql
SELECT
  endUserIds._experience.aaid.id AS AAID,
  timestamp,
  CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
  OVER(PARTITION BY endUserIds._experience.aaid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
  END AS eVar1Bind,
  EXPLODE(productListItems) AS Product_List,
  commerce.productViews.value AS prodView,
  commerce.purchases.value AS purchase
FROM adobe_analytics_midvalues
WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
LIMIT 100
```

### 將繫結值保留至個別產品的後續相符專案

以下範例查詢會將繫結值儲存至個別產品的後續發生次數。 最低的子查詢會建立值與宣告的捆綁事件上的產品關係。 下一個子查詢會在與個別產品的後續互動中執行該繫結值的歸因。 頂層SELECT會彙總結果以產生報表。

```sql
SELECT
  Product_List.SKU,
  eVar1101ConversionSyntax,
  SUM(prodView) AS Product_Views,
  SUM(purchase) AS Purchases
FROM
(
  SELECT
    Product_List,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'ConversionSyntax_eVar1', eVar1Bind)
      OVER(PARTITION BY AAID, Product_List.SKU
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
    AS eVar1ConversionSyntax,
    prodView,
    purchase
  FROM
  (
    SELECT
      endUserIds._experience.aaid.id AS AAID,
      timestamp,
      CASE WHEN commerce.productViews.value = 1 THEN ATTRIBUTION_LAST_TOUCH(timestamp, 'bindConversionSyntaxMerchVariable_eVar1', _experience.analytics.customDimensions.eVars.eVar1)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW).value
      END AS eVar1Bind,
      EXPLODE(productListItems) AS Product_List,
      commerce.productViews.value AS prodView,
      commerce.purchases.value AS purchase
    FROM adobe_analytics_midvalues
    WHERE commerce.productViews.value = 1 OR commerce.purchases.value = 1 OR _experience.analytics.customDimensions.eVars.eVar1 IS NOT NULL
  )
)
WHERE eVar1ConversionSyntax IS NOT NULL
GROUP BY 1, 2
ORDER BY 3 DESC
LIMIT 100
```

## 后续步骤

閱讀本檔案後，您應能更瞭解如何使用產品語法傳回銷售eVar，並使用轉換變數語法將值繫結至特定產品。

如果您尚未這樣做，請閱讀 [網頁和行動互動的Analytics深入分析檔案](./analytics-insights.md) 下一個。 它提供常見使用案例，並示範如何使用查詢服務，從網頁和行動Adobe Analytics資料建立可行的深入分析。

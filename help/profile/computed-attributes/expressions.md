---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 計算屬性的PQL運算式範例
type: Documentation
description: 計算屬性是用來將事件層級資料彙總到設定檔層級屬性的函式。 這些函式需要使用有效的設定檔查詢語言(PQL)運算式。 本指南概述計算屬性最常使用的PQL運算式。
exl-id: 7c80e2d3-919a-47f9-a59f-833a70f02a8f
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 2%

---

# (Alpha)計算屬性的PQL運算式範例

>[!IMPORTANT]
>
>計算屬性功能目前為Alpha版，並非所有使用者都可使用。 文档和功能可能会发生变化。

在Adobe Experience Platform中，計算屬性是用於彙總事件層級資料至設定檔層級屬性的函式。 這些函式會自動計算，以便用於區段、啟用和個人化。 每個計算屬性都以基本資訊定義，例如名稱和說明、結構描述類別和將保留值的欄位路徑，以及運算式，其計算值是您想要儲存在計算屬性中的值。

計算屬性中使用的運算式是使用 [!DNL Profile Query Language] (PQL)，與Experience Data Model (XDM)相容的查詢語言，專為支援即時客戶個人檔案資料的查詢定義和執行而設計。

計算屬性目前支援下列函式：sum、count、min、max和boolean。 本指南概述一些最常用的PQL運算式，可供您為組織定義自己的計算屬性時使用。 如需PQL的詳細資訊，以及額外格式化指引的連結和支援的查詢範例，請造訪 [PQL概述](../../segmentation/pql/overview.md).

## 串流運算式

下表提供串流模式支援的常用查詢運算式的詳細資訊。

| 描述 | PQL運算式 | 輸入型別：<br/>設定檔或體驗事件(EE[]) | 結果型別 |
|---|---|---|---|
| 過去7天內的影像下載次數。 | xEvent[（時間戳記發生在現在之前7天）和eventType=&quot;download&quot;以及contentType = &quot;image&quot;].count() | 設定檔與EE[] | 整数 |
| 客戶過去7天在體育用品上的花費總和。 | xEvent[（時間戳記發生於現在之前&lt; 7天）及eventType=&quot;transaction&quot;與category = &quot;sporting goods&quot;].sum(commerce.order.priceTotal) | 設定檔與EE[] | 整數或雙精度 |
| 過去7天客戶在體育用品上的平均支出。<br/><br/>**注意：** 需要建立三個計算屬性。 | **ca1：** xEvent[（時間戳記發生於現在之前&lt; 7天）及eventType=&quot;transaction&quot;與category = &quot;sporting goods&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2：** xEvent[（時間戳記發生於現在之前&lt; 7天）及eventType=&quot;transaction&quot;與category = &quot;sporting goods&quot;].count()<br/><br/>**ca3：** ca1 / ca2 | 設定檔與EE[] | 双精度 |
| 客戶過去7天在體育用品上的花費是否超過$100？<br/><br/>**注意：** 需要建立兩個計算屬性。 | **ca1：** xEvent[（時間戳記發生於現在之前&lt; 7天）及eventType=&quot;transaction&quot;與category = &quot;sporting goods&quot;].sum(commerce.order.priceTotal)<br/><br/>**ca2：** ca1 > 100 | 設定檔與EE[] | 布尔值 |
| 客戶在過去7天內有購買過嗎？ | chain(xEvent， timestamp， [答：WHAT(eventType = &quot;transaction&quot;) WHEN（&lt; 7天前）]) | 設定檔與EE[] | 布尔值 |
| 過去7天使用者在體育用品上的花費最低。 | xEvent[（時間戳記發生於現在之前&lt; 7天）及eventType=&quot;transaction&quot;與category = &quot;sporting goods&quot;].min(commerce.order.priceTotal) | 設定檔與EE[] | 整數或雙精度 |
| 過去7天使用者在體育用品上的最高支出。 | xEvent[（時間戳記發生於現在之前&lt; 7天）及eventType=&quot;transaction&quot;與category = &quot;sporting goods&quot;].max(commerce.order.priceTotal) | 設定檔與EE[] | 整數或雙精度 |
| 過去7天內每個已下載產品的下載計數（依產品索引）。 | xEvent[（時間戳記發生在現在之前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， G.count())) | 設定檔與EE[] | 地圖[字串，整數] |
| 過去7天內，每個已下載產品之下載次數的numeric屬性總和，依產品索引。 | xEvent[（時間戳記發生在現在之前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， G.sum(commerce.order.priceTotal))) | 設定檔與EE[] | 地圖[字串，整數] 或地圖[字串，雙精度] |
| 過去7天內，每個已下載產品下載的數值屬性平均值（依產品索引）。<br/><br/>**注意：** 需要建立三個計算屬性。 | **ca1：** xEvent[（時間戳記發生在現在之前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， G.sum(commerce.order.priceTotal)))<br/><br/>**ca2：** xEvent[（時間戳記發生在現在之前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， G.count()))<br/><br/>**ca3：** ca2 / ca1 | 設定檔與EE[] | 地圖[字串，雙精度] |
| 過去7天內，每個已下載產品之下載的數值屬性下限，依產品索引。 | xEvent[（時間戳記發生在現在之前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， G.min(commerce.order.priceTotal))) | 設定檔與EE[] | 地圖[字串，整數] 或地圖[字串，雙精度] |
| 過去7天內，每個已下載產品下載的數值屬性上限，依產品索引。 | xEvent[（時間戳記發生在現在之前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， G.max(commerce.order.priceTotal))) | 設定檔與EE[] | 地圖[字串，整數] 或地圖[字串，雙精度] |
| 設定檔上的數值運算式，未參考事件。 | if(person.gender = &quot;female&quot;， 60， 65) | 配置文件 | 整數或雙精度 |
| 設定檔上的布林運算式，不會參考事件。 | person.birthYear >= 2000 | 配置文件 | 布尔值 |
| 設定檔上的字串運算式，未參考事件。 | if(homeAddress.countryCode in [&quot;US&quot;，&quot;MX&quot;，&quot;CA&quot;]， &quot;NA&quot;， &quot;ROW&quot;) | 配置文件 | 字符串 |

## 批次運算式

下表提供僅可用於批次模式的查詢運算式的詳細資訊，這表示它們目前無法在串流中使用。

| 描述 | PQL運算式 | 輸入型別：<br/>設定檔或體驗事件(EE[]) | 結果型別 |
|---|---|---|---|
| 過去7天內產品下載的數值運算式總和是否超過100 （依產品索引）。 | xEvent[（時間戳記發生在現在之前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， G.sum(commerce.order.priceTotal) > 100)) | 設定檔與EE[] | 地圖[字串，布林值] |
| 過去7天內產品下載的平均數值運算式是否超過100 （依產品索引）。 | xEvent[（時間戳記發生在現在之前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， G.average(commerce.order.priceTotal) > 100)) | 設定檔與EE[] | 地圖[字串，布林值] |
| 過去7天內，每個已下載產品的各種量度累積值，並依產品編制索引。 | xEvent[（時間戳記發生在現在之前7天）和eventType=&quot;download&quot;].groupBy(product)。map((K， G) => mapEntry(K， {&quot;count&quot;： G.count()， &quot;sum&quot;： G.sum(commerce.order.priceTotal)}) | 設定檔與EE[] | 地圖[字串，物件] 其中物件是自訂XDM型別 |

---
keywords: Experience Platform；首頁；熱門主題；邊緣分段；分段；分段服務；分段服務；ui指南；串流邊緣；
solution: Experience Platform
title: Edge Segmentation UI指南
description: 邊緣區段是即時在邊緣評估Platform中區段的能力，可啟用相同頁面和下一頁個人化使用案例。
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# 边缘分段 UI 指南

>[!NOTE]
>
>邊緣區段現在可供所有Platform使用者普遍使用。 如果您在Beta版期間建立邊緣區段，這些區段將繼續運作。

邊緣區段是即時評估Adobe Experience Platform中區段的能力 [在邊緣](../../edge/home.md)，啟用相同頁面和下一頁個人化使用案例。

>[!IMPORTANT]
>
> 邊緣資料將會儲存在距離收集位置最近的邊緣伺服器位置，而且可能會儲存在指定為Adobe Experience Platform資料中心中心（或主體）以外的位置。
>
> 此外，邊緣區段引擎只會處理邊緣區段的請求，該邊緣區段有 **一** 主要標籤的身分，與非邊緣型主要身分一致。

## 邊緣細分查詢型別 {#query-types}

目前只有選取的查詢型別可使用邊緣區段進行評估。 以下小節提供可用邊緣區段評估的查詢型別清單，以及目前不支援的查詢型別清單。

如果查詢符合下表中列出的任何條件，則可以使用邊緣分段來評估查詢。

>[!NOTE]
>
>如果查詢符合下表中的任何查詢型別，則會自動使用邊緣分段來評估。 系統會根據查詢運算式自動判斷此能力。

| 查詢型別 | 详细信息 | 示例 | PQL範例 |
| ---------- | ------- | ------- | ----------- |
| 單一事件 | 任何區段定義，會參照沒有時間限制的單一傳入事件。 | 已將專案新增至購物車的使用者。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 單一設定檔 | 任何參考單一設定檔屬性的區段定義 | 美國居民。 | `homeAddress.countryCode = "US"` |
| 參考設定檔的單一事件 | 任何區段定義，會參照一或多個設定檔屬性，以及沒有時間限制的單一傳入事件。 | 居住在美國的人造訪了首頁。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")])` |
| 否定具有設定檔屬性的單一事件 | 任何參考否定單一傳入事件和一個或多個設定檔屬性的區段定義 | 居住在美國且有 **not** 造訪了首頁。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| 時間範圍內的單一事件 | 任何參考一段時間內單一傳入事件的區段定義。 | 過去24小時內造訪過首頁的人。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| 時間範圍內具有設定檔屬性的單一事件 | 任何區段定義，會參照一段時間內的一或多個設定檔屬性和單一傳入事件。 | 居住在美國的人在過去24小時內瀏覽過首頁。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| 否定時間範圍內具有設定檔屬性的單一事件 | 任何區段定義，會參照一或多個設定檔屬性，以及一段時間內否定單一傳入事件。 | 居住在美國且有 **not** 在過去24小時內造訪了首頁。 | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)]))` |
| 24小時時間範圍內的頻率事件 | 任何區段定義，會參照在24小時之時間範圍內發生特定次數的事件。 | 造訪過首頁的人 **至少** 過去24小時內5次。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小時時間範圍內具有設定檔屬性的頻率事件 | 任何區段定義，會參照一或多個設定檔屬性，以及在24小時之時間範圍內發生特定次數的事件。 | 造訪首頁的美國人 **至少** 過去24小時內5次。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小時時間範圍內具有設定檔的否定頻率事件 | 任何區段定義，會參照一或多個設定檔屬性，以及在24小時內特定次數內發生的否定事件。 | 尚未造訪過首頁的人 **更多** 在過去24小時內超過五次。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| 24小時時間設定檔內有多次傳入點選 | 任何區段定義，會參照在24小時內發生的時間範圍內所發生的多個事件。 | 造訪過首頁的人 **或** 在過去24小時內造訪過結帳頁面。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 在24小時時間範圍內有多個具有設定檔的事件 | 任何區段定義，會參照在24小時時間範圍內發生的一或多個設定檔屬性和多個事件。 | 造訪過首頁的美國人 **和** 在過去24小時內造訪過結帳頁面。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 區段區段 | 包含一或多個批次或串流區段的任何區段定義。 | 居住在美國且處於「現有區段」區段的人員。 | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| 參考地圖的查詢 | 任何參照屬性對應的區段定義。 | 已根據外部區段資料新增至購物車的使用者。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

區段定義會 **not** 在以下情況下啟用邊緣分段：

- 區段定義包含單一事件和 `inSegment` 事件。
   - 但是，如果區段包含在 `inSegment` 事件只是設定檔，區段定義 **將** 啟用邊緣區段。

## 后续步骤

本指南說明如何在Adobe Experience Platform上使用邊緣區段來評估區段。 若要進一步瞭解如何使用Experience Platform使用者介面，請閱讀 [區段使用手冊](./overview.md). 若要瞭解如何使用Experience PlatformAPI執行類似動作和使用區段，請造訪 [edge segmentation API指南](../api/edge-segmentation.md).

## 附录

下節列出與邊緣細分相關的常見問題：

### 在Edge Network上使用區段需要多久時間？

在Edge Network上提供區段最多需要一小時。
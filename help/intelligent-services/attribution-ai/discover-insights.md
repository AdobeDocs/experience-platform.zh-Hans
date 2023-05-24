---
keywords: Experience Platform；insights；歸因ai；熱門主題；歸因ai insights
feature: Attribution AI
title: 探索Attribution AI中的深入分析
description: 本檔案可作為在AdobeIntelligent Services使用者介面中與服務執行個體見解互動的指南。
exl-id: 6b8e51e7-1b56-4f4e-94cf-96672b426c88
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 0%

---

# 探索Attribution AI中的深入分析

Attribution AI服務例項提供深入分析，以協助您做出與行銷表現和投資報酬率相關的行銷決策，並加以衡量。 選取服務執行個體可提供視覺效果和篩選器，協助您瞭解客戶歷程每個階段每個客戶互動的影響。

本檔案可作為在AdobeIntelligent Services使用者介面中與服務執行個體見解互動的指南。

## 快速入门

若要運用Attribution AI的深入分析，您必須有具備成功執行狀態的服務執行個體。 若要建立新的服務執行個體，請造訪 [Attribution AI使用者介面指南](./user-guide.md). 如果您最近建立了服務執行個體，但仍在訓練和評分，請等待24小時讓執行個體完成執行。

## 服務執行個體深入分析概觀

在 [!DNL Adobe Experience Platform] UI，選取 **[!UICONTROL 服務]** 左側導覽列中。 此 **[!UICONTROL 服務]** 瀏覽器隨即出現，並顯示可用的AdobeIntelligent Services。 在Attribution AI的容器中，選取 **[!UICONTROL 開啟]**.

![存取您的執行個體](./images/insights/open_Attribution_ai.png)

便會顯示「Attribution AI服務」頁面。 此頁面列出Attribution AI的服務執行處理並顯示其相關資訊，包括執行處理名稱、轉換事件、執行處理的執行頻率，以及上次更新的狀態。 選取服務執行個體名稱以開始。

>[!NOTE]
>
>只能選取已完成成功評分回合的服務執行個體。

![建立例項](./images/insights/select-service-instance.png)

接著，該服務執行個體的深入分析頁面就會顯示，其中提供您視覺效果和許多篩選器，讓您與資料互動。 本指南會詳細說明視覺效果和篩選器。

![設定頁面](./images/insights/landing-page.png)

### 服務執行個體詳細資訊

若要檢視服務執行處理的其他詳細資訊，請選取 **[!UICONTROL 顯示更多]** 右上角。

![顯示更多](./images/insights/show-more.png)

詳細清單隨即顯示。 如需所列任何屬性的詳細資訊，請造訪 [Attribution AI使用手冊](./user-guide.md).

![顯示詳細資料](./images/insights/advanced-details.png)

### 編輯執行個體

若要編輯執行個體，請選取 **[!UICONTROL 編輯]** ，位於右上角導覽列中。
![按一下編輯按鈕](./images/insights/edit-button.png)

「編輯」對話方塊會出現，讓您編輯執行個體的名稱、說明和評分頻率。 如果例項狀態為停用，則無法編輯評分頻率。 若要確認變更並關閉對話方塊，請選取 **[!UICONTROL 儲存]** 右下角。

![編輯彈出視窗](./images/insights/edit-popover.png)

### 更多動作 {#more-actions}

此 **[!UICONTROL 更多動作]** 按鈕位於右上角導覽列旁邊 **[!UICONTROL 編輯]**. 選取 **[!UICONTROL 更多動作]** 開啟下拉式清單，讓您選取下列其中一個操作：

- **[!UICONTROL 原地複製]**：複製執行個體。
- **[!UICONTROL 刪除]**：刪除執行個體。
- **[!UICONTROL 下載摘要資料]**：下載包含摘要資料的CSV檔案。
- **[!UICONTROL 存取分數]**：選取 **[!UICONTROL 存取分數]** 將您重新導向至 [存取Attribution AI教學課程的分數](./download-scores.md).
- **[!UICONTROL 檢視執行歷程記錄]**：包含與服務執行個體相關聯之所有評分回合清單的彈出視窗會出現。

![更多動作](./images/insights/more-actions.png)

## 篩選您的資料

Attribution AI深入分析可讓您篩選資料，並根據您選取的篩選器自動更新UI視覺效果。

### 轉換事件

當您在Attribution AI中建立新執行個體時，必填欄位之一是「轉換事件」。 轉換事件是識別行銷活動影響的業務目標，例如電子商務訂單、店內購買和網站造訪。

在執行個體中， **[!UICONTROL 轉換事件]** 下拉式清單可讓您選取為您的執行個體定義的任何事件，以篩選您的資料。 選取特定事件會變更UI視覺效果，使其僅填入屬於這些事件的轉換。

![轉換事件](./images/insights/conversion-event.png)

### 归因模型

選取 **[!UICONTROL 歸因模型]** 會開啟下拉式清單，其中包含所有可用的不同歸因模型。 您可以選取多個模型來比較結果。 如需不同歸因模型及其運作方式的詳細資訊，請造訪 [Attribution AI](./overview.md) 概觀，其中包含每個模型資訊的表格。

![歸因模型](./images/insights/attribution-model.png)

### 地區

>[!NOTE]
>
>此篩選條件只有在您已執行選擇性步驟時才會出現 [區域型模型](./user-guide.md#region-based-modeling-optional) 在建立服務執行個體時，請參閱Attribution AI使用者介面指南。

此篩選可讓您選取您在建立執行個體過程中設定的任何區域。

### 新增篩選器

您可以選取「 」，新增其他篩選器 **篩選** 圖示以開啟 **[!UICONTROL 新增篩選器]** 彈出視窗。 此 **[!UICONTROL 新增篩選器]** 彈出視窗可讓您依「頻道」、「地理」、「媒體型別」和「產品」來篩選。 彈出視窗只會填入服務執行個體的適用篩選器。 例如，如果您未提供地理資料或媒體型別，這些篩選屬性將無法用於您的執行個體。

![額外的篩選器](./images/insights/additional-filters.png)

![篩選彈出視窗](./images/insights/filter-popover.png)

- **[!UICONTROL 頻道]：** 選取管道屬性可讓您篩選任何可用的行銷管道。 您可以選取多個管道來比較。
- **[!UICONTROL 地理位置]：** 選取地理位置屬性可讓您根據以區域為基礎的模型來篩選國家/地區代碼。 根據您的資料，此篩選器可能存在，也可能不存在。 國家/地區代碼長度為兩個字元。 檢視完整的國家/地區代碼清單 [此處](https://datahub.io/core/country-list).
- **[!UICONTROL 媒體型別]：** 選取媒體型別屬性可讓您篩選任何已定義的媒體型別。
- **[!UICONTROL 產品]：** 選取產品屬性可讓您從建立執行個體時最初擷取的任何產品中進行篩選。

### Date Range

選取行事曆圖示以開啟日期範圍彈出視窗。 開始和結束轉換事件日期會決定UI中填入的資料量。 您可以選擇縮小或擴大日期範圍，以集中或擴大填入的資料量。

![日期範圍](./images/insights/display-date-range.png)

## 您的資料概觀

此 **[!UICONTROL 概觀]** 卡片會依歸因模型顯示您的總轉換。 總數會根據您使用本檔案先前概述之篩選條件進行搜尋的特定方式而變更。 選取更多模型會在「概述」中新增其他圓圈，每個圓圈都有自己的顏色，與圖例相對應。

![概述](./images/insights/Overview.png)

## 每週趨勢

此 **[!UICONTROL 每週趨勢]** 卡片會依您在篩選程式期間設定的日期範圍來劃分總轉換。

選取右上角的省略符號 **每週趨勢** 卡片會顯示下拉式清單，讓您選取每日、每週或每月趨勢。

將滑鼠指標暫留在特定歸因模型的資料行上，會建立一個彈出視窗，顯示該日期的轉換總數。

![趨勢](./images/insights/weekly-trends.png)

## 依管道劃分

此 **[!UICONTROL 依管道劃分]** 卡片可用來決定與每個管道相關的轉換總數。 這張卡片可用來協助您決定每個管道的有效性及投資報酬率。

選取右上角的省略符號 **[!UICONTROL 依管道劃分]** 卡片會開啟下拉式清單，讓您根據接觸點填入資料。

![劃分頻道](./images/insights/channel-breakdown.png)

## 熱門行銷活動

此 **[!UICONTROL 熱門行銷活動]** 卡片會顯示行銷活動的概覽，以及行銷活動在每個管道中的執行方式。 此卡片可協助您的團隊瞭解特定頻道的特定行銷活動的成效，並提供諸如您應進一步投資哪些行銷活動等見解。

![熱門行銷活動](./images/insights/top-campaigns.png)

## 依接觸點位置劃分

選取 **[!UICONTROL 路徑分析]** 標籤載入 **[!UICONTROL 依接觸點位置劃分]** 和 **[!UICONTROL 排名在前的轉換路徑]** 圖表。

此 **[!UICONTROL 依接觸點位置劃分]** 圖表是依接觸點位置劃分的已歸因轉換劃分，比較對象是所有轉換路徑。 此圖表可協助您瞭解哪些接觸點在轉換路徑的不同階段中更有效率。 這些階段包括入門者、玩家和接近者。

- **入門：** 表示此接觸點是轉換路徑中的首次接觸。
- **播放器：** 表示此接觸點不是導致轉換的第一個或最後一個接觸。
- **更靠近：** 表示此接觸點是轉換前的最後一次接觸。

>!![NOTE]
歸因模型在所有接觸點和位置的貢獻百分比總和應等於100。

![使用者路徑劃分接觸點](./images/insights/user-paths.png)

## 排名在前的轉換路徑

此 **[!UICONTROL 排名在前的轉換路徑]** 圖表顯示所選區域中排名在前的轉換路徑上的受影響分數和演演算法分數。 此圖表可讓您視覺化哪些接觸點對轉換有貢獻，以及每個接觸點的歸因分數。 您可以使用此資訊來檢視特定區域中最頻繁的路徑，並檢視不同接觸點集之間是否有任何模式出現。

![最常見的使用者路徑](./images/insights/Touchpoint-paths.png)

## 接觸點有效性

選取 **[!UICONTROL 接觸點有效性]** 標籤載入 **[!UICONTROL 接觸點有效性]** 卡片。 此卡片會使用Attribution AI的資料分佈，顯示每個接觸點的資訊。 此資料表的資料只會針對特定的時段產生，如 **[!UICONTROL 截至]** 日期在卡片的右上方。

![接觸點有效性選取](./images/insights/Touchpoint-effectiveness.png)

您可以使用 **[!UICONTROL 接觸點有效性]** 卡片資訊，以瞭解接觸點如何有助於轉換。 您也可以透過下列效能量度檢視每個接觸點的有效性：

**接觸的路徑**：此量度顯示達成/未達成接觸點轉換的路徑百分比。 如果實現轉換的路徑與未實現轉換的路徑之間的比率（百分比）很高，您就會看到較高的已歸因轉換。

![接觸的路徑量度](./images/insights/Touchpoint-metrics.png)

**效率測量**：此量度以1至5的刻度顯示星星。 此比例代表接觸點對進行轉換的相對重要性。

>[!NOTE]
接觸點數量較多無法保證效率測量值較高。

**總數量**：使用者接觸接觸點的彙總次數。 這包括出現在達成轉換的路徑上的接觸點，以及未產生轉換的路徑。

## 后续步骤

篩選完資料並顯示適當資訊後，您就可以選擇存取分數。 如需如何存取評分的深入指南，請造訪 [在Attribution AI中存取分數](./download-scores.md) 教學課程。 此外，您也可以下載摘要資料，如所示 [更多動作](#more-actions). 選取「下載摘要資料」可下載按日期彙總的摘要資料。

## 其他资源

以下影片旨在協助您瞭解如何使用Attribution AI深入分析頁面來瞭解行銷管道和行銷活動的ROI。

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)

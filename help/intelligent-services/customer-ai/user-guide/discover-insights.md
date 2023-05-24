---
keywords: Experience Platform；深入分析；customer ai；熱門主題；customer ai深入分析
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 探索Customer AI的深入分析
description: 本檔案可作為在Intelligent Services Customer AI使用者介面中與服務執行個體見解互動的指南。
exl-id: 8aaae963-4029-471e-be9b-814147a5f160
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '2079'
ht-degree: 1%

---

# 探索Customer AI的深入分析

Customer AI是Intelligent Services的一部分，可讓行銷人員運用Adobe Sensei來預測客戶的下一個動作。 Customer AI 用于生成自定义倾向分数，如个人档案大规模的流失率和转化率。不必將業務需求轉換為機器學習問題、挑選演演算法、訓練或部署，即可完成這項工作。

本檔案可作為在Intelligent Services Customer AI使用者介面中與服務執行個體見解互動的指南。

## 快速入门

若要運用Customer AI的深入分析，您必須有可成功執行狀態的服務執行個體。 若要建立新的服務執行個體，請造訪 [設定Customer AI執行個體](./configure.md). 如果您最近建立了服務執行個體，但仍在訓練和評分，請等待24小時讓執行個體完成執行。

## 服務執行個體總覽

在 [!DNL Adobe Experience Platform] UI，選取 **[!UICONTROL 服務]** 左側導覽列中。 此 *服務* 瀏覽器隨即出現，並顯示可用的Intelligent Services。 在Customer AI的容器中，選取 **[!UICONTROL 開啟]**.

![存取您的執行個體](../images/insights/navigate-to-service.png)

Customer AI服務頁面隨即顯示。 此頁面列出Customer AI的服務執行個體並顯示其相關資訊，包括執行個體名稱、傾向型別、執行個體執行頻率以及上次更新狀態。

>[!NOTE]
>
>只有已完成成功評分回合的服務執行個體才會有深入分析。

![建立例項](../images/insights/dashboard.png)

選取服務執行個體名稱以開始。

![建立例項](../images/insights/click-the-name.png)

接著，會出現該服務執行個體的深入分析頁面，其中包含可選取的選項 **[!UICONTROL 最新分數]** 或 **[!UICONTROL 效能摘要]**. 預設標籤 **[!UICONTROL 最新分數]** 提供資料的視覺效果。 本指南會詳細說明視覺效果以及您可以對資料執行的操作。

此 **[!UICONTROL 效能摘要]** 索引標籤會顯示每個傾向性貯體的實際流失率或轉換率。 若要深入瞭解，請參閱以下章節： [績效摘要量度](#performance-metrics).

![設定頁面](../images/insights/landing_page_insights.png)

## 服務執行個體詳細資訊

檢視服務執行個體詳細資訊的方式有兩種：從儀表板或服務執行個體內。

### 服務執行個體儀表板

若要在儀表板中檢視服務執行個體詳細資訊的概觀，請選取服務執行個體容器，以避免附加到名稱的超連結。 這會開啟一個提供其他詳細資訊的右側邊欄。 控制項包含下列內容：

- **[!UICONTROL 編輯]**：選取 **[!UICONTROL 編輯]** 可讓您修改現有的服務執行個體。 您可以編輯執行個體的名稱、說明和評分頻率。
- **[!UICONTROL 原地複製]**：選取 **[!UICONTROL 原地複製]** 複製目前選取的服務執行個體設定。 然後您可以修改工作流程以進行微幅調整，並將其重新命名為新例證。
- **[!UICONTROL 刪除]**：您可以刪除服務執行個體，包括任何歷史執行。
- **[!UICONTROL 資料來源]**：此執行個體所使用資料集的連結。
- **[!UICONTROL 執行頻率]**：評分回合發生的頻率及時間。
- **[!UICONTROL 分數定義]**：您為此執行個體設定的目標快速概覽。

![](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>如果評分回合失敗，則會提供錯誤訊息。 錯誤訊息列於下方 **上次執行詳細資料** 右側邊欄中，只有失敗的執行才看得見。

![執行訊息失敗](../images/insights/failed-run.png)

### 顯示更多深入分析下拉式清單

檢視服務執行個體其他詳細資訊的第二種方式位於深入分析頁面中。 選取 **[!UICONTROL 顯示更多]** 填入下拉式清單。 所列出的詳細資訊包括分數定義、建立時間、傾向型別和使用的資料集。 如需所列任何屬性的詳細資訊，請造訪 [設定Customer AI執行個體](./configure.md).

![顯示更多](../images/insights/landing-show-more.png)

### Customer AI資料集預覽彈出視窗

如果Customer AI使用多個資料集，則會出現標示為 **[!UICONTROL 多個]** 後跟括弧中的資料集數目 `()` 「 」提供。

![多個資料集](../images/insights/insights-multi-datasets.png)

選取多個資料集連結會開啟Customer AI資料集預覽彈出視窗。 預覽中的每個顏色代表一個資料集，如資料集欄左側的顏色索引鍵所示。 在此範例中，您只能看到 **資料集1** 包含 `PROP1` 欄。

![顯示更多](../images/insights/dataset-preview.png)

### 編輯執行個體

若要編輯執行個體，請選取 **[!UICONTROL 編輯]** ，位於右上角導覽列中。

![按一下編輯按鈕](../images/insights/edit-button.png)

「編輯」對話方塊會出現，讓您編輯執行個體的名稱、說明、狀態和評分頻率。 若要確認變更並關閉對話方塊，請選取 **[!UICONTROL 儲存]** 右下角。

![編輯彈出視窗](../images/insights/edit-instance.png)

### 更多動作

此 **[!UICONTROL 更多動作]** 按鈕位於右上角導覽列旁邊 **[!UICONTROL 編輯]**. 選取 **[!UICONTROL 更多動作]** 開啟下拉式清單，讓您選取下列其中一個操作：

- **[!UICONTROL 原地複製]**：選取 **[!UICONTROL 原地複製]** 復制服務執行個體設定。 然後您可以修改工作流程以進行微幅調整，並將其重新命名為新例證。
- **[!UICONTROL 刪除]**：刪除執行個體。
- **[!UICONTROL 存取分數]**：選取 **[!UICONTROL 存取分數]** 開啟對話方塊，提供連結至 [下載Customer AI分數](./download-scores.md) 在教學課程中，此對話方塊也會提供進行API呼叫所需的資料集ID。
- **[!UICONTROL 檢視執行歷程記錄]**：包含與服務執行個體相關聯之所有評分回合清單的對話方塊隨即顯示。

![更多動作](../images/insights/more-actions.png)

## 評分摘要 {#scoring-summary}

評分摘要會顯示已評分的個人檔案總數，並將其分類為包含高、中和低傾向的貯體。 傾向值區是根據分數範圍來確定，低值小於24，中值為25至74，而高值大於74。 每個貯體都有對應圖例的顏色。

>[!NOTE]
>
>如果是轉換傾向分數，高分會以綠色顯示，低分則會以紅色顯示。 如果您預測的是流失傾向，這會逆轉，高分數為紅色，低分數為綠色。 無論您選擇哪種傾向型別，中段都會保持黃色。

![評分摘要](../images/insights/scoring-summary.png)

您可以將滑鼠游標停留在鈴聲上的任何顏色上，以檢視其他資訊，例如屬於貯體的設定檔百分比和總數。

![](../images/insights/scoring-ring.png)

## 分數的分佈

此 **[!UICONTROL 分數的分佈]** 卡片會根據分數為您提供母體的視覺摘要。 您在中看到的顏色 [!UICONTROL 分數的分佈] 卡片代表產生的傾向分數型別。 暫留在任何評分分配上，可提供屬於該分配的確切盤點。

![分數的分佈](../images/insights/distribution-of-scores.png)

## 影響因素

對於每個評分貯體，都會產生一張卡片，顯示該貯體的前10個影響因素。 影響因素會提供您更多詳細資料，說明您的客戶為何屬於各種分數貯體。

![影響因素](../images/insights/influential-factors.png)

### 影響因素明細

將滑鼠指標暫留在任何主要影響因素上，可進一步劃分資料。 系統會概述特定設定檔為何屬於傾向性貯體。 根據因子，您可能會獲得數字、分類或布林值。 下列範例會依地區顯示分類值。

![深入分析熒幕擷圖](../images/insights/drilldown.png)

此外，透過深入分析，您可以比較分佈因數（如果它出現在兩個或多個傾向性貯體中），並使用這些值建立更具體的區段。 下列範例說明第一個使用案例：

![](../images/insights/drilldown-compare.png)

您可以看到轉換傾向較低的設定檔最近造訪adobe.com網頁的可能性較低。 「上次造訪間隔天數」因子的涵蓋範圍只有8%，而中傾向個人檔案為26%。 使用這些數字，您可以比較係數每個時段內的分配。 此資訊可用於推斷網路造訪中的造訪間隔在低傾向性貯體中的影響力較小，因為在中傾向性貯體中。

### 建立區段

選取 **[!UICONTROL 建立區段]** 低、中和高傾向的任何貯體中的按鈕會將您重新導向至區段產生器。

>[!NOTE]
>
>此 **[!UICONTROL 建立區段]** 只有在資料集啟用即時客戶設定檔時，按鈕才可用。 如需如何啟用即時客戶個人檔案的詳細資訊，請瀏覽 [即時客戶個人檔案總覽](../../../rtcdp/overview.md).

![按一下建立區段](../images/insights/influential-factors-create-segment.png)

![建立區段](../images/insights/create-segment.png)

區段產生器可用來定義區段。 選取 **[!UICONTROL 建立區段]** Customer AI會從「深入分析」頁面自動將選取的貯體資訊新增至區段。 若要完成建立區段，只需填寫 **名稱** 和 **說明** 位於區段產生器使用者介面右側邊欄的容器。 為區段指定名稱和說明後，選取 **[!UICONTROL 儲存]** 右上角。

>[!NOTE]
>
>由於傾向分數會寫入個別設定檔，因此可像任何其他設定檔屬性一樣，用於區段產生器。 當您導覽至區段產生器以建立新區段時，您可以在名稱空間Customer AI下看到所有各種傾向分數。

![區段填入](../images/insights/segment-saving.png)

若要在Platform UI中檢視您的新區段，請選取 **[!UICONTROL 區段]** 左側導覽列中。 此 **[!UICONTROL 瀏覽]** 頁面隨即顯示，並顯示所有可用的區段。

![您的所有區段](../images/insights/Segments-dashboard.png)

## 歷史績效 {#historical-performance}

此 **[!UICONTROL 效能摘要]** 索引標籤會顯示實際流失率或轉換率，並分隔為Customer AI評分的每個傾向貯體。

![效能摘要標籤](../images/insights/summary_tab.png)

一開始只會顯示預期的比率（虛線）。 當評分回合尚未發生且資料尚不可使用時，會顯示預期比率。 不過，一旦結果視窗已過，預期比率會以實際比率（實線）取代。

將滑鼠游標停留在明細行上會顯示該時段中該日的日期和實際/預期費率。

![貯體範例](../images/insights/churn_tab.png)

您可以篩選要顯示的預期和實際費率的時間範圍。 選取 **行事曆圖示** ![圖示](../images/insights/calendar_icon.png)然後選取新的日期範圍。 每個貯體中的結果都會更新並在新日期範圍內顯示。

![日期選擇器](../images/insights/date_selector.png)

### 個別評分回合率

下半部 **[!UICONTROL 效能摘要]** 索引標籤會顯示每個個別評分回合的結果。 選取右上方的下拉式清單日期，以顯示不同評分回合的結果。

根據您預測的是流失率或轉換率， [!UICONTROL 分數的分佈] 圖表顯示每個增量中流失/已轉換和未流失/未轉換的設定檔分佈。

![個人得分](../images/insights/scoring_tab.png)

## 模型評估 {#model-evaluation}

除了在「歷史績效」標籤上追蹤一段時間內的預測和實際結果外，行銷人員在「模型評估」標籤上對於模型品質的透明度甚至更高。 您可以使用提升度和收益圖表來判斷使用預測模型與隨機鎖定目標之間的差異。 此外，您還能判斷在每個分數截止點會擷取多少個正面結果。 這對於細分及調整投資報酬率與行銷動作非常有用。

### 提升圖

![提升圖](../images/user-guide/lift-chart.png)

提升圖會衡量使用預測性模型而非隨機目標定位的改善情形。

高品質的模型指標包括：

- 前幾個十分位數中的高提升度值。 這表示該模型擅長識別具有最高興趣行動傾向的使用者。
- 遞減提升度值。 這表示分數較高的客戶比分數較低的人更有可能採取感興趣的行動。

### 收益圖

![收益表](../images/user-guide/gains-chart.png)

累積收益圖會衡量將分數鎖定在高於特定臨界值時所擷取的積極結果的百分比。 依高到低的傾向分數為客戶排序後，母體會分成十等分 — 10個大小相等的群組。 完美的模型會以最高分的十分位數來擷取所有積極的結果。 基線隨機鎖定目標方法會依群組規模的比例擷取積極結果，鎖定目標30%的使用者將擷取30%的結果。

高品質的模型指標包括：

- 累積收益會快速接近100%。
- 此模型的累計收益曲線比較靠近圖表的左上角。
- 累計收益表可用來決定細分和目標定位的分數截斷點。 例如，如果模型在前兩個分數十分位數中擷取到70%的正面結果，則以百分位數分數> 80的使用者為目標，預計將擷取大約70%的正面結果。

### AUC （曲線下的區域）

AUC反映了分數排名與預測目標發生之間的關係強度。 一個 **AUC** 為0.5表示此模型並不比隨機猜測好。 一個 **AUC** 其中1表示模型可完美預測誰會採取相關動作。

## 后续步骤

本檔案概述Customer AI服務執行個體提供的深入分析。 您現在可以繼續上的教學課程 [在Customer AI中下載分數](./download-scores.md) 或瀏覽其他 [Adobe智慧型服務](../../home.md) 提供的指南。

## 其他资源

以下影片概述如何使用Customer AI檢視模型和影響因素的輸出。

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)

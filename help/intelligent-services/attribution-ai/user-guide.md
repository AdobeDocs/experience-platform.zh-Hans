---
keywords: Experience Platform；使用手冊；attribution ai；熱門主題；地區
feature: Attribution AI
title: Attribution AI UI指南
description: 本檔案可作為在Intelligent Services使用者介面中與Attribution AI互動的指南。
exl-id: 32e1dd07-31a8-41c4-88df-8893ff773f79
source-git-commit: 66d20dc1141ff33211635ba74d320350f8b27fb7
workflow-type: tm+mt
source-wordcount: '2443'
ht-degree: 1%

---

# Attribution AIUI指南

Intelligent Services中的Attribution AI是多管道演演算法歸因服務，可計算客戶互動對指定結果的影響和累加影響。 利用 Attribution AI，营销人员可以通过了解客户历程各个阶段每个客户互动的影响来衡量和优化营销和广告支出。

本檔案可作為在Intelligent Services使用者介面中與Attribution AI互動的指南。

## 创建模型

在 [!DNL Adobe Experience Platform] UI，選取 **[!UICONTROL 服務]** 左側導覽列中。 此 **[!UICONTROL 服務]** 瀏覽器隨即出現，並顯示可用的Adobe智慧型服務。 在Attribution AI的容器中，選取 **[!UICONTROL 開啟]**.

![存取您的模型](./images/user-guide/open_Attribution_ai.png)

便會顯示「Attribution AI服務」頁面。 此頁面列出Attribution AI的服務模型並顯示其相關資訊，包括模型名稱、轉換事件、模型執行頻率以及上次更新狀態。

您可以找到 **[!UICONTROL 已評分的轉換事件總數]** 位於右下角的量度 **[!UICONTROL 建立模型]** 容器。 此量度會追蹤Attribution AI在目前日曆年度所評分的轉換事件總數，包括所有沙箱環境及任何已刪除的服務模型。

![總轉換次數](./images/user-guide/total_conversions.png)

您可以使用UI右側的控制項來編輯、複製和刪除服務模型。 若要顯示這些控制項，請從現有的控制項中選取模型 **[!UICONTROL 服務模式]**. 控制項包含下列資訊：

- **[!UICONTROL 編輯]**：選取 **[!UICONTROL 編輯]** 可讓您修改現有的服務模型。 您可以編輯模型的名稱、說明、狀態、評分頻率，以及其他評分資料集欄。
- **[!UICONTROL 原地複製]**：選取 **[!UICONTROL 原地複製]** 複製所選的服務模型。 然後您可以修改工作流程以進行微幅調整，並將其重新命名為新模型。
- **[!UICONTROL 刪除]**：您可以刪除服務模型，包括任何歷史執行。 對應的輸出資料集將會從Platform中刪除。 不過，同步至即時客戶設定檔的分數不會刪除。
- **[!UICONTROL 資料來源]**：使用中資料集的連結。 如果Attribution AI使用多個資料集，則會顯示「多個」，後面接著資料集數目。 選取超連結後，會顯示資料集預覽彈出視窗。
- **[!UICONTROL 上次執行詳細資料]**：這僅在執行失敗時顯示。 此處顯示執行失敗原因的資訊，例如錯誤代碼。

![側窗格](./images/user-guide/multiple-datasets-pane.png)

- **[!UICONTROL 轉換事件]**：針對此模型設定的轉換事件快速概覽。
- **[!UICONTROL 回顧期間]**：您定義的時間範圍，指出納入轉換事件接觸點前的天數。
- **[!UICONTROL 接觸點]**：建立此模型時定義的所有接觸點清單。

![](./images/user-guide/side_panel_2.png)

選取 **[!UICONTROL 建立模型]** 以開始。

![建立模型](./images/user-guide/landing_page.png)

接著，會顯示Attribution AI的設定頁面，您可以在其中提供服務模式的名稱和說明（選擇性）。

![命名模型](./images/user-guide/naming_instance.png)

## 选择数据 {#select-data}

<!-- https://www.adobe.com/go/aai-select-data -->

在設計上，Attribution AI可以使用Adobe Analytics、體驗事件和消費者體驗事件資料來計算歸因分數。 選取資料集時，只會列出與Attribution AI相容的資料集。 若要選取資料集，請選取(**+**)符號，或選取核取方塊一次新增多個資料集。 您也可以使用搜尋選項來快速尋找您感興趣的資料集。

選取您要使用的資料集後，選取 **[!UICONTROL 新增]** 按鈕以將資料集新增至資料集預覽窗格。

![選取資料集](./images/user-guide/select-datasets.png)

選取資訊圖示 ![資訊圖示](./images/user-guide/info-icon.png) 在資料集旁邊，會開啟「資料集預覽」彈出視窗。

![選取並搜尋資料集](./images/user-guide/dataset-preview.png)

資料集預覽包含上次更新時間、來源結構描述和前10欄的預覽等資料。

選取 **[!UICONTROL 儲存]** 以在工作流程中移動時儲存草稿。 您也可以儲存草稿模型組態，並移至工作流程中的下一個步驟。 使用 **[!UICONTROL 儲存並繼續]** 在模型組態期間建立和儲存草稿。 此功能可讓您建立和儲存模型設定的草稿，當您必須在設定工作流程中定義許多欄位時，此功能特別有用。

![「資料科學服務」Attribution AI標籤的「建立工作流程」中會反白顯示「儲存並儲存並繼續」。](./images/user-guide/aai-save-save-&-exit.png)

### 資料集完整性 {#dataset-completeness}

<!-- https://www.adobe.com/go/aai-dataset-completeness -->

在資料集預覽中，是資料集完整性百分比值。 此值可讓您快速瞭解資料集中有多少欄是空白/空值。 如果資料集包含許多缺少的值，而這些值是在其他地方擷取的，強烈建議您納入包含缺少值的資料集。

>[!NOTE]
>
>資料集完整度是使用Attribution AI的最大訓練時段（一年）來計算。 這表示在顯示您的資料集完整性值時，不會考慮超過一年的資料。

![資料集完整性](./images/user-guide/dataset-completeness.png)

### 選取身分 {#identity}

您現在可以根據身分對應（欄位）將多個資料集聯結到彼此中。 您必須選取身分型別（也稱為「身分名稱空間」）及該名稱空間中的身分值。 如果您在相同名稱空間下的結構描述中將多個欄位指派為身分，則所有指派的身分值都會出現在身分下拉式清單中（前面有名稱空間），例如 `EMAIL (personalEmail.address)` 或 `EMAIL (workEmail.address)`.

>[!IMPORTANT]
>
>您選取的每個資料集都必須使用相同的身分型別（名稱空間）。 在身分資料行內的身分型別旁會出現綠色核取記號，表示資料集相容。 例如，使用電話名稱空間和 `mobilePhone.number` 做為識別碼，其餘資料集的所有識別碼都必須包含並使用電話名稱空間。

若要選取識別，請選取位於識別欄中的加底線的值。 此時會出現「選取身分」彈出視窗。

![選取相同的名稱空間](./images/user-guide/aai-identity-map-save-and-exit.png)

如果名稱空間中有多個身分可用，請務必為您的使用案例選取正確的身分欄位。 例如，電子郵件名稱空間中有兩個電子郵件身分識別可用，一個是工作電子郵件，一個是個人電子郵件。 視使用案例而定，個人電子郵件更有可能被填寫，且在個人預測中更實用。 這表示您可以選取 `EMAIL (personalEmail.address)` 作為您的身分。

![未選取資料集索引鍵](./images/user-guide/aai-identity-namespace.png)

>[!NOTE]
>
> 如果資料集沒有有效的身分型別（名稱空間），您必須使用設定主要身分，並將其指派給身分名稱空間 [結構描述編輯器](../../xdm/schema/composition.md#identity). 若要進一步瞭解名稱空間和身分，請造訪 [Identity Service名稱空間](../../identity-service/namespaces.md) 說明檔案。

## 對應媒體頻道和行銷活動欄位 {#aai-mapping}

<!-- https://www.adobe.com/go/aai-mapping -->

完成選取和新增資料集後， **地圖** 設定步驟隨即顯示。 Attribution AI需要您對應您在上一步中選取的每個資料集的媒體頻道欄位。 這是因為如果沒有資料集之間的媒體管道對應，從Attribution AI衍生的見解可能無法正常顯示，導致見解頁面難以解讀。 雖然只需要媒體頻道，強烈建議您對應部分選用欄位，例如媒體動作、行銷活動名稱、行銷活動群組和行銷活動標籤。 這麼做可讓Attribution AI提供更清楚的深入分析和最佳結果。

![對應](./images/user-guide/mapping-save-&-exit.png)

## 定義事件 {#define-events}

<!-- https://www.adobe.com/go/aai-define-events -->

有三種不同型別的輸入資料用於定義事件：

- **轉換事件：** 可識別行銷活動影響的業務目標，例如電子商務訂單、店內購買和網站造訪。
- **回顧期間：** 提供一個時間範圍，指出應納入轉換事件接觸點前的天數。
- **接觸點：** 收件者、個人和/或Cookie層級的行銷事件，用於評估轉換的數字或收入型影響。

### 定義轉換事件 {#define-conversion-events}

若要定義轉換事件，您必須為事件命名，並從中選擇資料集和欄位來選取事件型別。 **選取資料集和欄位** 下拉式功能表。

![是下拉式清單](./images/user-guide/define-conversion-events.png)

選取事件後，其右側會出現新的下拉式清單。 第二個下拉式清單是用來透過使用作業為您的事件提供進一步內容。 對於此轉換事件，預設作業為 *存在* 已使用。

>[!NOTE]
>
>在底下的字串 *轉換名稱* 會隨著您定義事件而更新。

![無下拉式清單](./images/user-guide/conversion_event_1.png)

接下來，您可以選取合併資料集，此資料集是透過合併上一步驟中的所有輸入資料集產生的。 或者，您也可以根據個別資料集從以下專案選取欄： **選取資料集和欄位** 下拉式功能表。

此 **[!UICONTROL 新增事件]** 和 **[!UICONTROL 新增群組]** 按鈕可用來進一步定義轉換。 根據您定義的轉換，您可能需要使用 **[!UICONTROL 新增事件]** 和 **[!UICONTROL 新增群組]** 按鈕以提供更進一步的上下文。

![新增事件](./images/user-guide/add_event.png)

選取 **[!UICONTROL 新增事件]** 會建立其他欄位，可使用上述相同方法來填寫。 這樣做會將AND陳述式新增到轉換名稱下方的字串定義中。 選取 **x** 以移除已新增的事件。

![新增事件功能表](./images/user-guide/add_event_result.png)

選取 **[!UICONTROL 新增群組]** 會提供在原始欄位以外建立其他欄位的選項。 加入群組後，藍色 *和* 按鈕出現。 選取 **和** 提供變更引數以包含「Or」的選項。 &quot;Or&quot;用於定義多個成功的轉換路徑。 &quot;And&quot;會擴充轉換路徑，加入其他條件。

![使用和或](./images/user-guide/and_or.png)

如果您需要多個轉換，請選取 **新增轉換** 以建立新的轉換卡。 您可以重複上述程式來定義多個轉換。

![新增轉換](./images/user-guide/add_conversion.png)

### 定義回顧期間 {#lookback-window}

定義完轉換後，您必須確認回顧期間。 使用方向鍵或選取預設值(56)，指定您要在轉換事件前多少天加入來自的接觸點。 接觸點會在下一個步驟中定義。

![回顧](./images/user-guide/lookback_window.png)

### 定義接觸點

定義接觸點會遵循類似的工作流程 [定義轉換](#define-conversion-events). 最初，您需要為接觸點命名，並從 *輸入欄位名稱* 下拉式功能表。 選取後，運運算元下拉式清單會出現，其預設值為「exists」。 選取下拉式清單以顯示運運算元清單。

![運運算元](./images/user-guide/operators.png)

針對此接觸點，選取 **等於**.

![步驟1](./images/user-guide/touchpoint_step1.png)

選取接觸點的運運算元後， *輸入欄位值* 已可供使用。 的下拉式清單值 *輸入欄位值* 根據您先前選取的運運算元和接觸點值填入。 如果下拉式清單中未填入值，您可以手動在中鍵入該值。 選取下拉式清單並選取 **按一下**.

>[!NOTE]
>
>運運算元「存在」和「不存在」沒有關聯的欄位值。

![接觸點下拉式清單](./images/user-guide/touchpoint_dropdown.png)

此 **新增事件** 和 **新增群組** 按鈕可用來進一步定義您的接觸點。 由於接觸點周圍的性質複雜，單一接觸點常會有多個事件和群組。

選取時， **新增事件** 允許新增其他欄位。 選取 **x** 以移除已新增的事件。

![新增事件](./images/user-guide/touchpoint_add_event.png)

選取 **新增群組** 可讓您選擇建立與原始欄位不同的其他欄位。 加入群組後，藍色 *和* 按鈕出現。 選取 **和** 若要變更引數，新引數「Or」可用來定義多個成功路徑。 此特定接觸點只有一個成功路徑，因此不需要「或」。

![接觸點概觀](./images/user-guide/add_group_touchpoint.png)

>[!NOTE]
>
>使用下方的字串 *接觸點名稱* 以快速瞭解您的接觸點。 請注意，字串符合接觸點的名稱。

![](./images/user-guide/touchpoint_string.png)

您可以選取「 」，以新增其他接觸點 **新增接觸點** 並重複上述程式。

![新增接觸點](./images/user-guide/add_touchpoint.png)

定義完所有必要的接觸點後，向上捲動並選取 **下一個** 前往最後一個步驟。

![已完成的定義](./images/user-guide/define_event_save_and_exit.png)

## 進階訓練和評分設定

Attribution AI的最後一頁是 **[!UICONTROL 進階]** 用於設定訓練和評分的頁面。

![新頁面集選項](./images/user-guide/advanced_settings_set_options.png)

### 排程訓練

使用 *排程*，您可以選取一週中您希望評分發生的日期和時間。

選取下方的下拉式清單 *評分頻率* 以選取每日、每週和每月評分。 接下來，選取您希望在一週中的哪幾天進行評分。 可以選取多天。 再次選取同一天會取消選取。

![排程訓練](./images/user-guide/schedule_training.png)

若要變更評分發生的當天時間，請選取時鐘圖示。 在出現的新覆蓋圖中，輸入您要評分發生的時間。 選取覆蓋圖外部以將其關閉。

>[!NOTE]
>
>完成每個評分程式最多可能需要24小時的時間。

![時鐘圖示](./images/user-guide/time_of_day.png)

### 其他分數資料集欄（選擇性）

根據預設，系統會針對標準結構描述中的每個服務模型建立分數資料集。 您可以選擇根據轉換事件和接觸點設定，將其他欄新增到評分資料集輸出。 首先，從輸入資料集中選取欄，然後您可以按住滑鼠左鍵在漢堡圖示上以拖放欄來變更順序。

![分數資料集欄新增](./images/user-guide/Add-score-dataset.png)

### 以區域為根據的模型化（選擇性） {#region-based-modeling-optional}

您的客戶行為可能會因國家/地區和地理區域而有很大的差異。 對於全球企業而言，使用以國家/地區或地區為根據的模型可以提高歸因準確性。 每個新增的區域都會使用該區域的資料建立新模型。

若要定義新區域，請從選取 **[!UICONTROL 新增區域]**. 在出現的容器中，提供區域的名稱。 只會從「 」填入一個值(「placeContext.geo.countryCode」) **[!UICONTROL 輸入欄位名稱]** 下拉式清單。 選取此值。

![選擇區域](./images/user-guide/select_region_att.png)

接下來，選取運運算元。

![區域運運算元](./images/user-guide/region_operators.png)

最後，在「 」中輸入國家/地區代碼 **[!UICONTROL 輸入欄位值]** 下拉式清單。

>[!NOTE]
>
>國家/地區代碼長度為兩個字元。 您可以在這裡找到完整清單 [ISO 3166-1 alpha-2](https://datahub.io/core/country-list).

![區域](./images/user-guide/region-based.png)

### 訓練時段 {#training-window}

為確保您獲得儘可能準確的模型，請務必使用代表您企業的歷史資料來訓練您的模型。 根據預設，模型會使用2季（6個月）的轉換事件資料進行訓練。 選取下拉式清單以變更預設值。 您可以選擇使用一至四個季度的資料（3-12個月）進行訓練。

>[!NOTE]
>
>較短的訓練時段對最近的趨勢比較敏感，而較長的訓練時段可建立較穩固的模型，而且對最近的趨勢比較不敏感。

![訓練時段](./images/user-guide/training_window.png)

選取訓練視窗後，請選取 **[!UICONTROL 完成]** 右上角。 留出一些時間處理資料。 完成後，會顯示彈出視窗對話方塊，確認執行個體設定完成。 選取 **[!UICONTROL 確定]** 重新導向至 **[!UICONTROL 服務例項]** 您可以在此頁面檢視您的服務執行個體。

![設定完成](./images/user-guide/instance_setup_complete.png)

## 后续步骤

依照本教學課程，您已成功建立Attribution AI的服務執行個體。 執行個體完成評分後（最多允許24小時），您就可以 [探索Attribution AI深入分析](./discover-insights.md). 此外，如果您想下載評分結果，請造訪 [下載分數](./download-scores.md) 說明檔案。

## 其他资源

以下影片概述在Attribution AI中建立新執行個體的端對端工作流程。

>[!VIDEO](https://video.tv.adobe.com/v/32668?learn=on&quality=12)

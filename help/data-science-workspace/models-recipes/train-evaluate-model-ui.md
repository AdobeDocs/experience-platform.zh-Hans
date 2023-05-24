---
keywords: Experience Platform；訓練與評估；資料科學工作區；熱門主題；建立模型；建立訓練回合
solution: Experience Platform
title: 在Data Science Workspace UI中訓練和評估模型
type: Tutorial
description: 在Adobe Experience Platform Data Science Workspace中，機器學習模型是透過結合適合模型意圖的現有配方來建立。 然後訓練並評估模型，藉由微調其相關的Hyperparameters來最佳化其操作效率和功效。 配方可重複使用，這表示您可以透過單一配方建立多個模型，並針對特定目的量身打造。
exl-id: 6f674cfa-c123-46a3-80e2-9342fe687976
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 2%

---

# 在Data Science Workspace UI中訓練和評估模型

在Adobe Experience Platform Data Science Workspace中，機器學習模型是透過結合適合模型意圖的現有配方來建立。 然後訓練並評估模型，藉由微調其相關的Hyperparameters來最佳化其操作效率和功效。 配方可重複使用，這表示您可以透過單一配方建立多個模型，並針對特定目的量身打造。

本教學課程將逐步解說建立、訓練及評估模型的步驟。

## 快速入门

若要完成本教學課程，您必須擁有 [!DNL Experience Platform]. 如果您無權存取中的組織 [!DNL Experience Platform]，請在繼續之前聯絡您的系統管理員。

本教學課程需要現有配方。 如果您沒有配方，請遵循以下步驟 [在UI中匯入封裝的配方](./import-packaged-recipe-ui.md) 繼續之前，請先參閱教學課程。

## 创建模型

在Experience Platform中，選取 **[!UICONTROL 模型]** 標籤，然後選取瀏覽標籤以檢視現有模型。 選取 **[!UICONTROL 建立模型]** 在頁面右上角附近，開始建立模型的程式。

![](../images/models-recipes/train-evaluate-ui/models_browse.png)

瀏覽現有配方清單，尋找並選取要用來建立模型的配方，然後選取 **[!UICONTROL 下一個]**.
![](../images/models-recipes/train-evaluate-ui/select_recipe.png)

選取適當的輸入資料集，然後選取 **[!UICONTROL 下一個]**. 這會設定模型的預設輸入訓練資料集。
![](../images/models-recipes/train-evaluate-ui/select_dataset.png)

提供模型的名稱並檢閱預設模型組態。 在配方建立期間套用預設組態，按兩下值以檢閱和修改組態值。

若要提供一組新的設定，請選取 **[!UICONTROL 上傳新設定]** 並將包含模型設定的JSON檔案拖曳至瀏覽器視窗。 選取 **[!UICONTROL 完成]** 以建立模型。

>[!NOTE]
>
>設定是唯一的，且特定於其預期配方，這表示零售銷售配方的設定不適用於產品Recommendations配方。 請參閱 [參考資料](#reference) 區段，以取得零售銷售配方設定清單。

![](../images/models-recipes/train-evaluate-ui/name_and_configure.png)

## 建立訓練回合

在Experience Platform中，選取 **[!UICONTROL 模型]** 標籤，然後選取瀏覽標籤以檢視現有模型。 尋找並選取附加至您要訓練之模型名稱的超連結。

![](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

列出所有現有訓練回合及其目前的訓練狀態。 對於使用建立的模型 [!DNL Data Science Workspace] 會使用預設設定和輸入訓練資料集，自動產生並執行訓練回合。

選取以下專案以建立新的訓練回合 **[!UICONTROL 訓練]** 靠近模型概觀頁面的右上角。

![](../images/models-recipes/train-evaluate-ui/model_overview.png)

選取訓練回合的訓練輸入資料集，然後選取 **[!UICONTROL 下一個]**.

![](../images/models-recipes/train-evaluate-ui/training_input.png)

模型建立期間提供的預設組態會顯示，按兩下值可相應地變更和修改這些組態。 選取 **[!UICONTROL 完成]** 以建立並執行訓練回合。

>[!NOTE]
>
>設定是唯一的，且特定於其預期配方，這表示零售銷售配方的設定不適用於產品Recommendations配方。 請參閱 [參考資料](#reference) 區段，以取得零售銷售配方設定清單。

![](../images/models-recipes/train-evaluate-ui/training_configuration.png)


## 評估模型

在Experience Platform中，選取 **[!UICONTROL 模型]** 標籤，然後選取瀏覽標籤以檢視現有模型。 尋找並選取附加至要評估之模型名稱的超連結。

![選取模型](../images/models-recipes/train-evaluate-ui/model-hyperlink.png)

列出所有現有訓練回合及其目前的訓練狀態。 使用多個已完成的訓練回合時，可在模型評估圖表中比較不同訓練回合中的評估量度。 使用圖表上方的下拉式清單選取評估量度。

平均絕對百分比誤差(MAPE)量度會以誤差百分比來表示精確度。 這可用來識別表現最佳的實驗。 MAPE越低越好。

![訓練回合概觀](../images/models-recipes/train-evaluate-ui/complete_training_run.png)

「精確度」量度說明相關執行個體佔總數的百分比 *已擷取* 執行個體。 精確度可視為隨機選取的結果正確的可能性。

![執行多個回合](../images/models-recipes/train-evaluate-ui/multiple_training_runs.png)

選取特定訓練回合會透過開啟評估頁面來提供該回合的詳細資料。 這可以在執行完成之前完成。 在評估頁面上，您可以檢視訓練回合專用的其他評估量度、設定引數和視覺效果。

![預覽記錄](../images/models-recipes/train-evaluate-ui/evaluate_training.png)

您也可以下載活動記錄檔以檢視執行的詳細資訊。 記錄檔對於失敗的執行特別有用，以檢視哪裡出了問題。

![活動記錄](../images/models-recipes/train-evaluate-ui/activity_logs.png)

無法訓練Hyperparameters，且必須透過測試不同的Hyperparameters組合來最佳化Model。 重複此模型訓練和評估程式，直到您到達最佳化模型為止。

## 后续步骤

本教學課程會逐步引導您建立、訓練和評估中的模型 [!DNL Data Science Workspace]. 到達最佳化模型後，您可以使用經過訓練的模型透過以下步驟產生見解 [在UI中為模型評分](./score-model-ui.md) 教學課程。

## 参考 {#reference}

### 零售配方設定

超引數會決定模型的訓練行為，修改Hyperparameters將會影響模型的精確度和精確度：

| 超引數 | 描述 | 建議的範圍 |
| --- | --- | --- |
| learning_rate | 學習率會藉由learning_rate縮減每個樹狀結構的貢獻。 learning_rate和n_estimators之間存在取捨。 | 0.1 |
| n_estimators | 要執行的提升階段數目。 漸層提升對於過擬合相當穩健，因此大量數字通常會產生較佳的效能。 | 100 |
| max_depth | 個別回歸估計值的最大深度。 最大深度會限制樹狀結構中的節點數目。 調整此引數以獲得最佳效能；最佳值取決於輸入變數的互動。 | 3 |

其他引數會決定模型的技術屬性：

| 引數索引鍵 | 类型 | 描述 |
| ----- | ----- | ----- |
| `ACP_DSW_INPUT_FEATURES` | 字符串 | 以逗號分隔的輸入結構描述屬性清單。 |
| `ACP_DSW_TARGET_FEATURES` | 字符串 | 逗號分隔的輸出結構描述屬性清單。 |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | 布尔值 | 決定輸入和輸出特徵是否可修改 |
| `tenantId` | 字符串 | 此ID可確保您建立的資源能正確建立名稱空間，並包含在您的組織內。 [請依照這裡的步驟操作](../../xdm/api/getting-started.md#know-your-tenant_id) 以尋找您的租使用者ID。 |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | 字符串 | 用於訓練模型的輸入結構描述。 |
| `evaluation.labelColumn` | 字符串 | 評估視覺效果的欄標籤。 |
| `evaluation.metrics` | 字符串 | 用於評估模型的評估量度清單（以逗號分隔）。 |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | 字符串 | 用於對模型評分的輸出結構描述。 |

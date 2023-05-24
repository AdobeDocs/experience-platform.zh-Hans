---
keywords: Experience Platform；為模型評分；資料科學工作區；熱門主題；ui；評分回合；評分結果
solution: Experience Platform
title: 在Data Science Workspace UI中為模型評分
type: Tutorial
description: Adobe Experience Platform Data Science Workspace中的評分可藉由將輸入資料饋送至現有的已訓練模型來達成。 評分結果會儲存於指定的輸出資料集，並可作為新批次檢視。
exl-id: 00d6a872-d71a-47f4-8625-92621d4eed56
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# 在Data Science Workspace UI中為模型評分

Adobe Experience Platform中的評分 [!DNL Data Science Workspace] 可將輸入資料饋送至現有的已訓練模型。 評分結果會儲存於指定的輸出資料集，並可作為新批次檢視。

本教學課程示範在中為模型評分所需的步驟。 [!DNL Data Science Workspace] 使用者介面。

## 快速入门

若要完成本教學課程，您必須擁有 [!DNL Experience Platform]. 如果您無權存取中的組織 [!DNL Experience Platform]，請在繼續之前聯絡您的系統管理員。

本教學課程需要經過訓練的模型。 如果您沒有經過訓練的模型，請遵循 [在UI中訓練及評估模型](./train-evaluate-model-ui.md) 繼續之前，請先參閱教學課程。

## 建立新的評分回合

評分回合是使用先前完成並評估的訓練回合中的最佳化設定來建立。 模型的最佳設定集通常由檢閱訓練回合評估量度來決定。

尋找最佳訓練回合，以使用其設定進行評分。 然後，選取附加至其名稱的超連結，以開啟所需的訓練回合。

![選取訓練回合](../images/models-recipes/score/select-run.png)

從訓練回合 **[!UICONTROL 評估]** 索引標籤，選取 **[!UICONTROL 分數]** 位於熒幕右上方。 新的評分工作流程隨即開始。

![](../images/models-recipes/score/training_run_overview.png)

選取輸入評分資料集，然後選取 **[!UICONTROL 下一個]**.

![](../images/models-recipes/score/scoring_input.png)

選取輸出評分資料集，這是儲存評分結果的專用輸出資料集。 確認您的選取範圍並選取 **[!UICONTROL 下一個]**.

![](../images/models-recipes/score/scoring_results.png)

工作流程的最後一步會提示您設定評分回合。 模型會將這些設定用於評分回合。
請注意，您無法移除在建立模型期間設定的繼承引數。 您可以編輯或還原非繼承的引數，方法是按兩下值，或在將游標停留在專案上時選取還原圖示。

![設定](../images/models-recipes/score/configuration.png)

檢閱並確認評分設定，然後選取 **[!UICONTROL 完成]**  以建立並執行評分回合。 系統會將您導向至 **[!UICONTROL 評分回合]** 索引標籤和新的評分回合 **[!UICONTROL 擱置中]** 狀態會顯示。

![評分回合索引標籤](../images/models-recipes/score/scoring_runs_tab.png)

評分回合可以以下列其中一種狀態顯示：
- 擱置中
- 完成
- 失败
- 執行中

狀態會自動更新。 如果狀態為「 」，請繼續進行下一個步驟 **[!UICONTROL 完成]** 或 **[!UICONTROL 已失敗]**.

## 檢視評分結果

若要檢視評分結果，請從選取訓練回合開始。

![選取訓練回合](../images/models-recipes/score/select-run.png)

系統會將您重新導向至訓練回合 **[!UICONTROL 評估]** 頁面。 在訓練回合評估頁面頂端附近，選取 **[!UICONTROL 評分回合]** 索引標籤以檢視現有評分回合的清單。

![評估頁面](../images/models-recipes/score/view_scoring_runs.png)

接著，選取評分回合以檢視回合詳細資料。

![執行詳細資料](../images/models-recipes/score/view_details.png)

如果選取的評分回合具有「完成」或「失敗」狀態，則 **[!UICONTROL 檢視活動記錄]** 連結已可供使用。 如果評分回合失敗，執行記錄可提供有用的資訊來判斷失敗的原因。 若要下載執行記錄，請選取「 」 **[!UICONTROL 檢視活動記錄]**.

![選取檢視記錄](../images/models-recipes/score/view_logs.png)

此 **[!UICONTROL 檢視活動記錄]** 彈出視窗隨即顯示。 選取URL以自動下載關聯的記錄檔。

![](../images/models-recipes/score/activity_logs.png)

您也可選擇選取「 」，檢視您的評分結果  **[!UICONTROL 預覽評分結果資料庫]**.

![選取預覽結果](../images/models-recipes/score/view_results.png)

提供輸出資料集的預覽。

![預覽結果](../images/models-recipes/score/preview_results.png)

若要取得完整的評分結果，請選取 **[!UICONTROL 評分結果資料集]** 在右側欄中找到連結。

## 后续步骤

本教學課程會逐步引導您完成步驟，使用中經過訓練的模型為資料評分 [!DNL Data Science Workspace]. 請依照上的教學課程進行 [在UI中發佈模型作為服務](./publish-model-service-ui.md) 讓您組織內的使用者透過輕鬆存取機器學習服務來評分資料。

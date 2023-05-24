---
title: 在Real-Time CDP B2B中管理預測性銷售線索和帳戶評分
type: Documentation
description: 本檔案提供在Experience PlatformCDP B2B中管理預測性銷售線索和帳戶評分功能的相關資訊。
exl-id: fe7eb94e-5cf1-46bf-80e5-affe5735c998
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 2%

---

# 在Adobe Real-time Customer Data Platform， B2B版本中管理預測性銷售線索和帳戶評分

>[!NOTE]
>
>只有具有「管理B2B AI」許可權的使用者才能建立、變更和刪除分數目標。

本教學課程將逐步帶您瞭解管理預測性銷售線索和帳戶評分服務之評分目標的步驟。 分數目標可用於個人設定檔或帳戶設定檔

## 建立新分數

若要建立新分數，請選取 **[!UICONTROL 服務]** 在側邊欄中並選取 **[!UICONTROL 建立分數]**.

![plas-new-score](../assets/../b2b-ai-ml-services/assets/plas-create-score.png)

此 **[!UICONTROL 基本資訊]** 畫面隨即顯示，提示您選取設定檔型別、輸入名稱及說明（選擇性）。 完成後，選取 **[!UICONTROL 下一個]**.

![plas-enter-basic-information](../assets/../b2b-ai-ml-services/assets/plas-basic-information.png)

此 **[!UICONTROL 定義您的目標]** 畫面隨即顯示。 選取下拉箭頭，然後從出現的下拉式視窗中選取目標型別。

![plas-select-a-goal](../assets/../b2b-ai-ml-services/assets/plas-define-goal.png)

此 **[!UICONTROL 目標細節]** 對話方塊開啟。 選取下拉箭頭，然後從出現的下拉式視窗中選取目標欄位名稱。

![plas-select-a-goal-field-name](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-name.png)

此 **[!UICONTROL 目標條件]** 選取範圍隨即顯示。 選取下拉箭頭，然後從出現的下拉式視窗中選取條件。

![plas-goal-specifics-condition](../assets/../b2b-ai-ml-services/assets/plas-goal-specidics-condition.png)

此 **[!UICONTROL 目標值]** 欄位隨即顯示。 接下來，設定您的 [!UICONTROL 目標細節]. 選取 [!UICONTROL 輸入欄位值] 並輸入您的目標值。

>[!NOTE]
>
>可以新增多個目標值。

![plas-goal-specifics-field-value](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-value.png)

若要新增其他欄位，請選取 **[!UICONTROL 新增欄位]**.

![plas-goal-specifics-add-event](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-add-event.png)

若要設定預測時間範圍，請選取下拉式箭頭，然後選取您選擇的時間範圍。

![plas-prediction-timeframe](../assets/../b2b-ai-ml-services/assets/plas-prediction-timeframe.png)

選取的合併原則會決定如何選取人員設定檔的欄位值。 使用下拉式箭頭選取您選擇的合併原則，然後選取 **[!UICONTROL 完成]**.

此 **[!UICONTROL 評分設定完成]** 隨即顯示對話方塊，確認已建立新分數。 選取 **[!UICONTROL 確定]**.

![plas-score-complete](../assets/../b2b-ai-ml-services/assets/plas-score-complete.png)

>[!NOTE]
>
>完成每個評分程式最多可能需要24小時的時間。

您會返回 **[!UICONTROL 服務]** 索引標籤，您可在其中檢視在分數清單中建立的新分數。

![plas-score-create](../assets/../b2b-ai-ml-services/assets/plas-score-created.png)

選取分數以檢視詳細資訊和上次執行詳細資訊的其他資訊。

![plas-score-additional-information](../assets/../b2b-ai-ml-services/assets/plas-score-info.png)

如需有關可在上次執行詳細資訊下看到的錯誤碼的詳細資訊，請參閱以下章節： [潛在客戶AI管道錯誤代碼](#leads-ai-pipeline-error-codes) 於本檔案中。

## 編輯分數

若要編輯分數，請從 **[!UICONTROL 服務]** 標籤並選取 **[!UICONTROL 編輯]** 從畫面右側的其他詳細資訊面板。

![plas-edit-score](../assets/../b2b-ai-ml-services/assets/plas-edit-score.png)

此 **[!UICONTROL 編輯例項]** 對話方塊隨即顯示，您可以在其中編輯分數說明。 進行變更並選取 **[!UICONTROL 儲存]**.

![plas-edit-save](../assets/../b2b-ai-ml-services/assets/plas-edit-save.png)

>[!NOTE]
>
>無法變更分數設定，因為這會觸發模型重新訓練和重新評分。 這等同於刪除分數並建立新分數。 若要編輯評分的設定，您必須複製此評分或建立新評分。

您會返回 **[!UICONTROL 服務]** 標籤。 選取分數可在畫面右側的其他詳細資訊面板中檢視更新的說明詳細資訊。

## 原地複製分數

若要複製分數，請從 **[!UICONTROL 服務]** 標籤並選取 **[!UICONTROL 原地複製]** 從畫面右側的其他詳細資訊面板。

![plas-clone-score](../assets/../b2b-ai-ml-services/assets/plas-clone-score.png)

此 **[!UICONTROL 基本資訊]** 畫面隨即顯示。 設定檔型別、名稱和說明是從原始分數複製而來。 修改這些詳細資料並選取 **[!UICONTROL 下一個]**.

![plas-clone-basic-info](../assets/../b2b-ai-ml-services/assets/plas-clone-basic-info.png)

此 **[!UICONTROL 定義您的目標]** 畫面隨即顯示。 完成目標區段，就像建立新分數時一樣，然後選取 **[!UICONTROL 完成]**.

您會返回 **[!UICONTROL 服務]** 索引標籤，您可在其中檢視清單中新複製的分數。

>[!NOTE]
>
>此 **[!UICONTROL 定義您的目標]** 區段並非複製自原始分數。

## 刪除分數

若要刪除分數，請從 **[!UICONTROL 服務]** 標籤並選取 **[!UICONTROL 刪除]** 從畫面右側的其他詳細資訊面板。

![plas-delete-score](../assets/../b2b-ai-ml-services/assets/plas-delete-score.png)

此 **[!UICONTROL 刪除檔案]** 確認對話方塊隨即顯示。 选择&#x200B;**[!UICONTROL 删除]**。

![plas-delete-score-confirmation](../assets/../b2b-ai-ml-services/assets/plas-delete-score-confirmation.png)

>[!NOTE]
>
>刪除分數定義也會刪除個人設定檔或帳戶設定檔上的所有預測分數，但不會刪除為分數定義建立的欄位群組。 欄位群組在資料模型中會保持「孤立」。

您會返回 **[!UICONTROL 服務]** 索引標籤中無法再看到清單中的分數。

## 潛在客戶AI管道錯誤代碼

| 错误代码 | 错误消息 |
| --- | --- |
| 401 | 錯誤401。 銷售機會AI管道已停止：帳戶評分的有效帳戶不足。 帳戶計數： {}。 |
| 402 | 錯誤402。 銷售機會AI管道已停止：沒有足夠的有效聯絡人進行聯絡人評分。 連絡人計數： {}。 |
| 403 | 錯誤403。 潛在客戶AI管道已停止：活動量不足以進行模型訓練。 事件計數： {}。 |
| 404 | 錯誤404。 潛在客戶AI管道已停止：模型訓練的轉換不足。 轉換次數： {}。 |
| 405 | 錯誤405。 潛在客戶AI管道已停止：活動太稀疏，無法用於有效的模型訓練。 只有{}%的帳戶有活動。 |
| 406 | 錯誤406。 潛在客戶AI管道已停止：活動太稀疏，無法用於有效的模型訓練。 只有{}%的連絡人有活動。 |
| 407 | 錯誤407。 銷售機會AI管道已停止：評分資料活動型別與訓練資料不符。 |
| 408 | 錯誤408。 銷售機會AI管道已停止：活動功能的遺漏率太高。 遺漏率： {}。 |
| 409 | 錯誤409。 潛在客戶AI管道已停止：測試auc太低。 測試auc： {}。 |
| 410 | 錯誤410。 Leads AI管道已停止：引數調整後測試auc過低。 測試auc： {}。 |
| 411 | 錯誤411。 Leads AI管道已停止：訓練資料沒有足夠的轉換來產生可靠的模型。 转化: {}. |
| 412 | 錯誤412。 潛在客戶AI管道已停止：測試資料沒有任何可計算AUC-ROC的轉換。 |

| 警告/資訊代碼 | 消息 |
| --- | --- |
| 100 | 資訊100。 銷售機會AI品質檢查：帳戶數為： {}。 |
| 101 | 資訊101。 銷售機會AI品質檢查：聯絡人數目是： {}。 |
| 102 | 資訊102。 銷售機會AI品質檢查：機會數為： {}。 |
| 103 | 資訊103。 潛在客戶AI品質檢查：測試auc為低。 開始引數調整。 正在測試auc： {}。 |
| 200 | 警告200。 銷售機會AI品質檢查：第一影像功能的遺漏率為： {}。 |
| 201 | 警告201。 銷售機會AI品質檢查：活動功能的遺漏率為： {}。 |

## 后续步骤

依照此教學課程，您現在可以成功建立和管理分數。 如需更多詳細資訊，請參閱下列檔案：

* [預測性銷售線索和帳戶評分](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
* [監控預測性銷售線索和帳戶評分工作](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)

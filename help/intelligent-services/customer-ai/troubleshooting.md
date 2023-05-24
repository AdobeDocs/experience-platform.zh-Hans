---
keywords: Experience Platform；快速入門；customer ai；熱門主題；customer ai輸入；customer ai輸出；customer ai疑難排解；customer ai錯誤
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Customer AI錯誤疑難排解
description: 尋找Customer AI中常見錯誤的解答。
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: 3bc750b5e1cf47cbca6b037d099936c80c926cf8
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Customer AI錯誤疑難排解

當模型訓練、評分和設定失敗時，Customer AI會顯示錯誤。 在 **[!UICONTROL 服務例項]** 區段，欄用於 **[!UICONTROL 上次執行狀態]** 顯示下列其中一則訊息： **[!UICONTROL 成功]**， **[!UICONTROL 訓練問題]**、和 **[!UICONTROL 已失敗]**.

![上次執行狀態](./images/errors/last-run-status.png)

在 **[!UICONTROL 已失敗]** 或 **[!UICONTROL 訓練問題]** 顯示，您可以選取「執行」狀態以開啟側面板。 側面板包含 **[!UICONTROL 上次執行狀態]** 和 **[!UICONTROL 上次執行詳細資料]**. **[!UICONTROL 上次執行詳細資料]** 包含執行失敗原因的資訊。 如果Customer AI無法提供有關您錯誤的詳細資訊，請聯絡支援人員並提供錯誤代碼。

<img src="./images/errors/last-run-details.png" width="300" /><br />

## 無法無痕存取Chrome中的Customer AI

由於Google Chrome無痕模式安全性設定有所更新，導致Google Chrome無痕模式中發生載入錯誤。 這個問題正在積極與Chrome合作，使experience.adobe.com成為受信任的網域。

<img src="./images/errors/error.PNG" width="500" /><br />

### 建議的修正

若要解決此問題，您需要將experience.adobe.com新增為可隨時使用Cookie的網站。 首先，請瀏覽至 **chrome://settings/cookies**. 接下來，向下捲動至 **自訂行為** 區段，然後選取 **新增** 按鈕（在「可隨時使用Cookie的網站」旁）。 在出現的彈出視窗中，複製並貼上 `[*.]experience.adobe.com` 然後選取 **包含第三方Cookie** 「在此網站上」核取方塊。 完成後，選取 **新增** 和重新載入無痕的Customer AI。

![建議的修正](./images/errors/cookies2.gif)

## 模型品質不佳

如果您收到錯誤&quot;[!UICONTROL 模型品質不佳。 建議您使用修改後的設定來建立新的應用程式]「。 請依照下列建議步驟協助進行疑難排解。

<img src="./images/errors/model-quality.png" width="300" /><br />

### 建議的修正

「模型品質不良」表示模型精度不在可接受的範圍內。 Customer AI在訓練後無法建立可靠的模型且AUC （ROC曲線下的區域）&lt; 0.65。 若要修正錯誤，建議您變更其中一個設定引數並重新執行訓練。

首先檢查資料的準確性。 您的資料包含預測結果所需的必要欄位非常重要。

- 檢查您的資料集是否有最新日期。 Customer AI一律假設資料在模型觸發時為最新。
- 檢查您所定義的預測與適用性視窗中是否有遺漏的資料。 您的資料必須完整無缺。 此外，請確認您的資料集符合 [Customer AI歷史資料需求](./data-requirements.md#data-requirements).
- 在您的結構描述欄位屬性中，檢查商務、應用程式、網頁和搜尋中是否有缺少的資料。

如果您的資料似乎不是問題，請嘗試變更適用人口條件，將模型限製為特定設定檔(例如， `_experience.analytics.customDimensions.eVars.eVar142` 在過去56天內存在)。 這會限制訓練時段中使用的資料母體及大小。

如果限制適用人口無效或無法進行，請變更您的預測期間。

- 請嘗試將預測時段變更為7天，並檢視錯誤是否持續發生。 如果錯誤不再發生，則表示您可能沒有足夠的資料可供定義的預測時段使用。

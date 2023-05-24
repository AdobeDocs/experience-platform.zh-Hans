---
keywords: Experience Platform；開發人員指南；Data Science Workspace；熱門主題；即時機器學習；
solution: Experience Platform
title: Real-time Machine Learning概述
description: 即時機器學習可大幅提升數位體驗內容對使用者的相關性。 在Experience Edge上運用即時參考和持續學習，便可做到這一點。
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# Real-time Machine Learning概述(Alpha)

>[!IMPORTANT]
>
>即時機器學習尚未開放所有使用者使用。 此功能目前處於Alpha測試階段，仍在測試中。 此檔案可能會有變動。

即時機器學習可大幅提升數位體驗內容對使用者的相關性。 這可透過對進行即時參考和持續學習來達成 [!DNL Experience Edge].

Hub和AEM上無縫計算的組合 [!DNL Edge] 大幅減少傳統上為高度個人化的體驗提供相關且回應式支援的延遲。 因此，即時機器學習以極低的延遲提供推斷以進行同步決策。 範例包括呈現個人化網頁內容或呈現優惠或折扣，以減少流失率並增加網店的轉換率。

## Real-time Machine Learning架構 {#architecture}

下列圖表提供即時機器學習架構的概觀。 目前，Alpha有更簡化的版本。

![alpha arch](../images/rtml/alpha-arch.png)

![簡化的概觀](../images/rtml/end-to-end-arch.png)

## 即時機器學習工作流程

下列工作流程概述建立及使用即時機器學習模型的一般步驟和結果。

### 資料擷取與準備

資料會以下列方式擷取和轉換： [!DNL Experience Data Model] Adobe Experience Platform (XDM)。 此資料用於模型訓練。 若要進一步瞭解XDM，請造訪 [XDM概觀](../../xdm/home.md).

### 创作

從頭開始製作，或在Adobe Experience Platform Jupyter Notebooks中匯入預先訓練的序列化ONNX模型，藉此建立即時機器學習模型。

### 部署

將您的模型部署到 [!DNL Experience Edge] 若要在中建立即時機器學習服務 [!UICONTROL 服務庫] 使用預測API端點。

### 推斷

使用Prediction REST API端點即時產生機器學習深入分析。

### 交付

行銷人員可以使用Adobe Target定義區段和規則，將Real-time Machine Learning分數對應至體驗。 這可讓您品牌的網站訪客即時獲得相同或下一頁超個人化體驗。

## 目前功能

即時機器學習目前採用Alpha版。 隨著更多功能和節點可供使用，以下概述的功能可能會有所變更。

>[!NOTE]
>
> Alpha限制：
> - 目前僅支援基於ONNX的模型。
> - 無法序列化節點中使用的函式。 例如，用於Pandas節點中的lambda函式。
> - 之後有20秒的睡眠 [!DNL Edge] 部署是手動完成的。
> - 若要進行深入學習，您的資料傳送方式必須允許 `df.values` 稱為，它會傳回DL模型可接受的陣列。 這是因為ONNX模型評分節點使用 `df.values` 並傳送輸出以對照模型評分。



### 功能:

|  | Alpha （五月） |
| --- | --- |
| **功能** |  — 使用RTML筆記本範本，編寫、測試和部署自訂機器學習模型。 <br>  — 支援匯入預先訓練的機器學習模型。 <br>  — 即時機器學習SDK。 <br>  — 入門製作節點集。 <br>  — 部署至Adobe Experience Platform中樞。 |
| **可用性** | 北美洲 |
| **製作節點** |  — 熊貓 <br> - ScikitLearn <br> - ONNXNode <br>  — 分割 <br> - ModelUpload <br> - OneHotEncoder |
| **評分執行時間** | ONNX |

## 后续步骤

您可以依照以下說明開始操作 [快速入門](./getting-started.md) 指南。 本指南會逐步引導您設定建立Real-time Machine Learning模型的所有必要先決條件。

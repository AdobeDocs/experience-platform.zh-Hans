---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查詢
solution: Experience Platform
title: 查询服务概述
description: 本檔案概述了Experience Platform中查詢服務的角色。
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# [!DNL Query Service] 概述

Adobe Experience Platform會擷取來自各種來源的資料。 行銷人員面臨的主要挑戰是瞭解這些資料以深入瞭解客戶。 Adobe Experience Platform [!DNL Query Service] 允許您使用標準SQL來查詢資料，以利於 [!DNL Platform]. 使用 [!DNL Query Service]，您可以加入中的任何資料集， [!DNL Data Lake] 並將查詢結果擷取為新資料集，以用於報表、機器學習或內嵌至 [!DNL Real-Time Customer Profile]. 本檔案概述以下角色： [!DNL Query Service] 範圍 [!DNL Experience Platform].

[!DNL Query Service] 讓品牌得以連結線上至離線客戶歷程，並瞭解全頻道歸因。 以下影片說明體驗業務可如何運用 [!DNL Query Service] 解決主要使用案例及運作方式 [!DNL Query Service] 有效。

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## 使用 [!DNL Query Service]

[!DNL Query Service] 提供使用者介面和RESTful API，您可以從中建立SQL查詢以更好地分析資料。 透過使用者介面，您可以撰寫和執行查詢、檢視先前執行的查詢，以及存取由您組織內的使用者儲存的查詢。 使用者介面旨在作為沙箱，用來在您的更廣泛資料集上執行查詢之前先測試查詢。 有關在中使用互動式服務的詳細資訊 [!DNL Platform] 您可在以下網址找到： [查詢服務使用者介面指南](ui/overview.md). RESTful API提供類似的體驗，可讓您以程式設計方式撰寫和執行查詢、排程查詢以供日後使用和重複，以及建立您要撰寫的查詢範本。 有關使用的詳細資訊 [!DNL Query Service] API可在以下網址找到： [Query Service開發人員指南](api/getting-started.md).

## [!DNL Query Service] 和 [!DNL Experience Platform] 服務

[!DNL Query Service] 會互動，並可與多個結合使用 [!DNL Experience Platform] 服務。 為了充分利用 [!DNL Query Service's] 功能，建議您熟悉這些服務及其互動方式 [!DNL Query Service].

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] 使用機器學習和人工智慧，從儲存於中的資料取得深入分析 [!DNL Experience Platform]. [!DNL Data Science Workspace] 可讓資料科學家根據有關客戶及其活動的記錄和時間序列資料來建置配方，促進預測，例如購買傾向和個人可能欣賞和使用的建議選件。 您可以在以下位置使用SQL： [!DNL Data Science Workspace] 透過整合 [!DNL Query Service] 到 [!DNL JupyterLab]，可讓您探索、轉換及分析Adobe Analytics資料。 請閱讀 [!DNL Data Science Workspace] 概觀以取得更多關於 [!DNL Data Science Workspace]，以及 [!DNL Query Service] 整合指南，以瞭解如何進行 [!DNL Data Science Workspace] 會與 [!DNL Query Service].

### [!DNL Segmentation Service]

Adobe Experience Platform [!DNL Segmentation Service] 可讓使用者將其客戶劃分為具有類似特徵的較小群組。 這些區段隨後可進行評估，以便為您的提供更好的分析 [!DNL Real-Time Customer Profile] 資料。 [!DNL Query Service] 可用於透過對此區段資料執行查詢來提供此分析 [!DNL Data Lake]. 請閱讀 [!DNL Segmentation Service] 概述，以瞭解有關細分和 [!DNL Profile Query Language] (PQL)指南，以取得如何分析區段的詳細資訊。

## 用例

[!DNL Query Service] 提供彈性的資料處理方式，用途廣泛。 其中包括，它可減輕行銷人員劃分割槽段的負擔，並有助於產生可操作受眾和有意義的業務見解。 下列使用案例提供更深入的 [!DNL Query Service].

### Adobe Analytics瀏覽放棄

此 [以使用Adobe為中心的瀏覽放棄範例 [!DNL Analytics]](./use-cases/abandoned-browse.md) 建立特定可操作受眾的資料。 [!DNL Query Service] 配合複雜的區段邏輯，以計算各種個人化屬性以供下游使用，或大幅簡化您建立區段的方式。

### Looker BI儀表板

透過Adobe Experience Platform，您可以擷取、儲存、建構和提取所有儲存的資料集，包括行為、CRM和銷售點資料。 使用 [!DNL Experience Platform's Query Service]，您可以查詢這些資料集並回答有關業務的特定問題，然後開始產生具影響力的見解。 以下影片示範使用在商業智慧(BI)工具中建立儀表板的價值 [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## 後續步驟和其他資源

閱讀本檔案後，您將瞭解 [!DNL Query Service] 以及它如何在 [!DNL Experience Platform]. 如需與內各種端點互動的詳細資訊， [!DNL Query Service] API，請閱讀 [Query Service開發人員指南](api/getting-started.md). 如需在中使用互動式服務的詳細資訊 [!DNL Platform]，請閱讀 [查詢服務使用者介面指南](ui/overview.md). 如需連線外部使用者端與的完整清單 [!DNL Query Service]，請閱讀 [查詢服務使用者端總覽](clients/overview.md).

為了更能準備好執行查詢，請觀看以下影片。 此影片分享在查詢編輯器介面、PSQL使用者端、商業智慧(BI)解決方案和HTTP API中執行查詢的秘訣和最佳實務。

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)

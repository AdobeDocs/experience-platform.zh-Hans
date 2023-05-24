---
title: 帳戶設定檔儀表板指南
description: Adobe Experience Platform提供控制面板，讓您檢視有關組織B2B帳戶設定檔的重要資訊。
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 0%

---

# [!UICONTROL 帳戶設定檔] 儀表板

Adobe Experience Platform使用者介面(UI)提供了一個儀表板，您可以通過該儀表板檢視有關您的帳戶設定檔的重要資訊，如每日快照期間所擷取。 本指南概述如何存取及使用 [!UICONTROL 帳戶設定檔] UI中的控制面板，並提供控制面板中所顯示視覺效果的詳細資訊。

如需帳戶設定檔使用者介面中所有功能的概述，請造訪 [帳戶設定檔UI指南](../../rtcdp/accounts/account-profile-ui-guide.md).

## 快速入门

您必須有權使用 [Adobe Real-time Customer Data Platform B2B版本](../../rtcdp/b2b-overview.md) 以存取B2B [!UICONTROL 帳戶設定檔] 儀表板。

## 帳戶設定檔資料

此 [!UICONTROL 帳戶設定檔] dashboard可顯示您的行銷管道的多個來源，以及貴組織目前用來儲存客戶帳戶資訊的各種系統的整合帳戶資訊快照。

快照中的設定檔資料顯示的資料與拍攝快照的特定時間點完全相同。 換言之，快照不是資料的近似或樣本，而且 [!UICONTROL 帳戶設定檔] 儀表板未即時更新。

>[!NOTE]
>
>自建立快照以來對資料所做的任何變更或更新，都不會反映在控制面板中，直到建立下一個快照為止。

## 探索 [!UICONTROL 帳戶設定檔] 儀表板

若要導覽至 [!UICONTROL 帳戶設定檔] 在Platform UI中，選取 **[!UICONTROL 設定檔]** 在 [!UICONTROL 帳戶] ，位於左側導覽面板中。

![左側導覽中具有帳戶設定檔的Platform UI會醒目提示，並顯示「概觀」索引標籤。](../images/account-profiles/account-profiles-dashboard.png)

從 [!UICONTROL 帳戶設定檔] 控制面板，您可以 [瀏覽擷取到您組織的帳戶設定檔](#browse-account-profiles)，或 [使用Widget一目瞭然地檢視您的帳戶設定檔資料](#standard-widgets) 以視覺效果呈現資料的各方面。

## 瀏覽帳戶設定檔 {#browse-account-profiles}

此 [!UICONTROL 瀏覽] 索引標籤可讓您使用來自已連線企業來源的帳戶ID或直接輸入來源詳細資訊，來搜尋及檢視擷取到您組織的唯讀帳戶設定檔。 從這裡，您可以檢視屬於帳戶設定檔的重要資訊，包括其名稱、產業、收入、區段等。

選取 [!UICONTROL 設定檔ID] 結果顯示在 [!UICONTROL 瀏覽] 標籤以開啟 [!UICONTROL 詳細資料] 帳戶設定檔的標籤。

![「帳戶設定檔」瀏覽標籤會顯示結果，並反白顯示「設定檔ID」。](../images/account-profiles/account-profiles-browse-tab.png)

顯示在「 」上的帳戶設定檔資訊 [!UICONTROL 詳細資料] 索引標籤已從多個設定檔片段合併在一起，以形成個別帳戶的單一檢視。 請參閱以下說明檔案： [在Adobe Real-time Customer Data Platform中瀏覽帳戶設定檔](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) 以進一步瞭解Platform UI中的帳戶設定檔檢視功能。

## 此 [!UICONTROL 帳戶設定檔] [!UICONTROL 概觀] {#overview}

此 [!UICONTROL 概觀] tab由widget組成，提供唯讀量度，傳達有關您帳戶設定檔的重要資訊。 選取 **[!UICONTROL 修改儀表板]** 變更 [!UICONTROL 概觀] 移動Widget並調整其大小以定位。

![反白顯示「修改儀表板」的「帳戶設定檔」概述標籤。](../images/account-profiles/modify-dashboard.png)

請參考以下檔案： [修改儀表板](../customize/modify.md) 和 [Widget程式庫概觀](../customize/widget-library.md) 以深入瞭解。

## 標準Widget {#standard-widgets}

Adobe提供標準的Widget，您可用來視覺化與帳戶設定檔相關的各種量度。

若要進一步瞭解每個可用的標準Widget，請從下列清單中選取Widget的名稱：

* [依產業區分的帳戶總數](#total-accounts-by-industry)
* [帳戶設定檔已新增](#account-profiles-added)
* [預測性評分分佈](#predictive-scoring-distribution)
* [預測性評分主要影響因素](#predictive-scoring-top-influential-factors)

### 依產業區分的帳戶總數 {#total-accounts-by-industry}

此Widget會顯示單一量度中的帳戶總數，並使用環圈圖來說明組成整體數字之產業中的比例計數大小。 索引鍵為組成環圈圖的不同產業提供色彩編碼資訊。

當游標暫留在環圈圖的個別區段上時，不同產業的個別計數會顯示在對話方塊中。

![依產業Widget區分的帳戶總數。](../images/account-profiles/total-accounts-by-industry-widget.png)

### 帳戶設定檔已新增 {#account-profiles-added}

此Widget使用顏色編碼的長條圖，說明在指定時間內新增到帳戶的設定檔計數，以及構成這些新增設定檔的不同行業比例。 各產業皆採用色彩編碼，而索引鍵則提供橫條圖中各產業所使用的色彩編碼資訊。 從Widget下拉式選單中選取分析期間。 長條圖可以在30天、90天和12個月期間進行視覺化。

>[!NOTE]
>
>由於設定檔只會新增至帳戶且永遠不會移除，因此在一段時間內新增的設定檔數量可能最低為零。

![帳戶設定檔已新增Widget。](../images/account-profiles/accounts-profiles-added-widget.png)

### 預測性評分分佈 {#predictive-scoring-distribution}

此 [!UICONTROL 預測性評分分佈] widget會顯示所有帳戶設定檔的分數分佈，協助您一眼瞭解銷售管道的狀況。 評分資料會透過環形圖和直條圖傳送。

環圈圖可說明您的總帳戶設定檔在高、中及低購買值區傾向中的比例。 索引鍵針對以顏色標示的區段提供詳細資訊，包括評分貯體範圍和該範圍內的帳戶設定檔數量。

柱狀圖提供更細微的評分劃分。 每欄顯示20個五點增量貯體中每個貯體中的帳戶設定檔數。

Widget中的下拉式選單可讓您選取帳戶評分模型。

![預測性評分分佈Widget。](../images/account-profiles/predictive-scoring-distribution.png)

### 預測性評分主要影響因素 {#predictive-scoring-top-influential-factors}

此 [!UICONTROL 預測性評分主要影響因素] widget可協助您瞭解驅動每個傾向性貯體分數的最重要因素。

此Widget會顯示每個高、中和低傾向值區的主要影響因素。 每個影響因子的橫條會指出該傾向性貯體中包含特定影響因子的帳戶設定檔百分比。

Widget中的下拉式選單可讓您選取帳戶評分模型。

![預測性評分主要影響因素Widget。](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## 后续步骤

依照本檔案操作，您現在應該知道如何找到 [!UICONTROL 帳戶設定檔] 儀表板。 您也應該瞭解可用介面工具列中顯示的量度。 若要進一步瞭解如何在Experience PlatformUI中使用帳戶設定檔，請參閱 [帳戶設定檔概述](../../rtcdp/accounts/account-profile-overview.md) 適用於Adobe Real-Time CDP， B2B版本。

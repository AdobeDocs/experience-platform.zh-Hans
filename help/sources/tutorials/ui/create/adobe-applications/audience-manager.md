---
keywords: Experience Platform；首頁；熱門主題；Audience Manager來源聯結器；Audience Manager；Audience Manager聯結器
title: 在使用者介面中建立Adobe Audience Manager來源連線
description: 本教學課程將逐步帶您瞭解如何建立Adobe Audience Manager的來源連線，以使用使用者介面將消費者體驗事件資料匯入Platform。
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# 在使用者介面中建立Adobe Audience Manager來源連線

本教學課程將逐步帶您瞭解如何建立Adobe Audience Manager的來源聯結器，以便使用使用者介面將消費者體驗事件資料匯入Platform。

## 建立與Adobe Audience Manager的來源連線

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列來尋找您要使用的特定來源。

下 [!UICONTROL Adobe應用程式]，選取 **[!UICONTROL Adobe Audience Manager]** 然後選取 **[!UICONTROL 設定]**.

![目錄](../../../../images/tutorials/create/aam/catalog.png)

### 選取特徵和區段

>[!NOTE]
>
>您無法從Audience Manager來源將地區資料擷取至Experience Platform。 如果您的Analytics使用案例需要地區資料，請使用 [Analytics來源聯結器](../adobe-applications/analytics.md).

此 [!UICONTROL 選取特徵和區段] 步驟隨即顯示，提供互動式介面，讓您探索及選取特徵、區段和資料。

* 介面的左側面板包含 [!UICONTROL 選取特徵和區段] 選項以及所有可用區段的階層式目錄。
* 介面的右半部分可讓您與選取的區段互動，並挑選您要使用的特定資料。

![add-data](../../../../images/tutorials/create/aam/add-data.png)

若要瀏覽可用區段，請從以下位置選取您要存取的資料夾： [!UICONTROL 所有區段] 面板。 選取資料夾可讓您周游資料夾的階層，並提供您要篩選的區段清單。

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

識別並選取要使用的區段後，右側會出現新面板，顯示所選專案的清單。 您可以繼續存取不同的資料夾，並為您的連線選取不同的區段。 選取更多區段會更新右側的面板。

![select-data](../../../../images/tutorials/create/aam/select-data.png)

或者，您可以選取 **[!UICONTROL 選取所有區段]** 和 **[!UICONTROL 選取所有特徵]** 方塊。 選取所有區段會將Audience Manager區段帶入Platform，而選取所有特徵則會從Audience Manager中啟用所有第一方特徵。

>[!WARNING]
>
>當您首次使用Audience Manager來源將Audience Manager區段傳送至Platform時，大量的Audience Manager區段母體的擷取會直接影響您的總設定檔計數。 這表示選取所有區段可能會導致「設定檔」計數超過您的授權使用權益。 請檢閱您的 [授權使用量](../../../../../dashboards/guides/license-usage.md) 然後再繼續。

完成後，選取 **[!UICONTROL 下一個]**

![所有區段](../../../../images/tutorials/create/aam/all-segments.png)

此 [!UICONTROL 檢閱] 步驟隨即顯示，可讓您在選取的特徵和區段連線至Platform之前先檢閱這些特徵和區段。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示來源平台和連線狀態。
* **[!UICONTROL 選取的資料]**：顯示選取的區段數和啟用的特徵數。

![檢閱](../../../../images/tutorials/create/aam/review.png)

檢閱資料流後，選取 **[!UICONTROL 完成]** 並留出一些時間來建立資料流。

## 后续步骤

當Audience Manager資料流作用中時，傳入的資料會自動擷取到即時客戶設定檔中。 您現在可以利用這些傳入資料，並使用Platform Segmentation Service建立對象區段。 如需更多詳細資訊，請參閱下列檔案：

* [即時客戶個人檔案總覽](../../../../../profile/home.md)
* [Segmentation Service概述](../../../../../segmentation/home.md)

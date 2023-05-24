---
keywords: Experience Platform；首頁；熱門主題；Adobe Experience Platform；使用手冊；ui指南；平台ui指南；平台簡介；控制面板；
solution: Experience Platform
title: Experience PlatformUI概觀
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1797'
ht-degree: 2%

---

# Adobe Experience Platform UI指南

本指南旨在簡介如何使用Adobe Experience Platform使用者介面(UI)、說明各種元件的用途，並提供進一步檔案的連結以取得詳細資訊。

若要進一步瞭解Adobe Experience Platform，請閱讀 [Experience Platform概觀](home.md).

## 主畫面

登入Adobe Experience Platform後，您便可在 [!UICONTROL 首頁] 頁面，由 [量度控制面板](#metrics)， [最近的資料](#recent-data)、和 [建議的學習](#recommended-learning) 區段。

![](images/user-guide/homepage.png)

### 量度

量度儀表板提供的卡片可向您提供有關資料集、設定檔、區段和組織內目的地的資訊。

![](images/user-guide/homepage-dashboard.png)

此 **[!UICONTROL 資料集]** 區段會顯示貴組織內的資料集數目。 此數字會在建立新資料集時更新。 有關資料集的更多資訊可在以下網址找到： [資料集總覽](../catalog/datasets/overview.md).

此 **[!UICONTROL 設定檔]** 區段顯示貴組織中具有設定檔的總人數，不包括設定檔片段。 此總人數代表可定址對象總數，每24小時會更新一次。 有關設定檔的更多資訊可在以下網址找到： [即時客戶個人檔案總覽](../profile/home.md).

此 **[!UICONTROL 區段]** 區段會顯示貴組織內建立的區段總數。 此數字會在建立新區段時更新。 如需區段的詳細資訊，請參閱 [Segmentation Service概述](../segmentation/home.md).

此 **[!UICONTROL 目的地]** 區段顯示針對組織建立的目的地總數。 此數字會在建立新目的地時更新。 關於目的地的更多資訊可在以下連結中找到： [目的地概觀](../destinations/home.md).

### 最近資料

最近的資料儀表板提供有關最近建立的資料集、來源、區段和目的地的資訊。

![](images/user-guide/homepage-recent.png)

此 **[!UICONTROL 最近的資料集]** 區段會列出貴組織內最近建立的五個資料集。 每次建立新資料集時，此清單都會更新。 您可以從清單中選取資料集，以檢視指定資料集的詳細資訊，或選取 **[!UICONTROL 檢視全部]** 檢視所有已建立資料集的清單。 有關資料集的更多資訊可在以下網址找到： [資料集總覽](../catalog/datasets/overview.md).

此 **[!UICONTROL 最近的來源]** 區段列出貴組織內最近建立的五個來源聯結器。 每次建立新的來源聯結器時，此清單都會更新。 您可以從清單中選取來源連線，以檢視有關指定聯結器的詳細資訊，或選取 **[!UICONTROL 檢視全部]** 檢視所有已建立來源連線的清單。 有關來源的更多資訊可在以下連結中找到： [來源概觀](../sources/home.md).

此 **[!UICONTROL 最近的區段]** 區段列出貴組織內最近建立的五個區段定義。 每次建立新區段定義時，此清單都會更新。 您可以從清單中選取區段定義，以檢視有關指定區段定義的詳細資訊，或選取 **[!UICONTROL 檢視全部]** 以檢視所有已建立區段定義的清單。 如需區段的詳細資訊，請參閱 [Segmentation Service概述](../segmentation/home.md).

此 **[!UICONTROL 最近的目的地]** 區段會列出貴組織內最近建立的五個目的地。 每次建立新目的地時，此清單都會更新。 您可以從清單中選取一個目的地，以檢視有關指定目的地的詳細資訊，或選取 **[!UICONTROL 檢視全部]** 檢視所有已建立目的地的清單。 關於目的地的更多資訊可在以下連結中找到： [目的地概觀](../destinations/home.md).

### 建議的學習

此 **[!UICONTROL 建議的學習]** 區段提供有用檔案的連結，以開始使用Adobe Experience Platform。

![](images/user-guide/homepage-recommended.png)

## 頂端導覽列

Platform UI中的頂端導覽列會顯示您目前登入的組織，並提供數個重要控制項。

導覽列的左側是Adobe Experience Platform標誌。 您隨時都可以選取此標誌，返回Platform UI首頁。

![](./images/user-guide/homepage-top-nav-bar.png)

### 組織切換器

頂端導覽列右側的第一個專案是 **組織切換器**.

![](./images/user-guide/homepage-ims-org-switcher.png)

選取切換器會開啟您有權存取的組織的下拉式選單（如果有的話）。 若要切換至其他組織，請選取列出的選項。

### 切換應用程式

頂部導覽右側的下一個專案為 **應用程式切換器**，由 ![應用程式切換器](./images/user-guide/app-switcher-icon.png) 圖示。 選取此圖示時，您可以在組織有權存取的Adobe應用程式(例如Experience Platform、Analytics、Assets等)之間切換。

### 帮助

應用程式切換器右側是 **說明與支援功能表**，以 ![問號/說明](./images/user-guide/help-icon.png) 圖示。 當您選取此圖示時，會出現一個彈出選單，其中包含數個說明和支援資源。 此 **[!UICONTROL 說明]** 索引標籤會顯示您目前所在頁面的相關檔案清單。 此 **[!UICONTROL 支援]** 索引標籤可讓您與Adobe支援團隊建立支援票證。 此 **[!UICONTROL 意見反應]** 標籤可讓您提交有關Platform的意見回饋給Adobe。

![](images/user-guide/homepage-help-clicked.png)

### 通知和公告

在 **通知區段**，以 ![鈴鐺/通知和公告](images/user-guide/notification-icon.png) 圖示。 此 **[!UICONTROL 通知]** 標籤會顯示產品的重要資訊以及其他相關更新，而 **[!UICONTROL 公告]** 標籤顯示有關服務維護的資訊。

### 用户配置文件

頂端導覽列上的最後一個專案是 **使用者設定**，由 ![使用者設定/使用者設定檔](images/user-guide/profile-icon.png) 圖示。 選取此圖示可編輯您的偏好設定或登出。

您可以使用位於您名稱和電子郵件正下方的開關，在Platform介面的淺色和深色主題之間切換。 選取您偏好的主題。

![](images/theme.png)

### 沙盒

上方導覽列正下方是沙箱列。 此列顯示您目前用於Platform的沙箱。 有關沙箱的更多資訊可在以下網址找到： [沙箱總覽](../sandboxes/home.md).

## 左侧导航栏 {#left-nav}

畫面左側的導覽會列出Platform UI支援的所有不同服務。

按一下功能表圖示以顯示或隱藏左側導覽面板。

![](images/user-guide/hidemenu.png)

您可以在顯示面板後按一下，將導覽鎖定在開啟位置。

>[!IMPORTANT]
>
>左側導覽列僅顯示您可以存取的功能。 在舊版Adobe Experience Platform中，無法使用的專案已停用。 如果您認為您應該具有未出現之區段的存取權，請聯絡您的系統管理員。

![](images/user-guide/homepage-left.png)

此 **[!UICONTROL 首頁]** 區段可讓您返回平台UI首頁。

此 **[!UICONTROL 工作流程]** 區段會顯示在Platform內執行作業的多步驟工作流程清單。 如需工作流程的詳細資訊，請參閱 [工作流程概觀](./workflows.md).

### [!UICONTROL 连接]

此 **[!UICONTROL 來源]** 區段可讓您建立、更新和刪除來源連線，好讓您將資料從外部來源擷取到Platform。 有關來源的更多資訊可在以下連結中找到： [來源概觀](../sources/home.md).

此 **[!UICONTROL 目的地]** 區段可讓您建立、更新和刪除目的地，好讓您將資料從Platform匯出至許多外部目的地。 關於目的地的更多資訊可在以下連結中找到： [目的地概觀](../destinations/home.md).

### [!UICONTROL 客户]

此 **[!UICONTROL 設定檔]** 區段可讓您瀏覽客戶設定檔、檢視設定檔量度、建立和管理合併原則，以及檢視聯合結構描述。 若要進一步瞭解如何使用 [!UICONTROL 設定檔] 區段，請閱讀 [[!DNL Profile] 使用手冊](../profile/ui/user-guide.md). 如需Real-Time Customer Profile的詳細資訊，請參閱 [即時客戶個人檔案總覽](../profile/home.md).

此 **[!UICONTROL 區段]** 區段可讓您建立和管理區段定義。 若要進一步瞭解如何使用 [!UICONTROL 區段] 區段，請閱讀 [分段使用手冊](../segmentation/ui/overview.md). 有關Segmentation Service的詳細資訊，請參閱 [Segmentation Service概述](../segmentation/home.md).

此 **[!UICONTROL 身分]** 區段可讓您建立和管理身分名稱空間。 如需更多有關「 」的資訊， [!UICONTROL 身分] 區段，包含身分識別名稱空間以及如何在Platform UI中使用身分識別的資訊，請參閱 [身分名稱空間總覽](../identity-service/namespaces.md).

### [!UICONTROL Privacy]

此 **[!UICONTROL 原則]** 區段可讓您建立和管理資料使用原則。 若要進一步瞭解如何使用原則區段，請閱讀 [資料使用原則使用手冊](../data-governance/policies/user-guide.md). 有關資料使用原則的更多資訊可在以下連結中找到： [資料使用原則概觀](../data-governance/policies/overview.md).

此 **[!UICONTROL 請求]** 區段可讓您建立和管理隱私權請求。 請注意，您必須列入允許清單才能存取Privacy ServiceUI。 若要進一步瞭解如何使用請求區段，請閱讀 [Privacy Service使用手冊](../privacy-service/ui/user-guide.md). 有關Privacy Service的更多資訊可在以下連結中找到： [Privacy Service概觀](../privacy-service/home.md).

### [!UICONTROL 数据科学]

此 **[!UICONTROL Notebooks]** 區段可讓您存取JupyterLab，這是一個互動式開發環境，可讓您探索、分析和模型化您的資料。 若要進一步瞭解如何使用Notebooks區段，請閱讀 [JupyterLab使用手冊](../data-science-workspace/jupyterlab/overview.md). 有關資料科學工作區的詳細資訊，請參閱 [資料科學工作區概觀](../data-science-workspace/home.md)

此 **[!UICONTROL 模型]** 區段可讓您使用機器學習和人工智慧來建立、開發、訓練及調整模型以做出預測。 有關「模型」區段的更多資訊可在的教學課程中找到： [訓練和評估模型](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

此 **[!UICONTROL 服務]** 區段可讓您管理已發佈的模型，以進行排程的培訓和評分，或使用Adobe的Intelligent Services （一組提供即時、個人化客戶體驗的AI服務）。 有關「服務」區段的詳細資訊，請參閱 [將模型發佈為服務教學課程](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL 数据管理]

此 **[!UICONTROL 結構描述]** 區段可讓您建立和管理Experience Data Model (XDM)結構。 若要進一步瞭解結構描述，請閱讀以下教學課程： [建立結構描述](../xdm/tutorials/create-schema-ui.md). 有關XDM的更多資訊可在以下網址找到： [XDM系統總覽](../xdm/home.md).

此 **[!UICONTROL 資料集]** 區段可讓您建立和管理資料集。 有關資料集的更多資訊可在以下網址找到： [資料集使用手冊](../catalog/datasets/user-guide.md).

此 **[!UICONTROL 查詢]** 區段可讓您建立和管理查詢、記錄Adobe Experience Platform查詢服務所進行的SQL查詢，以及檢視 [!DNL PostgreSQL] 認證。 有關查詢的更多資訊可在以下網址找到： [查詢服務使用手冊](../query-service/ui/overview.md).

此 **[!UICONTROL 監視]** 區段可讓您監視批次和串流擷取。 如需有關監控的詳細資訊，請參閱 [監控資料擷取使用手冊](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL 決策]

Adobe Journey Optimizer是以Experience Platform為基礎建立的應用程式服務。 它可讓您使用強大的決策技術，在適當的時間為所有接觸點的客戶提供最佳優惠和體驗。 若要進一步瞭解Journey Optimizer，包括使用 [!UICONTROL 選件] 和 [!UICONTROL 活動] 造訪 [Journey Optimizer檔案](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=zh-Hans).

### [!UICONTROL 管理]

Platform使用者介面(UI)提供了一個儀表板，您可以透過該儀表板檢視有關您組織的授權使用情況的重要資訊，如每日快照期間所擷取。 選取「 」，存取此儀表板 **[!UICONTROL 授權使用情況]** 在導覽中。 若要進一步瞭解授權使用量儀表板，請造訪 [授權使用儀表板指南](./license-usage-and-guardrails/license-usage-dashboard.md).

>[!IMPORTANT]
>
>授權使用儀表板功能目前為Alpha版，並非所有使用者都可使用。 文档和功能可能会发生变化。

## 后续步骤

閱讀本指南後，您現在已能瞭解首頁和Platform UI的主要導覽元素。 如需在使用者介面中運作的詳細資訊，請參閱每個個別平台服務的檔案。 本檔案的連結提供於 [左側導覽](#left-nav) 區段可在此檔案的先前章節找到。

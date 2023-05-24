---
keywords: 平台；目的地；目的地工作區；工作區；ui；目的地ui；目錄；目的地目錄；
title: 目的地工作區
description: 「目的地」工作區包含五個區段：「概述」、「目錄」、「瀏覽」、「帳戶」和「系統檢視」。 以下各節將予以說明。
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: 69e1f065cb3b302c4b144f39c84179075379f648
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 2%

---

# 目的地工作區 {#destinations-workspace}

在Adobe Experience Platform中選取 **[!UICONTROL 目的地]** 以存取 [!UICONTROL 目的地] 工作區。

此 [!UICONTROL 目的地] 工作區由五個區段組成， [!UICONTROL 概觀]， [!UICONTROL 目錄]， [!UICONTROL 瀏覽]， [!UICONTROL 帳戶]、和 [!UICONTROL 系統檢視]，如下節所述。

![目的地總覽儀表板顯示三個Widget。](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL 概述] {#overview}

此 **[!UICONTROL 概觀]** 標籤顯示 [!UICONTROL 目的地] 控制面板，提供與貴組織目的地資料相關的關鍵量度。 若要進一步瞭解，請造訪 [[!UICONTROL 目的地] 儀表板指南](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>如果您的組織剛開始進行Experience Platform，但尚未具備作用中的目的地，則 [!UICONTROL 目的地] 儀表板和 [!UICONTROL 概觀] 標籤不可見。 請改為選取 [!UICONTROL 目的地] 左側導覽會顯示 [[!UICONTROL 目錄] 標籤](#catalog).

![目的地儀表板概觀標籤。](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalog] {#catalog}

此 **[!UICONTROL 目錄]** 索引標籤會顯示中可用的所有目的地清單 [!DNL Platform]，即可將資料傳送至。

此 [!DNL Platform] 使用者介面在目的地目錄頁面上提供數個搜尋和篩選選項：

* 使用頁面上的搜尋功能來找出特定目的地。
* 使用以下專案篩選目的地 [!UICONTROL 類別] 控制。
* 切換於 [!UICONTROL 所有目的地] 和 [!UICONTROL 我的目的地]. 當您選取 **[!UICONTROL 所有目的地]**，全部可用 [!DNL Platform] 會顯示目的地。 當您選取 **[!UICONTROL 我的目的地]**，您只能看見與其建立連線的目的地。
* 選取以檢視 **[!UICONTROL 連線]** 和/或 **[!UICONTROL 擴充功能]** 型別。 若要瞭解這兩個類別之間的差異，請閱讀 [目的地型別和類別](../destination-types.md).

![目的地目錄，顯示一些廣告和雲端儲存空間目的地。](../assets/ui/workspace/catalog.png)

目的地卡片包含主要和次要控制選項。 主要控制項包括 [!UICONTROL 設定]， [!UICONTROL 啟動]， [!UICONTROL 啟用區段]，或 [!UICONTROL 匯出資料集]. 次要控制項允許檢視選項。 這些控制項說明如下：

| 控制 | 描述 |
|---------|----------|
| [!UICONTROL 設定] | 可讓您建立與目的地的連線。 |
| [!UICONTROL 激活] | 建立與目的地的連線後，您可以啟用區段或匯出資料集到此目的地。 |
| [!UICONTROL 啟用區段] | 建立與目的地的連線後，即可啟用此目的地的區段。 |
| [!UICONTROL 匯出資料集] | 建立與目的地的連線後，您可以將資料集匯出至此目的地。 |
| [!UICONTROL 檢視帳戶] | 檢視您為目的地連線的帳戶。 |
| [!UICONTROL 檢視資料流] | 檢視目的地存在的資料啟用流程。 |
| [!UICONTROL 查看文档] | 開啟該特定目的地的檔案頁面連結，以取得詳細資訊並協助您設定。 |

{style="table-layout:auto"}

![目的地卡上的控制項](../assets/ui/workspace/destination-card-options.png)

在目錄中選取目的地卡以開啟右側邊欄。 在這裡，您可以看到目的地的說明。 右邊欄提供與上表相同的控制項，包括目的地說明，以及目的地類別和型別的指示。

![目的地目錄選項](../assets/ui/workspace/destination-right-rail.png)

如需目的地類別和每個目的地相關資訊的詳細資訊，請參閱 [目的地目錄](../catalog/overview.md) 和 [目的地型別和類別](../destination-types.md).

## [!UICONTROL 帐户] {#accounts}

此 **[!UICONTROL 帳戶]** 索引標籤會顯示您已建立與不同目的地的連線的詳細資訊，並可讓您更新或刪除現有的帳戶詳細資訊。 請參閱下表，瞭解您可以取得每個目的地帳戶的所有資訊。

>[!TIP]
>
> * 選取省略符號(`...`)中 [!UICONTROL Platform] 欄並使用 ![啟用控制項](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL 啟動&#x200B;]**/**[!UICONTROL &#x200B;啟用區段&#x200B;]**/**[!UICONTROL &#x200B;匯出資料集&#x200B;]**控制將區段或資料集匯出至該目的地。
> * 選取省略符號(`...`)中 [!UICONTROL Platform] 欄並使用 ![編輯詳細資訊控制項](../assets/ui/workspace/pencil-icon.png)**[!UICONTROL 編輯詳細資料&#x200B;]**控制對象 [更新](update-accounts.md) 現有目的地帳戶的詳細資料。
> * 選取省略符號(`...`)中 [!UICONTROL Platform] 欄並使用 ![刪除控制項](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL 刪除&#x200B;]**控制對象 [刪除](delete-destination-account.md) 現有的目的地帳戶。


![帳戶標籤](../assets/ui/workspace/destination-account-options.png)

| 元素 | 描述 |
|---|---|
| [!UICONTROL 平台] | 您為其設定連線的目的地。 |
| [!UICONTROL 连接类型] | 代表儲存貯體或目的地的帳戶連線型別。 根據目的地，驗證選項包括： <ul><li>對於電子郵件行銷目的地：可以是S3、FTP或Azure Blob。</li><li>對於即時廣告目的地：伺服器對伺服器</li><li>對於Amazon S3雲端儲存目的地：存取金鑰 </li><li>對於SFTP雲端儲存目標： SFTP的基本驗證</li><li>OAuth 1或OAuth 2驗證</li><li>持有人權杖驗證</li></ul> |
| [!UICONTROL 用户名] | 您在「 」中選擇的使用者名稱 [連線目的地精靈](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL 目标] | 代表與針對目的地建立的基本資訊相連結的不重複成功目的地資料流數目。 |
| [!UICONTROL 已授权] | 授權連線到此目的地的日期。 |

{style="table-layout:auto"}

## [!UICONTROL 浏览] {#browse}

此 **[!UICONTROL 瀏覽]** 索引標籤會顯示您已建立連線的目的地。 具有的目的地 **[!UICONTROL 已啟用/已停用]** 切換功能已開啟，並分別將目的地設定為「作用中」或「非作用中」。 您也可以選取「 」，檢視資料流動的目的地 **[!UICONTROL 區段]** > **[!UICONTROL 瀏覽]** 並選取要檢查的區段。 請參閱下表，瞭解中為每個目的地提供的所有資訊 [!UICONTROL 瀏覽] 標籤：

>[!TIP]
>
> * 選取省略符號(`...`)中 [!UICONTROL 名稱] 欄並使用 ![啟用區段控制項](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL 啟動&#x200B;]**控制將區段或資料集匯出至該目的地。
> * 選取省略符號(`...`)中 [!UICONTROL 名稱] 欄並使用 ![刪除控制項](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL 刪除&#x200B;]**控制對象 [移除](delete-destinations.md) 與目的地的現有連線。
> * 選取省略符號(`...`)中 [!UICONTROL 名稱] 欄並使用 ![在監控控制中檢視](../assets/ui/workspace/monitoring-icon.png)**[!UICONTROL 在監視中檢視&#x200B;]**控制項以檢視此目的地的啟用資訊，在 [監視儀表板](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * 選取省略符號(`...`)中 [!UICONTROL 名稱] 欄並使用 ![訂閱警示 ](../assets/ui/workspace/alerts-icon.png)**[!UICONTROL 訂閱警示&#x200B;]**控制以訂閱目的地資料流警示。 您可以訂閱警示，以接收有關流程執行的狀態、成功或失敗的訊息。 另請參閱 [訂閱內容感知目的地警示](alerts.md) 以取得目的地資料流警示的詳細資訊。


![瀏覽標籤](../assets/ui/workspace/browse-tab.png)

| 元素 | 描述 |
|---------|----------|
| 名称 | 您為此目的地的啟用流程提供的名稱。 同一欄包含兩個控制項： [!UICONTROL 啟動 ] 和 [!UICONTROL 刪除目的地]. |
| [!UICONTROL 上次資料流執行狀態] | 上次資料流執行的狀態。 另請參閱 [檢視目的地詳細資料](destination-details-page.md) 以取得資料流執行的詳細資訊。 |
| [!UICONTROL 上次資料流執行日期] | 上次資料流執行的時間和日期。 另請參閱 [檢視目的地詳細資料](destination-details-page.md) 以取得資料流執行的詳細資訊。 |
| [!UICONTROL 目标] | 您為啟用流程選取的目的地平台。 |
| [!UICONTROL 连接类型] | 代表儲存貯體或目的地的連線型別。 <ul><li>針對電子郵件行銷目的地：可以是S3、FTP或 [!DNL Azure Blob].</li><li>對於即時廣告目的地：伺服器對伺服器。</li><li>對於串流目的地：可以是 [!DNL Azure Event Hubs] 或 [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL 用户名] | 您為目的地流程選取的帳戶認證。 |
| [!UICONTROL 啟用資料] | 表示正在啟用至此目的地的區段數。 選取此控制項可進一步瞭解已啟用的區段。 請參閱 [啟用資料](/help/destinations/ui/destination-details-page.md#activation-data) 「目的地詳細資料」頁面取得已啟動區段的詳細資訊。 |
| [!UICONTROL 已建立] | 至目的地的啟動流程建立日期和UTC時間。 選取向上/向下箭頭符號，依最新先或最舊先排序啟動流程。 |
| [!UICONTROL 状态] | `Enabled` 或 `Disabled`. 指出資料是否正在啟用至此目的地。 |

按一下目的地列，即可在右側邊欄中顯示有關目的地的詳細資訊。

![按一下目的地列](../assets/ui/workspace/click-destination-row.png)

選取目的地名稱，以檢視啟用至此目的地的區段相關資訊。 按一下 **[!UICONTROL 編輯啟動]** 修改或新增至傳送至此目的地的區段。

## [!UICONTROL 系統檢視] {#system-view}

此 **[!UICONTROL 系統檢視]** 索引標籤會以圖形呈現您在Adobe Experience Platform中設定的啟動流程。

![Data-flows1](../assets/ui/workspace/data-flows1.png)

選取頁面上顯示的任何目的地，然後按一下 **[!UICONTROL 檢視資料流]** 檢視您為每個目的地設定的所有連線的相關資訊。

![Data-flows2](../assets/ui/workspace/data-flows2.png)

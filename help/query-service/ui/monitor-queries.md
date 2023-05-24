---
title: 監視排定的查詢
description: 瞭解如何透過查詢服務UI監視查詢。
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: 1b4554e204663d40c3a18da792614305abb7d296
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 0%

---

# 監視排定的查詢

Adobe Experience Platform透過UI改善所有查詢作業的狀態可見性。 從 [!UICONTROL 排定的查詢] 索引標籤您現在可以找到有關查詢執行的重要資訊，包括狀態、排程詳細資訊，以及失敗時的錯誤訊息/代碼。 您還可以透過UI訂閱基於查詢狀態的查詢警報，用於以下任何查詢： [!UICONTROL 排定的查詢] 標籤。

## [!UICONTROL 排定的查詢]

此 [!UICONTROL 排定的查詢] 索引標籤會提供所有已排程CTA和ITAS查詢的概觀。 您可以找到所有已排程查詢的執行詳細資料，以及任何失敗查詢的錯誤代碼和訊息。

若要導覽至 [!UICONTROL 排定的查詢] 索引標籤，選取 **[!UICONTROL 查詢]** 從左側導覽列，後面接著 **[!UICONTROL 排定的查詢]**

![「查詢」工作區中的「排程查詢」索引標籤。](../images/ui/monitor-queries/scheduled-queries.png)

下表說明每個可用的欄。

>[!NOTE]
>
>警示訂閱圖示包含在未命名欄的每一列中。 請參閱 [警報訂閱](#alert-subscription) 區段以取得詳細資訊。

| 栏目 | 描述 |
|---|---|
| **[!UICONTROL 名称]** | 名稱欄位可以是範本名稱或SQL查詢的前幾個字元。 使用查詢編輯器透過UI建立的任何查詢最初都會命名。 如果查詢是透過API建立的，則其名稱會變成用來建立查詢的初始SQL的片段。 從「 」中選取任何專案 [!UICONTROL 名稱] 欄，以檢視與查詢相關聯的所有執行專案清單。 如需詳細資訊，請參閱 [查詢執行排程詳細資料](#query-runs) 區段。 |
| **[!UICONTROL 模板]** | 查詢的範本名稱。 選取範本名稱以導覽至「查詢編輯器」。 為方便起見，查詢範本會顯示在查詢編輯器中。 如果沒有範本名稱，資料列會標示一個連字型大小，且無法重新導向至「查詢編輯器」來檢視查詢。 |
| **[!UICONTROL SQL]** | SQL查詢的片段。 |
| **[!UICONTROL 執行頻率]** | 這是設定查詢執行的步調。 可用的值包括 `Run once` 和 `Scheduled`. 可以根據查詢的執行頻率來篩選查詢。 |
| **[!UICONTROL 创建者]** | 建立查詢的使用者名稱。 |
| **[!UICONTROL 已建立]** | 建立查詢時的時間戳記（UTC格式）。 |
| **[!UICONTROL 上次執行時間戳記]** | 執行查詢時的最新時間戳記。 此欄會根據查詢目前的排程來反白顯示查詢是否已執行。 |
| **[!UICONTROL 上次執行狀態]** | 最近查詢執行的狀態。 狀態值為： `Success`， `Failed`， `In progress`、和 `No runs`. |

>[!TIP]
>
>如果您導覽至「查詢編輯器」，可以選取 **[!UICONTROL 查詢]** 以返回 [!UICONTROL 範本] 標籤。

### 自訂排程查詢的表格設定

您可以調整欄位 [!UICONTROL 排定的查詢] 定位鍵以符合您的需求。 選取設定圖示(![設定圖示。](../images/ui/monitor-queries/settings-icon.png))以開啟 [!UICONTROL 自訂表格] 設定對話方塊並編輯可用的欄。

![自訂表格設定圖示。](../images/ui/monitor-queries/customze-table-settings-icon.png)

切換相關的核取方塊以移除或新增表格欄。 接下來，選取 **[!UICONTROL 套用]** 以確認您的選擇。

>[!NOTE]
>
>透過UI建立的任何查詢都會在建立過程中成為具名範本。 範本名稱顯示在範本欄中。 如果查詢是透過API建立的，則範本欄為空白。

![自訂表格設定對話方塊。](../images/ui/monitor-queries/customize-table-dialog.png)

### 訂閱警示 {#alert-subscription}

您可以訂閱以下專案的警示： [!UICONTROL 排定的查詢] 標籤。 選取警示通知圖示(![警示圖示。](../images/ui/monitor-queries/alerts-icon.png))以開啟 [!UICONTROL 警報] 對話方塊。 此 [!UICONTROL 警報] 對話方塊會訂閱UI通知和電子郵件警示。 警示是根據查詢的狀態。 有三個可用選項： `start`， `success`、和 `failure`. 核取適當的方塊並選取 **[!UICONTROL 儲存]** 以訂閱。

![警示訂閱對話方塊。](../images/ui/monitor-queries/alert-subscription-dialog.png)

請參閱 [警報訂閱API檔案](../api/alert-subscriptions.md) 以取得詳細資訊。

### 篩選查詢 {#filter}

您可以根據執行頻率來篩選查詢。 從 [!UICONTROL 排定的查詢] 索引標籤中，選取篩選圖示(![篩選圖示](../images/ui/monitor-queries/filter-icon.png))以開啟篩選器側欄。

![已排程查詢索引標籤中反白了篩選圖示。](../images/ui/monitor-queries/filter-queries.png)

選取 **[!UICONTROL 已排程]** 或 **[!UICONTROL 執行一次]** 執行頻率篩選核取方塊以篩選查詢清單。

>[!NOTE]
>
>任何已執行但未排程的查詢都符合資格 [!UICONTROL 執行一次].

![反白顯示篩選側欄的已排程查詢索引標籤。](../images/ui/monitor-queries/filter-sidebar.png)

啟用篩選條件後，請選取 **[!UICONTROL 隱藏篩選器]** 以關閉篩選面板。

## 查詢執行排程詳細資料 {#query-runs}

選取查詢名稱，以切換作業選項至排程詳細資訊頁面。 此檢視提供排程查詢中執行的所有執行清單。 提供的資訊包括開始和結束時間、狀態和使用的資料集。

![排程詳細資訊頁面。](../images/ui/monitor-queries/schedule-details.png)

此資訊會以五欄表格提供。 每一列表示查詢執行。

| 列名称 | 描述 |
|---|---|
| **[!UICONTROL 查詢執行ID]** | 每日執行的查詢執行識別碼。 選取 **[!UICONTROL 查詢執行ID]** 導覽至 [!UICONTROL 查詢執行總覽]. |
| **[!UICONTROL 查詢執行開始]** | 執行查詢時的時間戳記。 這是UTC格式。 |
| **[!UICONTROL 查詢執行完成]** | 查詢完成時的時間戳記。 這是UTC格式。 |
| **[!UICONTROL 状态]** | 最近查詢執行的狀態。 三個狀態值包括： `successful` `failed` 或 `in progress`. |
| **[!UICONTROL 数据集]** | 執行中涉及的資料集。 |

欲知正在排程的查詢詳情，請參閱 [!UICONTROL 屬性] 面板。 此面板包含初始查詢ID、使用者端型別、範本名稱、查詢SQL和排程的步調。

![「排程詳細資訊」頁面中會反白顯示屬性面板。](../images/ui/monitor-queries/properties-panel.png)

選取查詢執行ID以切換作業選項至執行詳細資訊頁面並檢視查詢資訊。

![反白顯示執行ID的排程詳細資訊畫面。](../images/ui/monitor-queries/navigate-to-run-details.png)

## 查詢執行總覽 {#query-run-overview}

此 [!UICONTROL 查詢執行總覽] 提供此排程查詢的個別執行的相關資訊，以及執行狀態的更詳細劃分。 此頁面也包含使用者端資訊，以及可能導致查詢失敗的任何錯誤的詳細資訊。

![執行詳細資訊畫面，其中總覽區段反白顯示。](../images/ui/monitor-queries/query-run-details.png)

查詢狀態區段提供查詢失敗時的錯誤碼和錯誤訊息。

![執行詳細資訊畫面中反白了錯誤區段。](../images/ui/monitor-queries/failed-query.png)

您可以從此檢視將查詢SQL複製到剪貼簿。 選取SQL程式碼片段右上角的復製圖示，以複製查詢。 會出現快顯訊息，確認已復製程式碼。

![執行詳細資訊畫面中反白顯示SQL復製圖示。](../images/ui/monitor-queries/copy-sql.png)

### 使用匿名區塊執行查詢的詳細資料 {#anonymous-block-queries}

使用匿名區塊組成其SQL陳述式的查詢會分隔成其個別的子查詢。 這可讓您個別檢查每個查詢區塊的執行詳細資料。

>[!NOTE]
>
>使用DROP命令的匿名區塊的執行詳細資料 **not** 將作為單獨的子查詢報告。 CTAS查詢、ITAS查詢和用作匿名區塊子查詢的COPY陳述式有獨立的執行詳細資訊。 目前不支援DROP命令的執行詳細資料。

匿名區塊是透過使用來表示 `$$` 查詢前的前置詞。 請參閱 [匿名封鎖檔案](../essential-concepts/anonymous-block.md) 以進一步瞭解查詢服務中的匿名區塊。

匿名區塊子查詢的執行狀態左側有標籤。 選取索引標籤以顯示執行詳細資料。

![顯示匿名區塊查詢的查詢執行概觀。 多個查詢標籤會反白顯示。](../images/ui/monitor-queries/anonymous-block-overview.png)

如果匿名區塊查詢失敗，您可以透過此UI找到該特定區塊的錯誤代碼。

![查詢執行概觀會顯示匿名區塊查詢，並反白顯示單一區塊的錯誤代碼。](../images/ui/monitor-queries/anonymous-block-failed-query.png)

選取 **[!UICONTROL 查詢]** 返回「排程詳細資料」畫面，或 **[!UICONTROL 排定的查詢]** 以返回 [!UICONTROL 排定的查詢] 標籤。

![反白顯示「查詢」的執行詳細資訊畫面。](../images/ui/monitor-queries/return-navigation.png)

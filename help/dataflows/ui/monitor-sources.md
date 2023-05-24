---
keywords: Experience Platform；首頁；熱門主題；監控帳戶；監控資料流；資料流；來源
description: 本教學課程提供使用彙總監視檢視和跨服務監視來監視資料流的步驟。
solution: Experience Platform
title: 在UI中監視來源的資料流
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 8%

---

# 在 UI 中监测源的数据流

>[!IMPORTANT]
>
>串流來源，例如 [HTTP API來源](../../sources/connectors/streaming/http.md) 目前不受監視儀表板支援。 目前，您只能使用儀表板來監視批次來源。

在Adobe Experience Platform中，資料會從各種來源擷取、在Experience Platform中分析，並啟用至各種目的地。 Platform藉由提供資料流透明度，讓追蹤這種潛在非線性資料流的程式變得更輕鬆。

監控儀表板可讓您以視覺化方式呈現資料流的歷程。 您可以使用彙總的監控檢視，並從來源層級垂直導覽至資料流，以及資料流執行，讓您檢視對資料流成功或失敗有貢獻的對應量度。 您也可以使用監控儀表板的跨服務監控容量，監控資料流從來源到目的地的歷程。 [!DNL Identity Service]，並至 [!DNL Profile].

本教學課程提供使用彙總監視檢視和跨服務監視來監視資料流的步驟。

## 快速入门 {#getting-started}

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [資料流](../home.md)：資料流可呈現跨平台行動資料的資料作業。 資料流會跨不同服務進行設定，有助於將資料從來源聯結器移至目標資料集，以及 [!DNL Identity] 和 [!DNL Profile]，並至 [!DNL Destinations].
   * [資料流執行](../../sources/notifications.md)：資料流執行是根據所選資料流的頻率設定的週期性排程作業。
* [來源](../../sources/home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [Identity Service](../../identity-service/home.md)：透過跨裝置和系統橋接身分，更能瞭解個別客戶及其行為。
* [即時客戶個人檔案](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [沙箱](../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 聚總監視檢視 {#aggregated-monitoring-view}

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="源提取"
>abstract="源提取视图包含有关数据湖服务中的数据活动状态和量度的信息，包括提取的记录和失败的记录。查看量度定义指南以了解有关量度和图表的更多信息。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="数据流运行详细信息"
>abstract="源处理包含有关数据湖服务中的数据活动状态和量度的信息，包括提取的记录和失败的记录。查看量度定义指南以了解有关量度和图表的更多信息。"
>text="Learn more in documentation"

在 [平台UI](https://platform.adobe.com)，選取 **[!UICONTROL 監視]** 從左側導覽存取 [!UICONTROL 監視] 儀表板。 此 [!UICONTROL 監視] 儀表板包含所有來源資料流的量度和資訊，包括從來源到來源之資料流量的健康情況分析 [!DNL Identity Service]，並至 [!DNL Profile].

圖示板中心是 [!UICONTROL 來源擷取] 面板，其中包含顯示擷取記錄和失敗記錄之資料的量度和圖形。

![monitoring-dashard](../assets/ui/monitor-sources/monitoring-dashboard.png)

依預設，顯示的資料包含過去24小時的擷取率。 選取 **[!UICONTROL 過去24小時]** 以調整記錄顯示的時間範圍。

![變更日期](../assets/ui/monitor-sources/change-date.png)

此時會出現一個日曆快顯視窗，為您提供替代擷取時間範圍的選項。 選取 **[!UICONTROL 過去30天]** 然後選取 **[!UICONTROL 套用]**

![調整時間範圍](../assets/ui/monitor-sources/adjust-timeframe.png)

圖表預設為啟用，您可以停用它們以展開下面的來源清單。 選取 **[!UICONTROL 度量和圖表]** 切換以停用圖形。

![量度與圖表](../assets/ui/monitor-sources/metrics-graphs.png)

| 源提取 | 描述 |
| ---------------- | ----------- |
| [!UICONTROL 已提取的记录 ] | 擷取的記錄總數。 |
| [!UICONTROL 失败的记录] | 因資料錯誤而未擷取的記錄總數。 |
| [!UICONTROL 失敗的資料流總數] | 具有「 」的資料流總數 `failed` 狀態。 |

來源擷取清單會顯示包含至少一個現有帳戶的所有來源。 此清單也包含每個來源的擷取率、失敗記錄數，以及根據您套用之時間範圍的失敗資料流總數的資訊。

![來源擷取](../assets/ui/monitor-sources/source-ingestion.png)

若要排序來源清單，請選取 **[!UICONTROL 我的來源]** 然後從下拉式選單中選取您選擇的類別。 例如，若要聚焦於雲端儲存，請選取  **[!UICONTROL 雲端儲存空間]**

![按類別排序](../assets/ui/monitor-sources/sort-by-category.png)

若要檢視所有來源的所有現有資料流，請選取「 」 **[!UICONTROL 資料流]**.

![view-all-dataflows](../assets/ui/monitor-sources/view-all-dataflows.png)

或者，您可以在搜尋列中輸入來源，以隔離單一來源。 識別來源後，請選取篩選器圖示 ![篩選](../assets/ui/monitor-sources/filter.png) 旁邊，可檢視其作用中資料流的清單。

![搜索](../assets/ui/monitor-sources/search.png)

資料流清單隨即顯示。 若要縮小清單範圍並專注於有錯誤的資料流，請選取「 」 **[!UICONTROL 僅顯示失敗]**.

![僅顯示 — 失敗](../assets/ui/monitor-sources/show-failures-only.png)

找到您要監控的資料流，然後選取篩選圖示 ![篩選](../assets/ui/monitor-sources/filter.png) 旁邊，可檢視其執行狀態的詳細資訊。

![資料流](../assets/ui/monitor-sources/dataflow.png)

資料流執行頁面會顯示資料流執行開始日期、資料大小、狀態及其處理持續時間的資訊。 選取篩選圖示 ![篩選](../assets/ui/monitor-sources/filter.png) 資料流執行開始時間旁邊，可檢視其資料流執行詳細資料。

![資料流 — run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

此 [!UICONTROL 資料流執行詳細資料] 頁面會顯示資料流的中繼資料、部分擷取狀態和錯誤摘要的相關資訊。 錯誤摘要包含特定的頂層錯誤，會顯示擷取程式在哪個步驟遇到錯誤。

向下捲動以檢視有關所發生錯誤的更多具體資訊。

![資料流 — 執行 — 詳細資料](../assets/ui/monitor-sources/dataflow-run-details.png)

此 [!UICONTROL 資料流執行錯誤] 面板會顯示導致資料流擷取失敗的特定錯誤和錯誤代碼。 在此案例中，發生對應程式轉換錯誤，導致24筆記錄失敗。

選取 **[!UICONTROL 檔案]** 以取得詳細資訊。

![資料流 — 執行 — 錯誤](../assets/ui/monitor-sources/dataflow-run-errors.png)

此 [!UICONTROL 檔案] 面板包含檔案名稱和路徑的資訊。

如需更精細的錯誤表示法，請選取 **[!UICONTROL 預覽錯誤診斷]**.

![檔案](../assets/ui/monitor-sources/files.png)

此 [!UICONTROL 錯誤診斷預覽] 視窗隨即顯示，在資料流中顯示最多100個錯誤的預覽。 您可以選取 **[!UICONTROL 下載]** 擷取curl指令，然後可讓您下載錯誤診斷。

完成後，選取 **[!UICONTROL 關閉]**

![錯誤診斷](../assets/ui/monitor-sources/error-diagnostics.png)

您可以使用頂端標題的階層連結系統，導覽回至 [!UICONTROL 監視] 儀表板。 選取 **[!UICONTROL 執行開始：2021年2月14日，晚上9:47]** 以返回上一頁，然後選取 **[!UICONTROL 資料流：忠誠度資料擷取示範 — 失敗]** 以返回「資料流」頁面。

![階層連結](../assets/ui/monitor-sources/breadcrumbs.png)

## 后续步骤 {#next-steps}

依照本教學課程，您已使用成功監視來源層級的擷取資料流 **[!UICONTROL 監視]** 儀表板。 您也已成功識別在擷取程式期間導致資料流失敗的錯誤。 如需更多詳細資訊，請參閱下列檔案：

* [監控資料流中的身分](./monitor-identities.md)
* [在資料流中監視設定檔](./monitor-profiles.md)

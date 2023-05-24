---
keywords: Experience Platform；首頁；熱門主題；監控帳戶；監控資料流；資料流；目的地
description: 目的地可讓您從Adobe Experience Platform向無數的外部合作夥伴啟用資料。 本教學課程提供如何使用Experience Platform使用者介面監控目的地的資料流的指示。
solution: Experience Platform
title: 在UI中監視目的地的資料流
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '3227'
ht-degree: 10%

---

# 在UI中監視目的地的資料流

目的地可讓您從Adobe Experience Platform向無數的外部合作夥伴啟用資料。 Platform透過資料流提供透明度，讓追蹤資料流向目的地的程式變得更輕鬆。

監控儀表板可讓您以視覺化方式呈現資料流的歷程，包括資料啟用的目的地。 本教學課程提供如何直接在目的地工作區中監視資料流或使用「監視」儀表板來使用Experience Platform使用者介面監視目的地的資料流的指示。

## 快速入门 {#getting-started}

本指南需要您實際瞭解下列Adobe Experience Platform元件：

- [資料流](../home.md)：資料流可呈現跨平台行動資料的資料作業。 資料流會跨不同服務進行設定，有助於將資料從來源聯結器移至目標資料集，以及 [!DNL Identity] 和 [!DNL Profile]，並至 [!DNL Destinations].
   - [資料流執行](../../sources/notifications.md)：資料流執行是根據所選資料流的頻率設定的週期性排程作業。
- [目的地](../../destinations/home.md)：目的地是預先建立的與常用應用程式的整合，可讓您順暢地從Platform啟用資料，用於跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例。
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

## 監視目的地工作區中的資料流 {#monitor-dataflows-in-the-destinations-workspace}

在 **[!UICONTROL 目的地]** 在平台UI中，導覽至 **[!UICONTROL 瀏覽]** 標籤並選取您要檢視的目的地名稱。

![選取目的地檢視](../assets/ui/monitor-destinations/select-destination.png)

現有資料流清單隨即顯示。 在此頁面是可檢視資料流的清單，包括有關其目的地、使用者名稱、資料流數量和狀態的資訊。

請參閱下表以取得狀態的詳細資訊：

| 状态 | 描述 |
| ------ | ----------- |
| 已启用 | 此 `Enabled` status表示資料流作用中，且正在根據提供的排程匯出資料。 |
| 已禁用 | 此 `Disabled` status表示資料流為非作用中且未匯出任何資料。 |
| 处理时间 | 此 `Processing` status表示資料流尚未啟用。 建立新資料流後，經常會立即出現此狀態。 |
| 错误 | 此 `Error` status表示資料流的啟用程式已中斷。 |

### 流式处理目标的数据流运行 {#dataflow-runs-for-streaming-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_streaming"
>title="数据流运行详细信息"
>abstract="目标数据流运行详细信息包含有关区段激活状态的信息，以及从实时客户配置文件中获取的量度，以生成唯一标识。要了解更多信息，请查看量度定义指南。"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_streaming"
>title="收到的配置文件"
>abstract="数据流中接收的配置文件总数。该值每 60 分钟更新一次。"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_streaming"
>title="已激活的标识"
>abstract="成功激活到所选目标的配置文件标识的计数。此量度包括创建、更新和从导出的区段中删除的标识。"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_streaming"
>title="排除的标识"
>abstract="根据缺少的属性和同意违规情况，从所选目标的激活中排除的个人配置文件记录的计数。"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed_streaming"
>title="失败的标识"
>abstract="针对所选目标失败的单个配置文件标识的计数。请检查错误诊断，以获取详细信息。"

對於串流目的地， [!UICONTROL 資料流執行] 索引標籤會每小時更新資料流執行中的量度資料。 標示為最顯著的統計資料是用於身分。

身分代表設定檔的不同面向。 例如，如果設定檔同時包含電話號碼和電子郵件地址，則該設定檔將有兩個身分。

會顯示個別執行及其特定量度的清單，以及下列身分總計：

- **[!UICONTROL 身分已啟用]**：成功啟用至所選目的地的設定檔身分總數。 此量度包括创建、更新和从导出的区段中删除的标识。
- **[!UICONTROL 身分已排除]**：根據缺少屬性和同意違規略過用於啟用的設定檔身分總數。
- **[!UICONTROL 身分失敗]**：由於錯誤而未啟用到目的地的設定檔身分總數。

![串流目的地的資料流執行詳細資料](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

每次個別資料流執行都會顯示下列詳細資料：

- **[!UICONTROL 資料流執行開始]**：資料流開始執行的時間。 對於串流資料流執行，Experience Platform會以每小時量度的形式，根據資料流執行的開始來擷取量度。 對於串流資料流執行，如果資料流執行在例如晚上10:30開始，量度會在UI中將開始時間顯示為晚上10:00。
- **[!UICONTROL 處理時間]**：資料流執行處理所花的時間。
   - 對象 **[!UICONTROL 已完成]** 執行時，處理時間量度一律會顯示一小時。
   - 針對仍在中的資料流執行 **[!UICONTROL 處理]** 狀態，擷取所有量度的視窗會開啟一小時以上，以處理對應至資料流執行的所有量度。 例如，上午9:30開始的資料流執行可能會維持處理狀態1小時30分鐘，以擷取及處理所有量度。 然後，處理視窗關閉且資料流執行的狀態更新為 **已完成**，顯示的處理時間會變更為一小時。
- **[!UICONTROL 已接收的設定檔]**：資料流中接收的設定檔總數。
- **[!UICONTROL 身分已啟用]**：在資料流執行期間成功啟用至所選目的地的設定檔身分總數。 此量度包括创建、更新和从导出的区段中删除的标识。
- **[!UICONTROL 身分已排除]**：根據缺少屬性和同意違規從啟用中排除的設定檔身分總數。
- **[!UICONTROL 身分失敗]** 由於錯誤而未啟用到目的地的設定檔身分總數。
- **[!UICONTROL 啟用率]**：已成功啟動或略過的已接收身分的百分比。 下列公式示範如何計算此值：
   ![啟用率公式](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL 狀態]**：代表資料流所處的狀態：可以 [!UICONTROL 已完成] 或 [!UICONTROL 處理中]. [!UICONTROL 已完成] 表示對應資料流執行的所有身分識別已在一小時內匯出。 [!UICONTROL 處理中] 表示資料流執行尚未完成。

若要檢視特定資料流執行的詳細資訊，請從清單中選取執行的開始時間。

資料流執行的詳細資訊頁面包含其他資訊，例如收到的設定檔數、啟用的身分數量、失敗的身分數量以及排除的身分數量。

![串流目的地的資料流詳細資料](../assets/ui/monitor-destinations/dataflow-details-stream.png)

詳細資訊頁面也會顯示失敗的身分和排除的身分清單。 會顯示失敗和排除的身分的相關資訊，包括錯誤代碼、身分計數和說明。 依預設，清單會顯示失敗的身分。 若要顯示略過的身分，請選取 **[!UICONTROL 身分已排除]** 切換。

![串流目的地的資料流記錄](../assets/ui/monitor-destinations/dataflow-records-stream.png)

### 批次目的地的資料流執行 {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation"
>title="数据流运行详细信息"
>abstract="目标数据流运行详细信息包含有关区段激活状态的信息，以及从实时客户配置文件中获取的量度，以生成唯一标识。要了解更多信息，请查看量度定义指南。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-destinations.html#dataflow-runs-for-streaming-destinations" text="流式处理目标的数据流运行"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_batch"
>title="收到的配置文件"
>abstract="数据流中接收的配置文件总数。该值每 60 分钟更新一次。"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_batch"
>title="已激活的标识"
>abstract="成功激活到所选目标的配置文件标识的计数。此量度包括创建、更新和从导出的区段中删除的标识。"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_batch"
>title="排除的标识"
>abstract="根据缺少的属性和同意违规情况，从所选目标的激活中排除的个人配置文件记录的计数。"

對於批次目的地， [!UICONTROL 資料流執行] 索引標籤會提供有關資料流執行的量度資料。 會顯示個別執行及其特定量度的清單，以及下列身分總計：

- **[!UICONTROL 身分已啟用]**：成功啟用至所選目的地的設定檔身分總數。 此量度包括创建、更新和从导出的区段中删除的标识。
- **[!UICONTROL 身分已排除]**：根據缺少屬性和同意違規，從選取的目的地的啟用中排除的個別設定檔身分計數。

![批次目的地的資料流執行檢視](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

每次個別資料流執行都會顯示下列詳細資料：

- **[!UICONTROL 資料流執行開始]**：資料流開始執行的時間。
- **[!UICONTROL 區段]**：與每個資料流執行相關聯的區段名稱。
- **[!UICONTROL 處理時間]**：處理資料流執行所花的時間。
- **[!UICONTROL 已接收的設定檔]**：資料流中接收的設定檔總數。 该值每 60 分钟更新一次。
- **[!UICONTROL 身分已啟用]**：在資料流執行期間成功啟用至所選目的地的設定檔身分總數。 此量度包括创建、更新和从导出的区段中删除的标识。
- **[!UICONTROL 身分已排除]**：根據缺少屬性和同意違規從啟用中排除的設定檔身分總數。
- **[!UICONTROL 狀態]**：代表資料流所處的狀態。 這可以是三種狀態之一： [!UICONTROL 成功]， [!UICONTROL 已失敗]、和 [!UICONTROL 處理中]. [!UICONTROL 成功] 表示資料流作用中，且正在根據其提供的排程匯出資料。 [!UICONTROL 已失敗] 表示資料啟用作業已因錯誤而暫停。 [!UICONTROL 處理中] 表示資料流尚未啟用，通常會在建立新資料流時發生。

若要檢視特定資料流執行的詳細資訊，請從清單中選取執行的開始時間。

>[!NOTE]
>
>根據目的地資料流的排程頻率產生資料流執行。 會分別執行每個資料流 [合併原則](../../profile/merge-policies/overview.md) 套用至區段。

除了資料流清單上顯示的詳細資訊之外，資料流的詳細資訊頁面還會顯示更多關於資料流的具體資訊：

- **[!UICONTROL 資料大小]**：正在匯出的資料流的大小。
- **[!UICONTROL 檔案總數]**：資料流中匯出的檔案總數。
- **[!UICONTROL 上次更新時間]**：上次更新資料流執行的時間。

![批次目的地的資料流執行詳細資料](../assets/ui/monitor-destinations/dataflow-batch.png)

詳細資訊頁面也會顯示失敗的身分和排除的身分清單。 會顯示失敗和排除的身分的相關資訊，包括錯誤碼和說明。 依預設，清單會顯示失敗的身分。 若要顯示排除的身分，請選取 **[!UICONTROL 身分已排除]** 切換。

![批次目的地的資料流記錄](../assets/ui/monitor-destinations/dataflow-records-batch.png)

## 監控目的地控制面板 {#monitoring-destinations-dashboard}

>[!NOTE]
>
>- Experience Platform中目前所有目的地都支援目的地監視功能 *例外* 此 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 和 [自訂個人化](/help/destinations/catalog/personalization/custom-personalization.md) 目的地。
>- 對於 [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)， [Azure事件中樞](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)、和 [HTTP API](/help/destinations/catalog/streaming/http-destination.md) 會估計與已排除、失敗和已啟用的身分相關的量度。 較大量的啟用資料會導致量度的準確性較高。


>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="激活"
>abstract="目标激活视图包含有关区段激活状态的信息，以及从实时客户配置文件中获取的量度，以生成唯一标识。"

若要存取 [!UICONTROL 監視] 儀表板，選取 **[!UICONTROL 監視]** (![監檢視示](../assets/ui/monitor-destinations/monitoring-icon.png))。 一次於 [!UICONTROL 監視] 頁面，選取 [!UICONTROL 目的地]. 此 [!UICONTROL 監視] 儀表板包含有關目的地執行作業的量度和資訊。

使用 [!UICONTROL 目的地] 儀表板來全面瞭解啟動流程的健康狀況。 首先取得所有批次和串流目的地的彙總層級的深入分析，然後深入研究資料流、資料流執行和已啟用的區段的詳細檢視，以深入瞭解您的啟用資料。 中的畫面 [!UICONTROL 監視] 控制面板透過量度和錯誤說明提供可操作的深入分析，協助您疑難排解啟用情況下可能發生的任何問題。

圖示板中心是 [!UICONTROL 啟用] 面板，其中包含量度和圖形，可顯示匯出至串流目的地的資料啟用率，以及匯出至批次目的地的失敗批次資料流執行的相關資料。

![串流和批次啟用圖表](../assets/ui/monitor-destinations/dashboard-graph.png)


依預設，顯示的資料包含過去24小時的啟用資訊。 選取 **[!UICONTROL 過去24小時]** 以調整記錄顯示的時間範圍。 可用選項包括 **[!UICONTROL 過去24小時]**， **[!UICONTROL 過去7天]**、和 **[!UICONTROL 過去30天]**. 或者，您可以在出現的行事曆彈出式視窗中選取日期。 選取日期後，請選取 **[!UICONTROL 套用]** 以調整所顯示資訊的時間範圍。

>[!NOTE]
>
>下列熒幕擷圖顯示啟用率和批次資料流在過去30天（而非過去24小時）內執行。 您可以透過選取調整時間範圍 **[!UICONTROL 過去30天]**.

![變更已啟動目的地的回顧日期範圍](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

使用箭頭圖示(![箭頭圖示](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png))以展開或關閉畫面頂端的卡片，卡片會根據目的地型別（串流或批次）顯示啟動詳細資訊的一目瞭然資訊：

- **[!UICONTROL 串流啟用率]**：代表已成功啟動或略過的已接收身分的百分比。 用於計算此百分比的公式已在本頁面的中進一步說明 [串流目的地的資料流執行](#dataflow-runs-for-streaming-destinations) 區段。
- **[!UICONTROL 批次失敗的資料流執行]**：代表在選取的時間間隔內失敗的資料流執行次數。

![在頁面頂端顯示或解除卡片](../assets/ui/monitor-destinations/monitoring-destinations-toggle-arrow.gif)

此 **[!UICONTROL 啟用]** 圖表預設會顯示，您可以停用它以展開底下的目的地清單。 選取 **[!UICONTROL 度量和圖表]** 切換以停用圖形。

此 **[!UICONTROL 啟用]** 面板會顯示至少包含一個現有帳戶的目的地清單。 此清單也包含接收的個人檔案、啟用的身分、失敗的身分、排除的身分、啟用率、失敗的資料流總數，以及這些目的地的最後更新日期的相關資訊。 並非所有量度都適用於所有目的地型別。 下表概述每個目的地型別、串流或批次可用的量度。

| 量度 | 目的地型別 |
---------|----------|
| **[!UICONTROL 收到的配置文件]** | 串流和批次 |
| **[!UICONTROL 已激活的标识]** | 串流和批次 |
| **[!UICONTROL 失败的标识]** | 串流 |
| **[!UICONTROL 排除的标识]** | 串流和批次 |
| **[!UICONTROL 啟用率]** | 串流 |
| **[!UICONTROL 失敗的資料流總數]** | 批次 |
| **[!UICONTROL 上次更新时间]** | 串流和批次 |

![儀表板所有啟用的目的地](../assets/ui/monitor-destinations/dashboard-destinations.png)

您也可以篩選目的地清單，以僅顯示選取的目的地類別。 選取 **[!UICONTROL 我的目的地]** 下拉式清單，然後選取 [目的地類別](/help/destinations/destination-types.md#categories) 要篩選的目標物件。

![使用下拉式選擇器篩選目的地](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

此外，您可以在搜尋列中輸入目的地，以隔離至單一目的地。 如果您想要檢視目的地的資料流，可以選取篩選器 ![篩選](../assets/ui/monitor-destinations/filter-add.png) 旁邊，可檢視其作用中資料流的清單。

![使用搜尋列篩選目的地](../assets/ui/monitor-destinations/filtered-destinations.png)

如果您想要檢視所有目的地的所有現有資料流，請選取「 」 **[!UICONTROL 資料流]**.

隨即顯示資料流清單，依上次資料流執行排序。 您可以找到要監控的目的地，並選取篩選器，以檢視特定資料流的其他詳細資料 ![篩選](../assets/ui/monitor-destinations/filter-add.png) 旁邊，然後選取篩選器 ![篩選](../assets/ui/monitor-destinations/filter-add.png) 資料流旁邊，您想要瞭解更多相關資訊。

![監控儀表板中醒目提示的所有資料流](../assets/ui/monitor-destinations/dashboard-dataflows.png)

選取資料流以進行進一步檢查後，「資料流詳細資料」頁面會包含切換按鈕，可讓您檢視資料流中已啟動的資料（依資料流執行或區段劃分）。

### 資料流執行檢視 {#dataflow-runs-view}

時間 **[!UICONTROL 資料流執行]** 選取時，您可以看到所選資料流的資料流執行清單，以及每次執行的進一步資訊。

>[!INFO]
>
>對於串流目的地的資料流，資料流執行會劃分為每小時時段。 每個每小時視窗都會產生對應的資料流執行ID。
>
>針對批次目的地的資料流，每個區段都會根據區段啟用排程頻率產生對應的資料流執行。 例如，如果您為相同目的地資料流中的五個區段設定每日排程啟動，則每天將會產生五個個別的資料流執行。

![「流量執行」面板](../assets/ui/monitor-destinations/dashboard-flow-runs-view.png)

使用 **[!UICONTROL 僅顯示失敗]** 切換以僅顯示資料流的失敗執行。

![資料流執行 — 僅顯示失敗切換](../assets/ui/monitor-destinations/dataflow-runs-show-failures-only.gif)

### 區段層級檢視 {#segment-level-view}

時間 **[!UICONTROL 區段]** ，您會看到在所選時間範圍內對所選資料流啟用的區段清單。 此畫麵包含啟用的身分、排除的身分以及上次資料流執行的狀態和時間的區段層級資訊。 透過檢閱已排除和已啟用的身分的量度，您可以驗證區段是否已成功啟用。

例如，您正在對Amazon S3目的地「加州忠誠會員12月」啟用名為「加州忠誠會員」的區段。 假設所選區段中有100個設定檔，但100個設定檔中只有80個包含忠誠度ID屬性，而您已將匯出對應規則定義為 `loyalty.id` 為必填欄位。 在此情況下，在區段層級，您會看到80個身分識別已啟用，20個身分識別已排除。

>[!IMPORTANT]
>
>請注意與區段層級量度相關的目前限制：
>- 區段層級檢視目前僅適用於批次目的地。
>- 目前僅針對成功的資料流執行記錄區段層級量度。 失敗的資料流執行和排除的記錄不會記錄它們。


![資料流面板中的區段](../assets/ui/monitor-destinations/dashboard-segments-view.png)

在區段層級檢視中，度量會在所選時間範圍內跨多個資料流執行進行彙總。 如果有多個資料流執行，您可以從區段層級向下切入，檢視每個資料流執行（依選取的區段篩選）的劃分。
使用篩選按鈕 ![篩選](../assets/ui/monitor-destinations/filter-add.png) 若要向下鑽研資料流中每個區段的資料流執行檢視，請執行下列動作。

### 資料流執行頁面 {#dataflow-runs-page}

「資料流執行」頁面會顯示資料流執行的相關資訊，包括資料流執行開始時間、處理時間、收到的設定檔、已啟用的身分、已排除的身分、身分失敗、啟用率和狀態。

當您從「 」向下切入資料流執行頁面時， [區段層級檢視](#segment-level-view)，您可選擇透過下列選項篩選資料流執行：

- **[!UICONTROL 具有失敗身分的資料流執行]**：針對選取的區段，此選項會列出所有無法啟用的資料流執行。 若要檢查特定資料流執行中的身分識別失敗的原因，請參閱 [資料流執行詳細資訊頁面](#dataflow-run-details-page) 用於該資料流執行。
- **[!UICONTROL 具有已略過身分的資料流執行]**：針對選取的區段，此選項會列出部分身分未完全啟用且部分設定檔已略過的所有資料流執行。 若要檢查某個資料流執行中的身分識別為何被略過，請參閱 [資料流執行詳細資訊頁面](#dataflow-run-details-page) 用於該資料流執行。
- **[!UICONTROL 具有已啟用的身分的資料流執行]**：針對選取的區段，此選項會列出具有已成功啟用的身分的所有資料流執行。

![篩選區段的資料流執行](/help/dataflows/assets/ui/monitor-destinations/dataflow-runs-segment-filter.png)

若要檢視特定資料流執行的詳細資訊，請選取篩選器 ![篩選](../assets/ui/monitor-destinations/filter-add.png) 資料流執行開始時間旁邊，可檢視資料流執行詳細資訊頁面。

![資料流會在監控儀表板中執行篩選](../assets/ui/monitor-destinations/dataflow-runs-filter.png)

### 資料流執行詳細資訊頁面 {#dataflow-run-details-page}

除了顯示在資料流執行清單上的詳細資訊之外，「資料流執行詳細資訊」頁面還會顯示有關資料流的更多特定資訊：

- **[!UICONTROL 資料流執行ID]**：資料流的ID。
- **[!UICONTROL IMS組織ID]**：資料流所屬的組織。
- **[!UICONTROL 上次更新時間]**：上次更新資料流執行的時間。

詳細資訊頁面也有切換功能，可在資料流執行錯誤和區段之間切換。 此選項僅適用於批次目的地中的資料流執行。

資料流執行錯誤檢視會顯示失敗的身分和已排除的身分清單。 會顯示失敗和排除的身分的相關資訊，包括錯誤代碼、身分計數和說明。 依預設，清單會顯示失敗的身分。 若要顯示略過的身分，請選取 **[!UICONTROL 身分已排除]** 切換。

![排除的身分切換](../assets/ui/monitor-destinations/identities-excluded.png)

時間 **[!UICONTROL 區段]** ，您會看到在所選資料流執行中啟動的區段清單。 此畫麵包含啟用的身分、排除的身分以及上次資料流執行的狀態和時間的區段層級資訊。

![資料流執行 — 區段檢視](../assets/ui/monitor-destinations/dataflow-run-segments-view.png)

## 后续步骤 {#next-steps}

依照本指南，您現在瞭解如何監控批次和串流目的地的資料流，包括所有相關資訊，例如處理時間、啟用率和狀態。 若要進一步瞭解Platform中的資料流，請閱讀 [資料流概觀](../home.md). 若要進一步瞭解目的地，請閱讀 [目的地概觀](../../destinations/home.md).
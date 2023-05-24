---
keywords: Experience Platform；首頁；熱門主題；監控設定檔；監控資料流；資料流；設定檔；即時客戶設定檔；
description: 即時客戶設定檔可讓您透過合併來自多個管道（包括線上、離線、CRM和協力廠商）的資料，檢視每個個別客戶的整體檢視。 本教學課程提供如何使用Experience Platform使用者介面監控設定檔資料流的指示。
title: 在UI中監視設定檔的資料流
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 9%

---

# 在UI中監視設定檔的資料流

即時客戶設定檔可讓您透過合併來自多個管道（包括線上、離線、CRM和協力廠商）的資料，檢視每個個別客戶的整體檢視。 档案允许您将您的客户数据整合到一个统一视图中，并提供每个客户交互的带时间戳的可操作帐户。

監控儀表板可讓您以視覺化方式呈現設定檔中的資料活動，包括資料設定檔的狀態。 本教學課程提供有關如何使用監視儀表板來使用Experience Platform使用者介面監視資料設定檔的說明，以允許您追蹤設定檔處理的狀態。

## 快速入门 {#getting-started}

本指南需要您實際瞭解下列Adobe Experience Platform元件：

- [資料流](../home.md)：資料流可呈現跨平台行動資料的資料作業。 資料流會跨不同服務進行設定，有助於將資料從來源聯結器移至目標資料集，以及 [!DNL Identity] 和 [!DNL Profile]，並至 [!DNL Destinations].
   - [資料流執行](../../sources/notifications.md)：資料流執行是根據所選資料流的頻率設定的週期性排程作業。
- [即時客戶個人檔案](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

## 監控設定檔儀表板 {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="配置文件处理"
>abstract="配置文件处理视图包含有关提取到配置文件服务的记录的信息，包括创建的配置文件片段数、更新的配置文件片段数以及配置文件片段总数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_profile"
>title="数据流运行详细信息"
>abstract="数据流运行详细信息页面显示有关配置文件数据流运行的更多信息，包括其组织 ID 和数据流运行 ID。"

若要存取 **[!UICONTROL 設定檔]** 儀表板，選取 **[!UICONTROL 監視]** 左側導覽列中。 一次於 **[!UICONTROL 監視]** 頁面，選取 **[!UICONTROL 設定檔]** 卡片。

![設定檔卡片。 畫面上會顯示有關已接收記錄數、已建立和已更新設定檔片段數以及成功率的資訊。](../assets/ui/monitor-profiles/focus-card.png)

在主要上 **[!UICONTROL 設定檔]** 儀表板， **[!UICONTROL 設定檔]** 卡片會顯示關於已接收記錄總數、已建立和已更新設定檔片段數，以及已建立和已更新設定檔片段成功率的資訊。

儀表板本身包含有關設定檔處理的量度。 預設情況下，儀表板將顯示您組織過去24小時來源的設定檔處理細節。

![設定檔控制面板。 顯示每個來源接收之設定檔記錄數目的相關資訊。](../assets/ui/monitor-profiles/sources.png)

此 [!UICONTROL 設定檔處理] 頁面包含擷取到的記錄資訊 [!DNL Profile]，包括已建立的設定檔片段數、已更新的設定檔片段數，以及設定檔片段總數。

下列量度適用於此儀表板檢視：

| 量度 | 描述 |
| -------| ----------- |
| **[!UICONTROL 來源名稱]** | 來源的名稱。 |
| **[!UICONTROL 已接收的记录]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 失败的记录]** | 已擷取但未擷取的記錄數 [!DNL Profile] 因為發生錯誤。 |
| **[!UICONTROL 已建立的設定檔片段]** | 淨新增數量 [!DNL Profile] 片段已新增。 |
| **[!UICONTROL 已更新設定檔片段]** | 現有數量 [!DNL Profile] 片段已更新。 |
| **[!UICONTROL 設定檔片段總數]** | 寫入的記錄總數 [!DNL Profile]，包括所有現有 [!DNL Profile] 片段已更新並新增 [!DNL Profile] 片段已建立。 |
| **[!UICONTROL 失敗的資料流總數]** | 失敗的資料流執行次數。 |

您可以選取篩選器圖示 ![篩選圖示](../assets/ui/monitor-profiles/filter.png) 在來源名稱旁邊，可檢視該所選來源資料流的設定檔處理資訊。

![篩選圖示會反白顯示。 選取此圖示可讓您檢視所選來源的資料流。](../assets/ui/monitor-profiles/sources-filter.png)

或者，您可以選取 **[!UICONTROL 資料流]** 在切換上，可檢視貴組織過去24小時資料流的設定檔處理詳細資料。

![設定檔控制面板。 將顯示有關每個資料流接收的設定檔記錄數的資訊。](../assets/ui/monitor-profiles/dataflows.png)

下列量度適用於此儀表板檢視：

| 量度 | 描述 |
| -------| ----------- |
| **[!UICONTROL 数据流]** | 資料流的名稱。 |
| **[!UICONTROL 数据集]** | 資料流所插入的資料集名稱。 |
| **[!UICONTROL 來源名稱]** | 資料流所屬的來源名稱。 |
| **[!UICONTROL 已接收的记录**] | 從資料湖接收的記錄數。 |
| **[!UICONTROL 失败的记录]** | 已擷取但未擷取的記錄數 [!DNL Profile] 因為發生錯誤。 |
| **[!UICONTROL 已建立的設定檔片段]** | 淨新增數量 [!DNL Profile] 片段已新增。 |
| **[!UICONTROL 已更新設定檔片段]** | 現有數量 [!DNL Profile] 片段已更新 |
| **[!UICONTROL 設定檔片段總數]** | 寫入的記錄總數 [!DNL Profile]，包括所有現有 [!DNL Profile] 片段已更新並新增 [!DNL Profile] 片段已建立。 |
| **[!UICONTROL 失敗的資料流執行總數]** | 失敗的資料流執行次數。 |
| **[!UICONTROL 上次使用時間]** | 上次執行資料流的時間戳記。 |

選取篩選圖示 ![篩選](../assets/ui/monitor-profiles/filter.png) 資料流執行開始時間旁邊，檢視更多有關您的資訊 [!DNL Profile] 資料流執行。

![篩選圖示會反白顯示。 選取此圖示可讓您檢視所選資料流的詳細資訊。](../assets/ui/monitor-profiles/dataflows-filter.png)

此 [!UICONTROL 資料流執行詳細資料] 頁面顯示更多關於您的資訊 [!DNL Profile] 資料流執行，包括其組織ID和資料流執行ID。 此頁面也會顯示提供的對應錯誤碼和錯誤訊息 [!DNL Profile]，以瞭解擷取過程中是否發生任何錯誤。

![此時會顯示一個儀表板，顯示所選資料流的詳細資訊。](../assets/ui/monitor-profiles/dataflow-run-details.png)

下列量度適用於此儀表板檢視：

| 量度 | 描述 |
| -------| ----------- |
| **[!UICONTROL 已接收的记录]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 失败的记录]** | 已擷取但未擷取的記錄數 [!DNL Profile] 因為發生錯誤。 |
| **[!UICONTROL 已建立的設定檔片段]** | 淨新增數量 [!DNL Profile] 片段已新增。 |
| **[!UICONTROL 已更新設定檔片段]** | 現有數量 [!DNL Profile] 片段已更新。 |
| **[!UICONTROL 状态]** | 定義資料流的整體狀態。 可能的狀態值包括： <ul><li>`Success`：指出資料流作用中，且正在根據提供的排程擷取資料。</li><li>`Failed`：指出資料流的啟用程式已因錯誤而中斷。 </li><li>`Processing`：指出資料流尚未啟用。 建立新資料流後，經常會立即出現此狀態。</li></ul> |
| **[!UICONTROL 資料流執行開始]** | 資料流開始執行的日期和時間。 |
| **[!UICONTROL 上次更新时间]** | 資料流上次更新的日期和時間。 |
| **[!UICONTROL 錯誤摘要]** | 如果資料流執行失敗，這會顯示錯誤碼和資料流執行失敗原因的摘要。 |
| **[!UICONTROL 資料流執行ID]** | 資料流執行的ID。 |
| **[!UICONTROL IMS組織ID]** | 資料流執行所屬的組織ID。 |

此外，您可以選取切換來檢視失敗的記錄或略過的記錄。 錯誤區段包含有關錯誤代碼和失敗或排除的記錄數的詳細資訊。

---
keywords: Experience Platform；首頁；熱門主題；監控身分；監控資料流；資料流；身分；
description: Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，藉此全面瞭解客戶及其行為。 本教學課程提供如何使用Experience Platform使用者介面監控具有身分的資料流的指示。
title: 在UI中監視身分識別的資料流
type: Tutorial
exl-id: 735b0e52-74f6-47fe-98c6-e12a633b6f57
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 8%

---

# 監視UI中身分的資料流

Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，藉此全面瞭解客戶及其行為。

監控儀表板可讓您以視覺化方式呈現身分內的資料活動，包括資料身分的狀態。 本教學課程提供有關如何使用監控儀表板來使用Experience Platform使用者介面監控資料身分的說明，讓您能夠追蹤身分處理狀態。

## 快速入门 {#getting-started}

- [資料流](../home.md)：資料流可呈現跨平台行動資料的資料作業。 資料流會跨不同服務進行設定，有助於將資料從來源聯結器移至目標資料集，以及 [!DNL Identity] 和 [!DNL Profile]，並至 [!DNL Destinations].
   - [資料流執行](../../sources/notifications.md)：資料流執行是根據所選資料流的頻率設定的週期性排程作業。
- [Identity Service](../../identity-service/home.md)：透過跨裝置和系統橋接身分，更能瞭解個別客戶及其行為。
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，以協助開發及改進數位體驗應用程式。

## 監控身分儀表板 {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="标识处理"
>abstract="标识处理视图包含有关提取到标识服务的记录的信息，包括添加的标识数量、创建的图表数量和更新的图表数量。查看量度定义指南以了解有关量度和图表的更多信息。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="数据流运行详细信息"
>abstract="数据流运行详细信息页面显示有关标识数据流运行的更多信息，包括其组织 ID 和数据流运行 ID。"

若要存取 **[!UICONTROL 身分]** 儀表板，選取 **[!UICONTROL 監視]** 左側導覽列中。 一次於 **[!UICONTROL 監視]** 頁面，選取 **[!UICONTROL 身分]** 卡片。

![身分卡。 畫面上會顯示有關已接收記錄數、已擷取記錄數以及成功率的資訊。](../assets/ui/monitor-identities/focus-card.png)

在主要上 **[!UICONTROL 身分]** 儀表板， **[!UICONTROL 身分]** 卡片會顯示所接收記錄總數、所擷取的記錄數以及記錄擷取成功率的相關資訊。

儀表板本身包含有關身分處理的量度。 預設情況下，儀表板將顯示您組織過去24小時來源的身分處理詳細資訊。

![身分控制面板。 顯示每個來源接收之記錄數目的相關資訊。](../assets/ui/monitor-identities/sources.png)

此 [!UICONTROL 身分處理中] 頁面包含擷取到的記錄資訊 [!DNL Identity Service]，包括新增的身分數量、建立的圖表和更新的圖表。

下列量度適用於此儀表板檢視：

| 身分量度 | 描述 |
| ---------------- | ----------- |
| **[!UICONTROL 已接收的记录]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 失败的记录]** | 因資料錯誤而未擷取至Platform的記錄數。 |
| **[!UICONTROL 跳过的记录数]** | 已擷取但未擷取的記錄數 [!DNL Identity Service] 因為記錄列中只有一個識別碼。 |
| **[!UICONTROL 已提取的记录]** | 擷取的記錄數 [!DNL Identity Service]. |
| **[!UICONTROL 身分已新增]** | 新增至的淨新識別碼數目 [!DNL Identity Service]. |
| **[!UICONTROL 已建立的圖表]** | 在中建立的淨新身分圖表數目 [!DNL Identity Service]. |
| **[!UICONTROL 圖表已更新]** | 以新邊更新的現有身分圖表數量。 |
| **[!UICONTROL 失敗的資料流總數]** | 失敗的資料流執行次數。 |

您可以選取篩選器圖示 ![篩選圖示](../assets/ui/monitor-identities/filter.png) 在來源名稱旁邊，可檢視該所選來源資料流的身分處理資訊。

![篩選圖示會反白顯示。 選取此圖示可讓您檢視所選來源的資料流。](../assets/ui/monitor-identities/sources-filter.png)

或者，您可以選取 **[!UICONTROL 資料流]** 在切換上，可檢視您組織過去24小時資料流的身分處理詳細資料。

![身分控制面板。 顯示有關每個資料流接收的身分數目的資訊。](../assets/ui/monitor-identities/dataflows.png)

下列量度適用於此儀表板檢視：

| 量度 | 描述 |
| -------| ----------- |
| **[!UICONTROL 数据流]** | 資料流的名稱。 |
| **[!UICONTROL 数据集]** | 資料流所插入的資料集名稱。 |
| **[!UICONTROL 來源名稱]** | 資料流所屬的來源名稱。 |
| **[!UICONTROL 已接收的记录]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 失败的记录]** | 因資料錯誤而未擷取至Platform的記錄數。 |
| **[!UICONTROL 跳过的记录数]** | 已擷取但未擷取的記錄數 [!DNL Identity Service] 因為記錄列中只有一個識別碼。 |
| **[!UICONTROL 已提取的记录]** | 擷取的記錄數 [!DNL Identity Service]. |
| **[!UICONTROL 記錄總數]** | 所有記錄的總數，包括失敗的記錄、略過的記錄、新增的身分和重複的記錄。 |
| **[!UICONTROL 身分已新增]** | 新增至的淨新識別碼數目 [!DNL Identity Service]. |
| **[!UICONTROL 已建立的圖表]** | 在中建立的淨新身分圖表數目 [!DNL Identity Service]. |
| **[!UICONTROL 圖表已更新]** | 以新邊更新的現有身分圖表數量。 |
| **[!UICONTROL 失敗的資料流總數]** | 失敗的資料流執行次數。 |

選取篩選圖示 ![篩選](../assets/ui/monitor-identities/filter.png) 資料流執行開始時間旁邊，檢視更多有關您的資訊 [!DNL Identity] 資料流執行。

![篩選圖示會反白顯示。 選取此圖示可讓您檢視所選資料流的詳細資訊。](../assets/ui/monitor-identities/dataflows-filter.png)

此 [!UICONTROL 資料流執行詳細資料] 頁面顯示更多關於您的資訊 [!DNL Identity] 資料流執行，包括其組織ID和資料流執行ID。 此頁面也會顯示提供的對應錯誤碼和錯誤訊息 [!DNL Identity Service]，以瞭解擷取過程中是否發生任何錯誤。

![此時會顯示一個儀表板，顯示所選資料流的詳細資訊。](../assets/ui/monitor-identities/dataflow-run-details.png)

下列量度適用於此儀表板檢視：

| 量度 | 描述 |
| -------| ----------- |
| **[!UICONTROL 已接收的记录]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 失败的记录]** | 因資料錯誤而未擷取至Platform的記錄數。 |
| **[!UICONTROL 跳过的记录数]** | 已擷取但未擷取的記錄數 [!DNL Identity Service] 因為記錄列中只有一個識別碼。 |
| **[!UICONTROL 已提取的记录]** | 擷取的記錄數 [!DNL Identity Service]. |
| **[!UICONTROL 身分已新增]** | 新增至的淨新識別碼數目 [!DNL Identity Service]. |
| **[!UICONTROL 已建立的圖表]** | 在中建立的淨新身分圖表數目 [!DNL Identity Service]. |
| **[!UICONTROL 圖表已更新]** | 以新邊更新的現有身分圖表數量。 |
| **[!UICONTROL 状态]** | 定義資料流的整體狀態。 可能的狀態值包括： <ul><li>`Success`：指出資料流作用中，且正在根據提供的排程擷取資料。</li><li>`Failed`：指出資料流的啟用程式已因錯誤而中斷。 </li><li>`Processing`：指出資料流尚未啟用。 建立新資料流後，經常會立即出現此狀態。</li></ul> |
| **[!UICONTROL 資料流執行開始]** | 資料流開始執行的日期和時間。 |
| **[!UICONTROL 上次更新时间]** | 資料流上次更新的日期和時間。 |
| **[!UICONTROL 錯誤摘要]** | 如果資料流執行失敗，這會顯示錯誤碼和資料流執行失敗原因的摘要。 |
| **[!UICONTROL 資料流執行ID]** | 資料流執行的ID。 |
| **[!UICONTROL IMS組織ID]** | 資料流執行所屬的組織ID。 |

此外，您可以選取切換來檢視失敗的記錄或略過的記錄。 錯誤區段包含有關錯誤代碼和失敗或排除的記錄數的詳細資訊。

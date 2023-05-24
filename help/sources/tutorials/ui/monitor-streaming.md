---
keywords: Experience Platform；首頁；熱門主題；監控帳戶；監控資料流；資料流
description: Adobe Experience Platform中的來源聯結器可讓您依排程擷取外部來源的資料。 本教學課程提供從來源工作區監控串流資料流的步驟。
title: 在UI中監視串流來源的資料流
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: 647f2780798dcf55a68e156af3318924c352a442
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 10%

---

# 在UI中監視串流來源的資料流

本教學課程涵蓋使用監控串流來源資料流的步驟。 [!UICONTROL 來源] 工作區。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [資料流](../../../dataflows/home.md)：資料流可呈現跨平台行動資料的資料作業。 資料流會跨不同服務進行設定，有助於將資料從來源聯結器移至目標資料集，以及 [!DNL Identity] 和 [!DNL Profile]，並至 [!DNL Destinations].
   * [資料流執行](../../notifications.md)：資料流執行是根據所選資料流的頻率設定的週期性排程作業。
* [來源](../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 監控串流來源的資料流

在Platform UI中選取 **[!UICONTROL 來源]** 以存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

若要檢視串流來源的現有資料流，請選取「 」 **[!UICONTROL 資料流]** 從頂端標題。

![目錄](../../images/tutorials/monitor-streaming/catalog.png)

此 [!UICONTROL 資料流] 頁面包含貴組織中所有現有資料流的清單，包括有關其來源資料、帳戶名稱和資料流執行狀態的資訊。

選取您要檢視的資料流名稱。

![資料流](../../images/tutorials/monitor-streaming/dataflows.png)

下表包含資料流執行狀態的詳細資訊：

| 状态 | 描述 |
| ------ | ----------- |
| 已完成 | 此 `Completed` status表示對應資料流執行的所有記錄皆在一小時內處理。 A `Completed` 狀態在資料流執行中仍可包含錯誤。 |
| 成功 | 此 `Success` status表示對應資料流執行的所有記錄都在一小時期間內處理，且在資料流執行期間沒有發生錯誤。 |
| 处理时间 | 此 `Processing` status表示資料流尚未啟用。 建立新資料流後，經常會立即出現此狀態。 |
| 错误 | 此 `Error` status表示資料流的啟用程式已中斷。 |
| 無回合 | 此 `No runs` status表示已建立資料流，但未開始任何資料流執行。 |

此 [!UICONTROL 資料流活動] 頁面會顯示串流資料流的特定資訊。 頂端橫幅包含所選日期範圍內所有串流資料流執行的已擷取和失敗記錄的累計數量。

![資料流活動](../../images/tutorials/monitor-streaming/dataflow-activity.png)

依預設，顯示的資料包含過去七天的擷取率。 選取 **[!UICONTROL 過去7天]** 以調整記錄顯示的時間範圍。

此時會出現一個日曆快顯視窗，為您提供替代擷取時間範圍的選項。 您可以設定資料流執行時間範圍，以檢視過去7天或過去30天的資料流執行。 或者，您也可以設定互動式行事曆，以設定自訂的時間範圍。 完成後，選取 **[!UICONTROL 套用]**.

![行事曆](../../images/tutorials/monitor-streaming/calendar.png)

頁面下半部會顯示每次資料流執行時接收、擷取和失敗的記錄數資訊。 每個資料流執行都會記錄在一個每小時的視窗中。

![資料流 — 執行](../../images/tutorials/monitor-streaming/dataflow-run.png)

### 資料流執行量度 {#dataflow-run-metrics}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_received"
>title="已接收的记录"
>abstract="“已接收的记录”量度指示数据流中接收的记录总数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_ingested"
>title="已提取的记录"
>abstract="“已提取的记录”量度指示已提取到数据湖中的记录总数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_failed"
>title="失败的记录"
>abstract="“失败的记录”量度指示因数据错误而未被提取到数据湖的记录总数。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_warnings"
>title="带警告的记录"
>abstract="“带警告的记录”指示带映射器转换警告的已提取记录总数。所有映射器转换错误都报告为警告，部分提取的行被视为成功并显示警告"
>text="Learn more in documentation"

每次個別資料流執行都會顯示下列詳細資料：

* **[!UICONTROL 資料流執行開始]**：資料流開始執行的時間。
* **[!UICONTROL 處理時間]**：資料流處理所花的時間。
* **[!UICONTROL 已接收的記錄]**：在資料流中從來源聯結器收到的記錄總數。
* **[!UICONTROL 記錄已擷取]**：擷取到的記錄總數 [!DNL Data Lake].
* **[!UICONTROL 有警告的記錄]**：已擷取含有警告的記錄總數。 所有對應程式轉換錯誤都會回報為警告，而部分擷取的列會標示為 `success` 有警告。 **注意**：只有串流來源才支援擷取含有警告的記錄。
* **[!UICONTROL 記錄失敗]**：未擷取的記錄數 [!DNL Data Lake] 因為資料中的錯誤。
* **[!UICONTROL 擷取率]**：擷取的記錄成功率 [!DNL Data Lake]. 此量度適用於 [!UICONTROL 部分擷取] 已啟用。
* **[!UICONTROL 狀態]**：代表資料流所處的狀態：可以 [!UICONTROL 已完成] 或 [!UICONTROL 處理中]. [!UICONTROL 已完成] 表示對應資料流執行的所有記錄都在一小時內處理。 [!UICONTROL 處理中] 表示資料流執行尚未完成。

此 [!UICONTROL 資料流執行概觀] 頁面包含資料流的其他資訊，例如其對應的資料流執行ID、目標資料集和組織ID。

有錯誤的流程執行也包含 [!UICONTROL 資料流執行錯誤] 面板，顯示導致執行失敗的特定錯誤，以及失敗的記錄總數。

![資料流 — 執行 — 概觀](../../images/tutorials/monitor-streaming/dataflow-run-overview.png)

### 檢視有警告的記錄 {#warnings}

[!UICONTROL 有警告的記錄] 顯示流程執行期間發生的對應程式轉換警告清單。 部分擷取的列會被視為成功，如果發現任何對應程式轉換錯誤，則會附加警告。

依預設，所有對應程式轉換錯誤都會被視為警告，除非它們符合下列任一條件：

* 語法錯誤
* 對不存在之屬性的參照
* XDM資料型別不相符

若要檢視錯誤診斷，請選取 **[!UICONTROL 預覽錯誤診斷]**.

![有警告的記錄](../../images/tutorials/monitor-streaming/records-with-warnings.png)

此 [!UICONTROL 錯誤診斷預覽] 視窗可讓您預覽與資料流執行相關的最多100個錯誤和/或警告。 您也可以從這裡下載內嵌失敗資訊清單，瞭解更多資訊，請使用 [!DNL Data Access] API。

![診斷](../../images/tutorials/monitor-streaming/diagnostics.png)

## 后续步骤

依照本教學課程，您已成功使用 [!UICONTROL 來源] 工作區，用來監控您的串流資料流，並識別導致任何資料流失敗的錯誤。 如需詳細資訊，請參閱下列檔案：

* [來源概觀](../../home.md)
* [資料流概觀](../../../dataflows/home.md)

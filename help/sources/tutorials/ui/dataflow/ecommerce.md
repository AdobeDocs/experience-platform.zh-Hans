---
keywords: Experience Platform；首頁；熱門主題；電子商務聯結器；電子商務
solution: Experience Platform
title: 在UI中使用電子商務來源建立資料流
type: Tutorial
description: 資料流是排程的工作，可擷取來源中的資料並將其擷取至Platform資料集。 本教學課程提供如何使用Platform UI為電子商務來源建立資料流的步驟。
exl-id: ee1382c5-78ac-4765-8883-0a922772bb20
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 0%

---

# 在UI中使用電子商務來源建立資料流

資料流是排程的工作，可從Adobe Experience Platform的來源擷取資料並擷取資料到資料集。 本教學課程提供如何使用Platform UI為電子商務來源建立資料流的步驟。

>[!NOTE]
>
>為了建立資料流，您必須擁有使用電子商務來源的已驗證帳戶。 在UI中建立不同電子商務來源帳戶的教學課程清單可在以下網址找到： [來源概觀](../../../home.md#ecommerce).

## 快速入门

本教學課程需要深入瞭解下列Platform元件：

* [來源](../../../home.md)：Platform可從各種來源擷取資料，同時讓您能夠使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [[!DNL Experience Data Model (XDM)] 系統](../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [[!DNL Data Prep]](../../../../data-prep/home.md)：讓資料工程師可對應、轉換及驗證來往於Experience Data Model (XDM)的資料。

## 新增資料

建立您的電子商務來源帳戶後， **[!UICONTROL 新增資料]** 步驟隨即顯示，提供您瀏覽電子商務來源帳戶表格階層的介面。

* 介面的左半部分是瀏覽器，顯示帳戶中包含的資料表清單。 介面也包含搜尋選項，可讓您快速識別要使用的來源資料。
* 介面的右半部分是預覽面板，可讓您預覽最多100列資料。

>[!NOTE]
>
>搜尋來源資料選項適用於除Adobe Analytics以外的所有表格來源。 [!DNL Amazon Kinesis]、和 [!DNL Azure Event Hubs].

找到來源資料後，請選取表格，然後選取 **[!UICONTROL 下一個]**.

![select-data](../../../images/tutorials/dataflow/table-based/select-data.png)

## 提供資料流詳細資料

此 [!UICONTROL 資料流詳細資料] 頁面可讓您選取要使用現有資料集還是新資料集。 在此程式中，您也可以為以下專案進行設定： [!UICONTROL 設定檔資料集]， [!UICONTROL 錯誤診斷]， [!UICONTROL 部分擷取]、和 [!UICONTROL 警報].

![資料流 — 詳細資料](../../../images/tutorials/dataflow/table-based/dataflow-detail.png)

### 使用現有的資料集

若要將資料內嵌至現有資料集，請選取「 」 **[!UICONTROL 現有資料集]**. 您可以使用來擷取現有的資料集 [!UICONTROL 進階搜尋] 選項，或是透過在下拉式選單中捲動現有資料集清單的方式。 選取資料集後，請為資料流提供名稱和說明。

![existing-data](../../../images/tutorials/dataflow/table-based/existing-dataset.png)

### 使用新資料集

若要內嵌至新資料集，請選取「 」 **[!UICONTROL 新資料集]** 然後提供輸出資料集名稱和選擇性說明。 接下來，使用 [!UICONTROL 進階搜尋] 選項或透過捲動下拉式選單中的現有結構描述清單的方式。 選取結構描述後，請為資料流提供名稱和說明。

![新資料集](../../../images/tutorials/dataflow/table-based/new-dataset.png)

### 啟用 [!DNL Profile] 和錯誤診斷

接下來，選取 **[!UICONTROL 設定檔資料集]** 切換以啟用您的資料集 [!DNL Profile]. 這可讓您建立實體屬性和行為的整體檢視。 來自所有人的資料 [!DNL Profile] — 啟用的資料集將包含在 [!DNL Profile] 和變更會在您儲存資料流時套用。

[!UICONTROL 錯誤診斷] 針對資料流中發生的任何錯誤記錄，啟用詳細的錯誤訊息產生，同時 [!UICONTROL 部分擷取] 可讓您擷取包含錯誤的資料，最多可擷取您手動定義的特定臨界值。 請參閱 [部分批次擷取概觀](../../../../ingestion/batch-ingestion/partial.md) 以取得詳細資訊。

![設定檔與錯誤](../../../images/tutorials/dataflow/table-based/profile-and-errors.png)

### 啟用警示

您可以啟用警報以接收有關資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱來源警報](../alerts.md).

當您完成提供詳細資訊給資料流時，請選取「 」 **[!UICONTROL 下一個]**.

![警報](../../../images/tutorials/dataflow/table-based/alerts.png)

## 將資料欄位對應至XDM結構描述

此 [!UICONTROL 對應] 步驟隨即顯示，為您提供介面，用於將來源結構描述中的來源欄位對應到目標結構描述中適當的目標XDM欄位。

Platform會根據您選取的目標結構描述或資料集，為自動對應的欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。 您可以視需要選擇直接對應欄位，或使用資料準備函式來轉換來源資料，以衍生計算值或計算值。 如需使用對應程式介面和計算欄位的完整步驟，請參閱 [資料準備UI指南](../../../../data-prep/ui/mapping.md).

成功對應來源資料後，請選取 **[!UICONTROL 下一個]**.

![對應](../../../images/tutorials/dataflow/table-based/mapping.png)

## 排程內嵌執行

此 [!UICONTROL 排程] 步驟隨即顯示，可讓您設定擷取排程，以使用已設定的對應自動擷取選取的來源資料。 根據預設，排程設定為 `Once`. 若要調整您的擷取頻率，請選取 **[!UICONTROL 頻率]** ，然後從下拉式選單中選取選項。

>[!TIP]
>
>間隔和回填在一次性內嵌期間不可見。

![排程](../../../images/tutorials/dataflow/table-based/scheduling.png)

如果您將擷取頻率設為 `Minute`， `Hour`， `Day`，或 `Week`，則必須設定間隔，以建立每次擷取之間所設定的時間範圍。 例如，擷取頻率設為 `Day` 而間隔設定為 `15` 表示您的資料流已排程每15天擷取一次資料。

在此步驟中，您也可以啟用 **回填** 和定義資料增量擷取的欄。 回填是用來擷取歷史資料，而您為增量擷取定義的欄則允許將新資料與現有資料區分開來。

請參閱下表以取得排程設定的詳細資訊。

| 字段 | 描述 |
| --- | --- |
| 频度 | 內嵌發生的頻率。 可選擇頻率包括 `Once`， `Minute`， `Hour`， `Day`、和 `Week`. |
| 間隔 | 設定所選頻率間隔的整數。 間隔值應為非零整數，且應設定為大於或等於15。 |
| 開始時間 | UTC時間戳記，指出第一次內嵌設定於何時發生。 開始時間必須大於或等於您目前的UTC時間。 |
| 回填 | 布林值，決定最初擷取的資料。 如果已啟用回填，則在第一次排程的擷取期間，將會擷取指定路徑中的所有目前檔案。 如果停用回填，則只會擷取在第一次執行擷取和開始時間之間載入的檔案。 將不會擷取在開始時間之前載入的檔案。 |
| 載入增量資料的方式 | 一個選項，其中包含一組型別、日期或時間的篩選來源結構描述欄位。 此欄位用於區分新資料和現有資料。 將根據所選欄的時間戳記擷取增量資料。 |

![回填](../../../images/tutorials/dataflow/table-based/backfill.png)

## 檢閱您的資料流

此 **[!UICONTROL 檢閱]** 步驟隨即顯示，可讓您在建立新資料流之前對其進行檢閱。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **[!UICONTROL 指派資料集和對應欄位]**：顯示要將來源資料擷取到哪個資料集中，包括資料集所堅持的結構描述。
* **[!UICONTROL 排程]**：顯示內嵌排程的作用中期間、頻率和間隔。

檢閱資料流後，選取 **[!UICONTROL 完成]** 並留出一些時間來建立資料流。

![檢閱](../../../images/tutorials/dataflow/table-based/review.png)

## 監視資料流

建立資料流後，您可以監視透過它擷取的資料，以檢視有關擷取率、成功和錯誤的資訊。 如需如何監視資料流的詳細資訊，請參閱以下教學課程： [在UI中監視帳戶和資料流](../monitor.md).

## 刪除您的資料流

您可以刪除不再必要或已使用建立錯誤的資料流 **[!UICONTROL 刪除]** 函式位於 **[!UICONTROL 資料流]** 工作區。 如需如何刪除資料流的詳細資訊，請參閱以下教學課程： [在UI中刪除資料流](../delete.md).

## 后续步骤

依照本教學課程所述，您已成功建立資料流，將電子商務來源的資料匯入Platform。 傳入資料現在可供下游使用 [!DNL Platform] 服務，例如 [!DNL Real-Time Customer Profile] 和 [!DNL Data Science Workspace]. 如需更多詳細資訊，請參閱下列檔案：

* [[!DNL Real-Time Customer Profile] 概述](../../../../profile/home.md)
* [[!DNL Data Science Workspace] 概述](../../../../data-science-workspace/home.md)


>[!WARNING]
>
> 以下影片中顯示的Platform UI已過期。 請參閱上述檔案，瞭解最新的UI熒幕擷取畫面及功能。
>
>[!VIDEO](https://video.tv.adobe.com/v/29711?quality=12&learn=on)


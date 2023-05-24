---
keywords: Experience Platform；首頁；熱門主題；資料流；資料流
title: 設定資料流以從UI中的雲端儲存空間來源擷取批次資料
description: 本教學課程提供如何設定新資料流的步驟，以便從UI中的雲端儲存空間來源擷取批次資料
exl-id: b327bbea-039d-4c04-afd3-f1d6a5f902a6
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 0%

---

# 設定資料流以從UI中的雲端儲存空間來源擷取批次資料

本教學課程提供如何設定資料流的步驟，以將雲端儲存空間來源的批次資料引進Adobe Experience Platform。

## 快速入门

>[!NOTE]
>
>為了建立資料流以從雲端儲存空間帶入批次資料，您必須已經擁有對已驗證的雲端儲存空間來源的存取權。 如果您沒有存取權，請前往 [來源概觀](../../../../home.md#cloud-storage) 以取得您可以用來建立帳戶的雲端儲存空間來源清單。

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

### 支持的文件格式

批次資料的雲端儲存空間來源支援下列檔案格式以供擷取：

* 分隔符號分隔值(DSV)：任何單一字元值都可作為DSV格式資料檔案的分隔符號。
* [!DNL JavaScript Object Notation] (JSON)： JSON格式的資料檔案必須符合XDM規範。
* [!DNL Apache Parquet]：Parquet格式資料檔案必須符合XDM標準。
* 壓縮檔案：JSON和分隔檔案可壓縮為： `bzip2`， `gzip`， `deflate`， `zipDeflate`， `tarGzip`、和 `tar`.

## 新增資料

建立雲端儲存空間帳戶後， **[!UICONTROL 新增資料]** 步驟隨即顯示，為您提供瀏覽雲端儲存空間檔案階層並選取您要帶至Platform的資料夾或特定檔案的介面。

* 介面的左側是目錄瀏覽器，顯示您的雲端儲存空間檔案階層。
* 介面的右側部分可讓您從相容的資料夾或檔案預覽最多100列資料。

![](../../../../images/tutorials/dataflow/cloud-batch/select-data.png)

選取根資料夾以存取您的資料夾階層。 從這裡，您可以選取單一資料夾，以遞回方式擷取資料夾中的所有檔案。 擷取整個資料夾時，您必須確保該資料夾中的所有檔案都共用相同的資料格式和結構描述。

![](../../../../images/tutorials/dataflow/cloud-batch/folder-directory.png)

選取資料夾後，正確的介面會更新為所選資料夾中第一個檔案的內容和結構預覽。

![](../../../../images/tutorials/dataflow/cloud-batch/select-folder.png)

在此步驟中，您可以對資料進行數個設定，然後再繼續。 首先，選取 **[!UICONTROL 資料格式]** 然後在出現的下拉式面板中，為您的檔案選取適當的資料格式。

下表顯示支援的檔案型別適用的資料格式：

| 檔案型別 | 資料格式 |
| --- | --- |
| CSV | [!UICONTROL 已分隔] |
| JSON | [!UICONTROL JSON] |
| Parquet | [!UICONTROL XDM Parquet] |

![](../../../../images/tutorials/dataflow/cloud-batch/data-format.png)

### 選取欄分隔符號

設定資料格式後，您可以在擷取分隔檔案時設定欄分隔符號。 選取 **[!UICONTROL 分隔符號]** 選項，然後從下拉式選單中選取分隔符號。 功能表會顯示分隔字元最常使用的選項，包括逗號(`,`)，索引標籤(`\t`)和垂直號(`|`)。

![](../../../../images/tutorials/dataflow/cloud-batch/delimiter.png)

如果您偏好使用自訂分隔字元，請選取 **[!UICONTROL 自訂]** 並在快顯視窗輸入列中輸入您選擇的單一字元分隔字元。

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

### 擷取壓縮檔案

您也可以指定壓縮JSON或分隔檔案的壓縮型別，藉此擷取壓縮檔案。

在 [!UICONTROL 選取資料] 步驟，選取要擷取的壓縮檔案，然後選取其適當的檔案型別以及是否符合XDM規範。 接下來，選取 **[!UICONTROL 壓縮型別]** 然後為您的來源資料選取適當的壓縮檔案型別。

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

若要將特定檔案帶入Platform，請選取資料夾，然後選取您要擷取的檔案。 在此步驟中，您也可以使用檔案名稱旁邊的預覽圖示來預覽指定資料夾內其他檔案的檔案內容。

完成後，選取 **[!UICONTROL 下一個]**.

![](../../../../images/tutorials/dataflow/cloud-batch/select-file.png)

## 提供資料流詳細資料

此 [!UICONTROL 資料流詳細資料] 頁面可讓您選取要使用現有資料集還是新資料集。 在此過程中，您也可以設定要擷取至設定檔的資料，並啟用以下設定 [!UICONTROL 錯誤診斷]， [!UICONTROL 部分擷取]、和 [!UICONTROL 警報].

![](../../../../images/tutorials/dataflow/cloud-batch/dataflow-detail.png)

### 使用現有的資料集

若要將資料內嵌至現有資料集，請選取「 」 **[!UICONTROL 現有資料集]**. 您可以使用來擷取現有的資料集 [!UICONTROL 進階搜尋] 選項，或是透過在下拉式選單中捲動現有資料集清單的方式。 選取資料集後，請為資料流提供名稱和說明。

![](../../../../images/tutorials/dataflow/cloud-batch/existing.png)

### 使用新資料集

若要內嵌至新資料集，請選取「 」 **[!UICONTROL 新資料集]** 然後提供輸出資料集名稱和選擇性說明。 接下來，使用 [!UICONTROL 進階搜尋] 選項或透過捲動下拉式選單中的現有結構描述清單的方式。 選取結構描述後，請為資料流提供名稱和說明。

![](../../../../images/tutorials/dataflow/cloud-batch/new.png)

### 啟用設定檔和錯誤診斷

接下來，選取 **[!UICONTROL 設定檔資料集]** 切換即可為設定檔啟用資料集。 這可讓您建立實體屬性和行為的整體檢視。 來自所有已啟用設定檔的資料集的資料將包含在設定檔中，當您儲存資料流時，將會套用變更。

[!UICONTROL 錯誤診斷] 針對資料流中發生的任何錯誤記錄，啟用詳細的錯誤訊息產生，同時 [!UICONTROL 部分擷取] 可讓您擷取包含錯誤的資料，最多可擷取您手動定義的特定臨界值。 請參閱 [部分批次擷取概觀](../../../../../ingestion/batch-ingestion/partial.md) 以取得詳細資訊。

![](../../../../images/tutorials/dataflow/cloud-batch/ingestion-configs.png)

### 啟用警示

您可以啟用警報以接收有關資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱來源警報](../../alerts.md).

當您完成提供詳細資訊給資料流時，請選取「 」 **[!UICONTROL 下一個]**.

![](../../../../images/tutorials/dataflow/cloud-batch/alerts.png)

## 將資料欄位對應至XDM結構描述

此 [!UICONTROL 對應] 步驟隨即顯示，為您提供介面，用於將來源結構描述中的來源欄位對應到目標結構描述中適當的目標XDM欄位。

Platform會根據您選取的目標結構描述或資料集，為自動對應的欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。 您可以視需要選擇直接對應欄位，或使用資料準備函式來轉換來源資料，以衍生計算值或計算值。 如需使用對應程式介面和計算欄位的完整步驟，請參閱 [資料準備UI指南](../../../../../data-prep/ui/mapping.md).

成功對應來源資料後，請選取 **[!UICONTROL 下一個]**.

![](../../../../images/tutorials/dataflow/cloud-batch/mapping.png)

## 排程內嵌執行

>[!IMPORTANT]
>
>強烈建議您在使用時，排程資料流進行一次性擷取 [FTP來源](../../../../connectors/cloud-storage/ftp.md).

此 [!UICONTROL 排程] 步驟隨即顯示，可讓您設定擷取排程，以使用已設定的對應自動擷取選取的來源資料。 根據預設，排程設定為 `Once`. 若要調整您的擷取頻率，請選取 **[!UICONTROL 頻率]** ，然後從下拉式選單中選取選項。

>[!TIP]
>
>間隔和回填在一次性內嵌期間不可見。

![排程](../../../../images/tutorials/dataflow/cloud-batch/scheduling.png)

如果您將擷取頻率設為 `Minute`， `Hour`， `Day`，或 `Week`，則必須設定間隔，以建立每次擷取之間所設定的時間範圍。 例如，擷取頻率設為 `Day` 而間隔設定為 `15` 表示您的資料流已排程每15天擷取一次資料。

在此步驟中，您也可以啟用 **回填** 和定義資料增量擷取的欄。 回填是用來擷取歷史資料，而您為增量擷取定義的欄則允許將新資料與現有資料區分開來。

請參閱下表以取得排程設定的詳細資訊。

| 字段 | 描述 |
| --- | --- |
| 频度 | 內嵌發生的頻率。 可選擇頻率包括 `Once`， `Minute`， `Hour`， `Day`、和 `Week`. |
| 間隔 | 設定所選頻率間隔的整數。 間隔值應為非零整數，且應設定為大於或等於15。 |
| 開始時間 | UTC時間戳記，指出第一次內嵌設定於何時發生。 開始時間必須大於或等於您目前的UTC時間。 |
| 回填 | 布林值，決定最初擷取的資料。 如果已啟用回填，則在第一次排程的擷取期間，將會擷取指定路徑中的所有目前檔案。 如果停用回填，則只會擷取在第一次執行擷取和開始時間之間載入的檔案。 將不會擷取在開始時間之前載入的檔案。 |

>[!NOTE]
>
>對於批次擷取，每個後續的資料流都會根據其 **上次修改時間** 時間戳記。 這表示批次資料流會從來源選取新的檔案，或自上次資料流執行以來修改的檔案。 此外，您必須確保檔案上傳與已排程的流程執行之間有足夠的時間跨度，因為在已排程的流程執行時間之前未完全上傳至雲端儲存體帳戶的檔案可能無法擷取以進行內嵌。

完成擷取排程的設定後，選取「 」 **[!UICONTROL 下一個]**.

![](../../../../images/tutorials/dataflow/cloud-batch/scheduling-configs.png)

## 檢閱您的資料流

此 **[!UICONTROL 檢閱]** 步驟隨即顯示，可讓您在建立新資料流之前對其進行檢閱。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **[!UICONTROL 指派資料集和對應欄位]**：顯示要將來源資料擷取到哪個資料集中，包括資料集所堅持的結構描述。
* **[!UICONTROL 排程]**：顯示內嵌排程的作用中期間、頻率和間隔。

檢閱資料流後，請按一下 **[!UICONTROL 完成]** 並留出一些時間來建立資料流。

![](../../../../images/tutorials/dataflow/cloud-batch/review.png)


## 后续步骤

依照本教學課程所述，您已成功建立資料流以從外部雲端儲存空間匯入資料，並深入瞭解監控資料集。 若要進一步瞭解如何建立資料流，您可以觀看下方的影片，以補充學習內容。 此外，下游現在可以使用傳入的資料 [!DNL Platform] 服務，例如 [!DNL Real-Time Customer Profile] 和 [!DNL Data Science Workspace]. 如需更多詳細資訊，請參閱下列檔案：

* [[!DNL Real-Time Customer Profile] 概述](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] 概述](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> 此 [!DNL Platform] 以下影片中顯示的UI已過期。 請參閱上述檔案，瞭解最新的UI熒幕擷取畫面及功能。

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## 附录

以下小節提供使用來源聯結器的其他資訊。

## 監視資料流

建立資料流後，您可以監視透過它擷取的資料，以檢視擷取率、成功和錯誤的資訊。 如需如何監視資料流的詳細資訊，請瀏覽上的教學課程 [在UI中監視帳戶和資料流](../../monitor.md).

## 更新您的資料流

若要更新資料流排程、對應和一般資訊的設定，請瀏覽上的教學課程 [在UI中更新來源資料流程](../../update-dataflows.md)

## 刪除您的資料流

您可以刪除不再必要或已使用建立錯誤的資料流 **[!UICONTROL 刪除]** 函式位於 **[!UICONTROL 資料流]** 工作區。 如需如何刪除資料流的詳細資訊，請造訪上的教學課程 [在UI中刪除資料流](../../delete.md).
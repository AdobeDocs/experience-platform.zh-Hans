---
title: 使用AI產生的Recommendations將CSV檔案對應到XDM結構描述
description: 本教學課程涵蓋如何使用AI產生的建議將CSV檔案對應到XDM結構描述。
exl-id: 1daedf0b-5a25-4ca5-ae5d-e9ee1eae9e4d
source-git-commit: df6f76be6beba962b1795bd33dc753ef04267734
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 1%

---

# 使用AI產生的建議將CSV檔案對應到XDM結構描述

>[!NOTE]
>
>如需Platform中一般可用CSV對應功能的相關資訊，請參閱以下檔案： [將CSV檔案對應到現有結構描述](./existing-schema.md).

為了將CSV資料擷取到 [!DNL Adobe Experience Platform]，資料必須對應至 [!DNL Experience Data Model] (XDM)結構描述。 您可以選擇對應至 [現有結構描述](./existing-schema.md)，但如果您不確定要使用哪個結構描述或應該如何使用結構描述，可以在Platform UI中使用根據機器學習(ML)模型的動態建議。

## 快速入门

本教學課程需要您深入瞭解下列元件 [!DNL Platform]：

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md)：作為依據的標準化架構 [!DNL Platform] 組織客戶體驗資料。
   * 您至少必須瞭解 [XDM中的行為](../../../xdm/home.md#data-behaviors)，以便決定是否將資料對應至 [!UICONTROL 設定檔] 類別（記錄行為）或 [!UICONTROL ExperienceEvent] 類別（時間序列行為）。
* [批次擷取](../../batch-ingestion/overview.md)：用來執行 [!DNL Platform] 從使用者提供的資料檔擷取資料。
* [Adobe Experience Platform資料準備](../../batch-ingestion/overview.md)：功能套件，可讓您對應及轉換所擷取的資料，以符合XDM結構描述。 上的檔案 [資料準備函式](../../../data-prep/functions.md) 與結構描述對應特別相關。

## 提供資料流詳細資料

在Experience PlatformUI中，選取 **[!UICONTROL 來源]** 左側導覽列中。 於 **[!UICONTROL 目錄]** 檢視，導覽至 **[!UICONTROL 本機系統]** 類別。 下 **[!UICONTROL 本機檔案上傳]**，選取 **[!UICONTROL 新增資料]**.

![此 [!UICONTROL 來源] Platform UI中的目錄，使用 [!UICONTROL 新增資料] 在 [!UICONTROL 本機檔案上傳] 已選取。](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

此 **[!UICONTROL 對應CSV XDM結構描述]** 工作流程隨即出現，從 **[!UICONTROL 資料流詳細資料]** 步驟。

選取 **[!UICONTROL 使用ML建議建立新結構描述]**，造成新控制項出現。 選擇您要對應之CSV資料的適當類別([!UICONTROL 設定檔] 或 [!UICONTROL ExperienceEvent])。 您可以選擇使用下拉式選單來選取您企業的相關產業，或如果提供的類別不適用於您，則將其保留空白。 如果您的組織在 [企業對企業(B2B)](../../../xdm/tutorials/relationship-b2b.md) 模型，選取 **[!UICONTROL B2B資料]** 核取方塊。

![此 [!UICONTROL 資料流詳細資料] 選取ML建議選項的步驟。 [!UICONTROL 設定檔] 已為類別選取，並且 [!UICONTROL 電信] 已針對產業選取](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

從這裡，為將從CSV資料建立的結構描述命名，以及包含在該結構描述下擷取之資料的輸出資料集名稱。

您可以選擇在繼續之前，為資料流設定下列附加功能：

| 輸入名稱 | 描述 |
| --- | --- |
| [!UICONTROL 描述] | 資料流的說明。 |
| [!UICONTROL 錯誤診斷] | 啟用後，系統會為新擷取的批次產生錯誤訊息，您可在擷取中對應批次時檢視這些訊息 [API](../../batch-ingestion/api-overview.md). |
| [!UICONTROL 部分擷取] | 啟用後，會在指定的錯誤臨界值內擷取新批次資料的有效記錄。 此臨界值可讓您設定在整個批次失敗之前可接受的錯誤百分比。 |
| [!UICONTROL 数据流详细信息] | 為會將CSV資料帶入Platform的資料流提供名稱和可選描述。 啟動此工作流程時，會自動為資料流指派預設名稱。 變更名稱為選用。 |
| [!UICONTROL 警报] | 從清單中選取 [產品內警示](../../../observability/alerts/overview.md) 啟動資料流後，您想要收到的資料流狀態相關資訊。 |

{style="table-layout:auto"}

完成資料流設定後，選取「 」 **[!UICONTROL 下一個]**.

![此 [!UICONTROL 資料流詳細資料] 區段已完成。](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## 选择数据

於 **[!UICONTROL 選取資料]** 步驟，使用左欄上傳您的CSV檔案。 您可以選取 **[!UICONTROL 選擇檔案]** 開啟檔案總管對話方塊以從中選取檔案，或是直接將檔案拖放到欄中。

![此 [!UICONTROL 選擇檔案] 按鈕和拖放區域(醒目提示於 [!UICONTROL 選取資料] 步驟。](../../images/tutorials/map-csv-recommendations/upload-files.png)

上傳檔案後，會出現範例資料區段，顯示收到的前10列資料，以便您驗證其已正確上傳。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![範例資料列會填入工作區中](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## 設定結構描述對應

ML模型會根據您的資料流設定和您上傳的CSV檔案來執行以產生新結構描述。 當程式完成時， [!UICONTROL 對應] 步驟會填入，以顯示每個個別欄位的對應，以及所產生結構描述結構的完整可導覽檢視。

![此 [!UICONTROL 對應] UI中的步驟，顯示對應的所有CSV欄位以及產生的結構描述結構。](../../images/tutorials/map-csv-recommendations/schema-generated.png)

從這裡，您可以選擇 [編輯欄位對應](#edit-mappings) 或 [變更與其關聯的欄位群組](#edit-schema) 根據您的需求。 滿意後，選取 **[!UICONTROL 完成]** 以完成對應並起始您先前設定的資料流。 CSV資料會內嵌至系統，並根據產生的結構描述結構填入資料集，以備下游平台服務使用。

![此 [!UICONTROL 完成] 按鈕，完成CSV對應程式。](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### 編輯欄位對應 {#edit-mappings}

使用欄位對應預覽來編輯現有對應或完全移除現有對應。 有關如何管理UI中對應集的詳細資訊，請參閱 [資料準備對應的UI指南](../../../data-prep/ui/mapping.md#mapping-interface).

### 編輯欄位群組 {#edit-field-groups}

CSV欄位會使用ML模型自動對應到現有XDM欄位群組。 如果您想要變更任何特定CSV欄位的欄位群組，請選取 **[!UICONTROL 編輯]** 位於結構描述樹狀結構旁邊。

![此 [!UICONTROL 編輯] 在結構描述樹旁邊選取的按鈕。](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

會出現一個對話方塊，讓您編輯對應中任何欄位的顯示名稱、資料型別和欄位群組。 選取編輯圖示(![編輯圖示](../../images/tutorials/map-csv-recommendations/edit-icon.png))來編輯其詳細資訊，然後再選取 **[!UICONTROL 套用]**.

![要變更之來源欄位的建議欄位群組。](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

當您完成調整來源欄位的結構描述建議時，請選取 **[!UICONTROL 儲存]** 以套用變更。

## 后续步骤

本指南說明如何使用AI產生的建議將CSV檔案對應到XDM結構描述，讓您透過批次擷取將該資料帶入Platform。

如需將CSV檔案對應至現有結構的步驟，請參閱 [現有結構描述對應工作流程](./existing-schema.md). 如需透過預先建立的來源連線將資料即時串流至Platform的詳細資訊，請參閱 [來源概觀](../../../sources/home.md).

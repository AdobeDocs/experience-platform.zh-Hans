---
keywords: Experience Platform；首頁；熱門主題；啟用資料集；資料集；資料集
solution: Experience Platform
title: 資料集UI指南
description: 瞭解如何在Adobe Experience Platform使用者介面中使用資料集時執行常見動作。
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 7%

---

# 資料集UI指南

本使用手冊提供在Adobe Experience Platform使用者介面中使用資料集時，執行常見動作的相關指示。

## 快速入门

本使用手冊需要您實際瞭解下列Adobe Experience Platform元件：

* [資料集](overview.md)：資料持續存在的儲存和管理結構 [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器](../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用建置您自己的自訂XDM結構描述 [!DNL Schema Editor] 在 [!DNL Platform] 使用者介面。
* [[!DNL Real-Time Customer Profile]](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md)：確保遵守使用客戶資料的相關法規、限制和政策。

## 檢視資料集 {#view-datasets}

>[!CONTEXTUALHELP]
>id="platform_datasets_negative_numbers"
>title="数据集活动中的负数"
>abstract="摄取的记录中的负数表示用户已删除选定时间范围内的某些批次。"
>text="Learn more in documentation"

在 [!DNL Experience Platform] UI，選取 **[!UICONTROL 資料集]** 在左側導覽中開啟 **[!UICONTROL 資料集]** 儀表板。 儀表板會列出貴組織的所有可用資料集。 会显示每个列出数据集的详细信息，包括其名称、数据集所遵循的架构以及最近摄取运行的状态。

![反白顯示左側導覽列中資料集專案的影像。](../images/datasets/user-guide/browse-datasets.png)

默认情况下，只会显示已摄取到的数据集。如果您想要檢視系統產生的資料集，請啟用 **[!UICONTROL 顯示系統資料集]** 切換。 系統產生的資料集僅用於處理其他元件。 例如，系統產生的設定檔匯出資料集可用來處理設定檔儀表板。

![可讓您選擇是否應顯示系統資料集的切換會反白顯示。](../images/datasets/user-guide/system-datasets.png)

選取要存取其資料集的名稱 **[!UICONTROL 資料集活動]** 畫面並檢視您選取之資料集的詳細資訊。 活动选项卡包含一个图表，其中可查看消息使用率，以及成功批次和失败批次的列表。

![系統會醒目顯示您所選資料集的詳細資料。](../images/datasets/user-guide/dataset-activity-1.png)
![屬於您所選資料集的範例批次會反白顯示。](../images/datasets/user-guide/dataset-activity-2.png)

## 預覽資料集

從 **[!UICONTROL 資料集活動]** 畫面，選取 **[!UICONTROL 預覽資料集]** 靠近熒幕右上角，可預覽最多100列資料。 如果資料集為空，預覽連結將會停用，並改為表示無法預覽。

![預覽資料集按鈕會反白顯示。](../images/datasets/user-guide/select-preview.png)

在預覽視窗中，資料集的結構描述階層檢視會顯示在右側。

![會顯示資料集的預覽。 隨即顯示有關結構的資訊以及範例值。](../images/datasets/user-guide/preview-dataset.png)

如需更穩健的資料存取方法， [!DNL Experience Platform] 提供下游服務，例如 [!DNL Query Service] 和 [!DNL JupyterLab] 以探索及分析資料。 如需詳細資訊，請參閱下列檔案：

* [查詢服務總覽](../../query-service/home.md)
* [JupyterLab使用手冊](../../data-science-workspace/jupyterlab/overview.md)

## 建立資料集 {#create}

要创建新数据集，请首先选择“数据集”仪表板中的&#x200B;**[!UICONTROL 创建数据集]**。****

![建立資料集按鈕會醒目提示。](../images/datasets/user-guide/select-create.png)

在下一個畫面中，畫面會顯示下列兩個建立新資料集的選項：

* [使用模式创建数据集。](#schema)
* [從CSV檔案建立資料集](#csv)

### 使用現有結構描述建立資料集 {#schema}

在 **[!UICONTROL 建立資料集]** 畫面，選取 **[!UICONTROL 從結構描述建立資料集]** 以建立新的空白資料集。

![會醒目顯示「從結構描述建立資料集」按鈕。](../images/datasets/user-guide/create-dataset-schema.png)

此 **[!UICONTROL 選取結構描述]** 步驟隨即顯示。 瀏覽結構描述清單，並選取資料集將遵循的結構描述，然後再選取 **[!UICONTROL 下一個]**.

![隨即顯示結構描述清單。 會醒目顯示將用來建立資料集的結構描述。](../images/datasets/user-guide/select-schema.png)

此 **[!UICONTROL 設定資料集]** 步驟隨即顯示。 為資料集提供名稱和可選說明，然後選取「 」 **[!UICONTROL 完成]** 以建立資料集。

![會插入資料集的設定詳細資料。 這包括資料集名稱和說明等詳細資訊。](../images/datasets/user-guide/configure-dataset-schema.png)

### 使用CSV檔案建立資料集 {#csv}

使用CSV檔案建立資料集時，會建立臨時結構描述，為資料集提供符合所提供CSV檔案的結構。 在 **[!UICONTROL 建立資料集]** 畫面，選取 **[!UICONTROL 從CSV檔案建立資料集]**.

![會醒目顯示「從CSV檔案建立資料集」按鈕。](../images/datasets/user-guide/create-dataset-csv.png)

此 **[!UICONTROL 設定]** 步驟隨即顯示。 為資料集提供名稱和可選說明，然後選取「 」 **[!UICONTROL 下一個]**.

![會插入資料集的設定詳細資料。 這包括資料集名稱和說明等詳細資訊。](../images/datasets/user-guide/configure-dataset-csv.png)

此 **[!UICONTROL 新增資料]** 步驟隨即顯示。 將CSV檔案拖放至熒幕中央或選取「 」，即可上傳CSV檔案 **[!UICONTROL 瀏覽]** 以探索您的檔案目錄。 檔案大小最多可達10GB。 上傳CSV檔案後，選取「 」 **[!UICONTROL 儲存]** 以建立資料集。

>[!NOTE]
>
>CSV欄名稱的開頭必須為英數字元，並且只能包含字母、數字和底線。

![隨即顯示「新增資料」畫面。 上傳資料集CSV檔案的位置會醒目提示。](../images/datasets/user-guide/add-csv-data.png)

## 啟用即時客戶個人檔案的資料集 {#enable-profile}

每個資料集都能夠使用其擷取的資料擴充客戶設定檔。 若要這麼做，資料集所遵守的結構描述必須相容，才能在中使用 [!DNL Real-Time Customer Profile]. 相容的結構描述符合下列要求：

* 結構描述至少指定一個屬性做為身分屬性。
* 結構描述具有定義為主要身分的身分屬性。

如需啟用結構描述的詳細資訊，請參閱 [!DNL Profile]，請參閱 [結構描述編輯器使用手冊](../../xdm/tutorials/create-schema-ui.md).

若要為設定檔啟用資料集，請存取其 **[!UICONTROL 資料集活動]** 畫面並選取 **[!UICONTROL 設定檔]** 切換於 **[!UICONTROL 屬性]** 欄。 啟用後，擷取到資料集中的資料也將用於填入客戶設定檔。

>[!NOTE]
>
>如果資料集已包含資料，且已啟用 [!DNL Profile]，現有資料不會自動由使用 [!DNL Profile]. 為啟用資料集後 [!DNL Profile]，建議您重新內嵌任何現有資料，以貢獻給客戶設定檔。

![資料集詳細資訊頁面會醒目顯示「設定檔」切換按鈕。](../images/datasets/user-guide/enable-dataset-profiles.png)

## 管理和強制執行資料集的資料控管

資料使用標籤可讓您根據套用至該資料的使用原則來分類資料集和欄位。 請參閱 [資料控管概觀](../../data-governance/home.md) 以進一步瞭解標籤，或參閱 [資料使用標籤使用手冊](../../data-governance/labels/overview.md) 以取得如何將標籤套用至資料集的指示。

## 刪除資料集 {#delete}

您可以先存取資料集，刪除資料集 **[!UICONTROL 資料集活動]** 畫面。 然後，選取 **[!UICONTROL 刪除資料集]** 以刪除它。

>[!NOTE]
>
>Adobe應用程式和服務(例如Adobe Analytics、Adobe Audience Manager或 [!DNL Offer Decisioning])無法刪除。

![「刪除資料集」按鈕會在資料集詳細資訊頁面中反白顯示。](../images/datasets/user-guide/delete-dataset.png)

確認方塊隨即出現。 選取 **[!UICONTROL 刪除]** 以確認刪除資料集。

![隨即顯示刪除的確認強制回應視窗，並反白顯示「刪除」按鈕。](../images/datasets/user-guide/confirm-delete.png)

## 刪除啟用設定檔的資料集

如果設定檔已啟用資料集，透過UI刪除該資料集將會從Data Lake、Identity Service和Platform內的設定檔存放區中刪除它。

您可以從中刪除資料集 [!DNL Profile] 使用即時客戶個人檔案API僅儲存（將資料保留在資料湖中）。 如需詳細資訊，請參閱 [設定檔系統作業API端點指南](../../profile/api/profile-system-jobs.md).

## 监测数据提取

在 [!DNL Experience Platform] UI，選取 **[!UICONTROL 監視]** 左側導覽中的。 此 **[!UICONTROL 監視]** 控制面板可讓您檢視批次或串流擷取的傳入資料狀態。 若要檢視個別批次的狀態，請選取 **[!UICONTROL 批次端對端]** 或 **[!UICONTROL 端對端串流]**. 儀表板會列出所有批次或串流擷取執行，包括成功、失敗或仍在進行的作業。 每個清單都提供批次的詳細資訊，包括批次ID、目標資料集的名稱和擷取的記錄數。 如果目標資料集已啟用 [!DNL Profile]，也會顯示內嵌的身分和設定檔記錄數。

![隨即顯示監控批次端對端畫面。 監控與批次對批次都會反白顯示。](../images/datasets/user-guide/batch-listing.png)

您可以對個人進行選取 **[!UICONTROL 批次識別碼]** 存取 **[!UICONTROL 批次總覽]** 儀表板，並檢視批次的詳細資料，包括批次擷取失敗時的錯誤記錄。

![所選批次的詳細資訊隨即顯示。 這包括擷取的記錄數、失敗的記錄數、批次狀態、檔案大小、擷取開始和結束時間、資料集和批次ID、組織ID、資料集名稱和存取資訊。](../images/datasets/user-guide/batch-overview.png)

如果要刪除批次，您可以選取 **[!UICONTROL 刪除批次]** 在儀表板的右上角附近找到。 這麼做也會從批次最初擷取的資料集中移除其記錄。

![「刪除批次」按鈕會在資料集詳細資訊頁面上反白顯示。](../images/datasets/user-guide/delete-batch.png)

## 后续步骤

本使用手冊提供在中處理資料集時執行常見動作的指示。 [!DNL Experience Platform] 使用者介面。 有關執行常見問題的步驟 [!DNL Platform] 涉及資料集的工作流程，請參閱下列教學課程：

* [使用API建立資料集](create.md)
* [使用資料存取API查詢資料集資料](../../data-access/home.md)
* [使用API設定即時客戶個人檔案和身分服務的資料集](../../profile/tutorials/dataset-configuration.md)

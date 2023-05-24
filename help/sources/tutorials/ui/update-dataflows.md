---
keywords: Experience Platform；首頁；熱門主題；更新資料流；編輯排程
description: 本教學課程涵蓋使用「來源」工作區更新資料流排程的步驟，包括其擷取頻率和間隔率。
solution: Experience Platform
title: 更新UI中的來源連線資料流
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---

# 更新UI中的資料流

本教學課程提供您如何使用「來源」工作區更新現有資料流的步驟，包括其排程和對應。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 更新資料流

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 選取 **[!UICONTROL 資料流]** 以檢視現有資料流的清單。

![目錄](../../images/tutorials/update-dataflows/catalog.png)

此 [!UICONTROL 資料流] 頁面包含所有現有資料流的清單，包括關於其對應目標資料集、來源和帳戶名稱的資訊。

若要排序清單，請選取篩選器圖示 ![篩選](../../images/tutorials/update/filter.png) 左上角以使用「排序」面板。

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

排序面板提供所有可用來源的清單。 您可以從清單中選取多個來源，以存取屬於不同來源的資料流篩選選取專案。

選取您要使用的來源，以檢視其現有資料流的清單。 識別您要更新的資料流後，選取省略符號(`...`)時，不會變更資料流名稱。

![edit-source](../../images/tutorials/update-dataflows/edit-source.png)

下拉式選單隨即出現，為您提供更新所選資料流的選項。 從這裡，您可以選擇更新資料流的對應集和擷取排程。 您也可以選取選項，以在監視控制面板中檢查資料流、訂閱警示，以及停用或刪除資料流。

若要更新資料流的資訊，請選取 **[!UICONTROL 更新資料流]**.

![update-dataflow](../../images/tutorials/update-dataflows/update-dataflow.png)

### 新增資料

此 [!UICONTROL 新增資料] 步驟隨即顯示。 選取適當的資料格式以檢閱所選資料的內容，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![add-data](../../images/tutorials/update-dataflows/add-data.png)

### 数据流详细信息

在 [!UICONTROL 資料流詳細資料] 頁面，您可以為資料流提供更新的名稱和說明，並重新設定資料流的錯誤臨界值。 在此步驟中，您也可以設定或修改警示訂閱的設定。

提供更新的值後，請選取 **[!UICONTROL 下一個]**.

![資料流 — 詳細資料](../../images/tutorials/update-dataflows/dataflow-detail.png)

### 映射

>[!NOTE]
>
>下列來源目前不支援編輯對應功能： Adobe Analytics、Adobe Audience Manager、HTTP API以及 [!DNL Marketo Engage].

此 [!UICONTROL 對應] 頁面提供您一個介面，您可以在其中新增和移除與資料流關聯的對應集。

對應介面會顯示資料流的現有對應集，而不是新的建議對應集。 對應更新僅適用於未來排程的資料流執行。 排程進行一次性內嵌的資料流無法更新其對應集。

從這裡，您可以使用對應介面來修改套用至資料流的對應集。 如需如何使用對應介面的完整步驟，請參閱 [資料準備UI指南](../../../data-prep/ui/mapping.md) 以取得詳細資訊。

![對應](../../images/tutorials/update-dataflows/mapping.png)

### 计划

此 [!UICONTROL 排程] 步驟隨即顯示，可讓您更新資料流的擷取排程，並使用更新的對應自動擷取選取的來源資料。

>[!NOTE]
>
>您無法重新排程要進行一次性內嵌的資料流。

![new-schedule](../../images/tutorials/update-dataflows/new-schedule.png)

您也可以使用資料流頁面提供的內嵌更新選項，更新資料流的擷取排程。

從資料流頁面，選取省略符號(`...`)，然後選取「 」 **[!UICONTROL 編輯排程]** 從出現的下拉式功能表中。

![edit-schedule](../../images/tutorials/update-dataflows/edit-schedule.png)

此 **[!UICONTROL 編輯排程]** 對話方塊提供更新資料流擷取頻率和間隔率的選項。 設定更新的頻率和間隔值後，請選取 **[!UICONTROL 儲存]**.

![排程快顯視窗](../../images/tutorials/update-dataflows/schedule-pop-up.png)

### 请查看

此 **[!UICONTROL 檢閱]** 步驟隨即顯示，可讓您在更新資料流之前先檢閱資料流。

檢閱資料流後，選取 **[!UICONTROL 完成]** 並留出一些時間，以便建立具有新對應集的資料流。

![檢閱](../../images/tutorials/update-dataflows/review.png)

## 后续步骤

依照本教學課程，您已成功使用 [!UICONTROL 來源] 工作區以更新資料流的擷取排程和對應集。

如需如何以程式設計方式執行這些操作的步驟，請使用 [!DNL Flow Service] API，請參考以下教學課程： [使用流量服務API更新資料流](../../tutorials/api/update-dataflows.md).

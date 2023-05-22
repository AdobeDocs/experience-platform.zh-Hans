---
title: UI中的草稿資料流
description: 瞭解如何將資料流儲存為草稿，並在稍後使用來源工作區時發佈。
source-git-commit: 5fc433f603c6e83c621df0f4a1d0aa27e18cd582
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# UI中的草稿資料流

將資料流設定為草稿狀態，以儲存未完成的資料擷取工作流程進度。 您可以稍後繼續並完成草擬的資料流。

本檔案提供在Adobe Experience Platform UI中使用來源工作區時，如何儲存資料流的步驟。

## 快速入门

本檔案需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。

## 將資料流儲存為草稿

選取要帶入Platform的資料後，您可以隨時暫停資料流建立進度。

例如，如果您想在資料流詳細資料步驟期間儲存進度，請選取 **[!UICONTROL 另存為草稿]**.

![已選取另存為草稿之來源工作流程的資料流詳細資料步驟。](../../images/tutorials/draft/save-as-draft.png)

儲存草稿後，系統會將您帶往您帳戶的頁面，您可以在其中檢視現有資料流的清單，包括草稿。

![指定帳戶的資料流清單。](../../images/tutorials/draft/draft-dataflow.png)

>[!TIP]
>
>草擬的資料流將不會啟用，其狀態將設為 `draft`.

若要繼續草稿，請選取省略符號(`...`)，然後選取「 」 **[!UICONTROL 更新資料流]**.

>[!NOTE]
>
>如果您的草稿包含排程資訊，則下拉式視窗也會提供您選項 **[!UICONTROL 編輯排程]**.

![已選取更新資料流的下拉式清單視窗。](../../images/tutorials/draft/update-dataflow.png)

### 從來源目錄存取您的草稿

您也可以透過資料流目錄存取草稿資料流。 選取 **[!UICONTROL 資料流]** 以存取資料流目錄。 從這裡，從組織內現有資料流清單中尋找草稿，選取省略符號(`...`)，然後選取「 」 **[!UICONTROL 更新資料流]**.

![指定組織的資料流清單。](../../images/tutorials/draft/catalog-access.png)

## 發佈草稿資料流

您會返回 [!UICONTROL 新增資料] 來源工作流程的步驟，您可以在此重新確認資料的格式，並繼續處理資料流。

在您確認資料的格式、分隔符號和壓縮型別後，請選取 **[!UICONTROL 下一個]** 以繼續進行。

![來源工作流程的新增資料步驟。](../../images/tutorials/draft/select-data.png)

接下來，確認您的資料流詳細資料。 使用資料流詳細資訊介面更新圍繞資料流名稱、說明、部分擷取、錯誤診斷設定和警報偏好設定的設定。

完成設定後，請選取 **[!UICONTROL 下一個]** 以繼續進行。

![來源工作流程的資料流詳細資料步驟。](../../images/tutorials/draft/dataflow-detail.png)

此 [!UICONTROL 對應] 步驟隨即顯示。 在此步驟中，您可以重新設定資料流的對應設定。 如需用於對應的資料準備功能的完整指南，請造訪 [資料準備UI指南](../../../data-prep/ui/mapping.md).

完成對應重新設定之後，請選取 **[!UICONTROL 下一個]** 以繼續進行。

![來源工作流程的對應步驟。](../../images/tutorials/draft/mapping.png)

使用 [!UICONTROL 排程] 為資料流建立擷取排程的步驟。 您可以將擷取頻率設為 `once`， `minute`， `hour`， `day`，或 `week`. 完成後，選取 **[!UICONTROL 下一個]** 以繼續進行。

![來源工作流程的排程步驟。](../../images/tutorials/draft/scheduling.png)

最後，檢閱資料流的詳細資訊，然後選取 **[!UICONTROL 完成]** 以發佈您的草稿。

![來源工作流程的稽核步驟。](../../images/tutorials/draft/review.png)

儲存並發佈草稿後，將會啟用資料流，您將無法再將其重設為草稿。

## 后续步骤

依照本教學課程，您已瞭解如何儲存進度並將資料流設定為草稿。 如需來源的詳細資訊，請瀏覽 [來源概觀](../../home.md).
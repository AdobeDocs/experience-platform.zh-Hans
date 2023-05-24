---
keywords: 刪除目的地、如何刪除目的地、刪除目的地
title: 刪除目的地
type: Tutorial
description: 本教學課程列出刪除Adobe Experience Platform UI中現有目的地的步驟
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: 1ef6430b6661a2b8b5aef196b75cfaf3f6220aab
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# 刪除目的地 {#delete-destinations}

## 概述 {#overview}

在Adobe Experience Platform使用者介面中，您可以刪除與目的地的現有連線。

刪除目的地會移除該目的地的所有現有資料流。 在刪除資料流之前，系統會取消對應在您刪除之目的地啟用的所有區段。

您可透過下列兩種方式刪除目的地： [!DNL Platform] [!DNL UI]. 您可以：

* [從刪除目的地 [!UICONTROL 瀏覽] 標籤](#delete-browse-tab)
* [從目的地詳細資訊頁面刪除目的地](#delete-destination-details-page)

## 從「瀏覽」索引標籤刪除目的地{#delete-browse-tab}

請依照下列步驟，從 [!UICONTROL 瀏覽] 標籤。

1. 登入 [EXPERIENCE PLATFORMUI](https://platform.adobe.com/) 並選取 **[!UICONTROL 目的地]** 左側導覽列中的。 若要檢視您現有的目的地，請選取 **[!UICONTROL 瀏覽]** 從頂端標題。

   ![瀏覽目的地](../assets/ui/delete-destinations/browse-destinations.png)

2. 選取篩選圖示 ![篩選圖示](../assets/ui/delete-destinations/filter.png) 以啟動「排序」面板。 排序面板會提供您所有目的地的清單。 您可以從清單中選取多個目的地，以檢視與所選目的地相關聯的資料流篩選選取專案。

   ![篩選目的地](../assets/ui/delete-destinations/filter-destinations.png)

3. 選取 ![「更多」按鈕](../assets/ui/delete-destinations/more-icon.png) 按鈕，然後選取 ![刪除按鈕](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL 刪除]** 以移除現有的目的地連線。
   ![刪除目的地](../assets/ui/delete-destinations/delete-destinations.png)

4. 選取 **[!UICONTROL 刪除]** 以確認移除目的地連線。

   ![確認刪除目的地](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## 從目的地詳細資訊頁面刪除目的地{#delete-destination-details-page}

請依照下列步驟，從目的地詳細資訊頁面中刪除目的地。

1. 登入 [EXPERIENCE PLATFORMUI](https://platform.adobe.com/) 並選取 **[!UICONTROL 目的地]** 左側導覽列中的。 若要檢視您現有的目的地，請選取 **[!UICONTROL 瀏覽]** 從頂端標題。

   ![瀏覽目的地](../assets/ui/delete-destinations/browse-destinations.png)

2. 選取篩選圖示 ![篩選圖示](../assets/ui/delete-destinations/filter.png) 以啟動「排序」面板。 排序面板會提供您所有目的地的清單。 您可以從清單中選取多個目的地，以檢視與所選目的地相關聯的資料流篩選選取專案。

   ![篩選目的地](../assets/ui/delete-destinations/filter-destinations.png)

3. 選取您要刪除的目的地名稱。

   ![選取目的地](../assets/ui/delete-destinations/delete-destination-select.png)

   * 如果目的地有現有的資料流，您會被帶到 [!UICONTROL 資料流執行] 標籤。

      ![資料流執行標籤](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * 如果目的地沒有現有的資料流，您會進入一個空白頁面，您可以在該頁面開始啟用對象。

      ![目的地詳細資料](../assets/ui/delete-destinations/destination-details-empty.png)

4. 選取 **[!UICONTROL 刪除]** 在右側邊欄中。

   ![刪除目的地](../assets/ui/delete-destinations/delete-destinations-button.png)

5. 選取 **[!UICONTROL 刪除]** 在確認對話方塊中移除目的地。

   ![刪除目的地確認](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >視伺服器負載而定，可能需要幾分鐘的時間 [!DNL Platform] 以刪除目的地。

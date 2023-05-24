---
keywords: Experience Platform；設定檔；即時客戶設定檔；使用者介面；UI；自訂；設定檔詳細資料；詳細資料
title: UI中的設定檔詳細資料自訂
description: 本指南逐步說明如何自訂Adobe Experience Platform UI中即時客戶設定檔資料的顯示方式。
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] 詳細資料自訂 {#profile-detail-customization}

在Adobe Experience Platform使用者介面中，您可以檢視並與互動 [!DNL Real-Time Customer Profile] 客戶設定檔形式的資料。 UI中顯示的設定檔資訊已從多個設定檔片段合併在一起，以形成每個個別客戶的單一檢視。 這包括基本屬性、連結的身分和管道偏好設定等詳細資訊。 設定檔中顯示的預設欄位也可以在組織層級變更以顯示偏好設定 [!DNL Profile] 屬性。 本指南提供逐步指示，說明自訂的方式 [!DNL Profile] 資料會顯示在Platform UI中。

如需設定檔UI的完整指南，請造訪 [設定檔UI指南](user-guide.md).

## 重新排序卡片並調整其大小 {#reorder-and-resize-cards}

從 **[!UICONTROL 詳細資訊]** 客戶設定檔的標籤中，您可以選取 **[!UICONTROL 自訂設定檔詳細資料]** 以調整現有卡片大小及重新排序。

![「自訂設定檔詳細資料」按鈕會醒目提示在「設定檔」控制面板上。](../images/profile-customization/customize-profile-details.png)

選擇修改控制面板後，您可以選取卡片標題並將卡片拖放至所需順序來重新排序卡片。 您也可以選取卡片右下角的角度符號(`⌟`)並將卡片拖曳至所需大小。 在此範例中， **[!UICONTROL 基本屬性]** 正在調整卡片大小。

![調整大小按鈕會在基本屬性卡中反白顯示。](../images/profile-customization/resize.png)

選取的卡片會調整至所需的大小，而周圍的卡片會動態重新定位。 這可能會導致某些卡片移動到其他列，需要您向下捲動才能看到所有卡片。 例如，當「[!UICONTROL 基本屬性]「卡片大小已調整為」[!UICONTROL 連結的身分]「卡片不再顯示在頂端列，現在顯示在設定檔內的新第二列（未顯示）。 傳回&quot;[!UICONTROL 連結的身分]「卡片拖放至頂列，您可將其拖放至「 」的目前位置[!UICONTROL 頻道偏好設定]「卡片。

![重新調整大小的卡片會反白顯示。](../images/profile-customization/resized.png)

## 編輯和移除卡片

除了調整卡片大小和重新排序卡片外，您還可以編輯特定卡片的內容，並從控制面板中完全移除某些卡片。 選取省略符號(`...`)以編輯或移除卡片。 這會開啟一個下拉式清單，內含編輯或移除卡片的選項，視所選卡片的屬性而定。

>[!NOTE]
>
>並非所有卡片都可以編輯或移除。 這是因為有些卡片包含唯讀或必要資訊。 如果卡片右上角沒有橢圓，則包含唯讀的AND必要資訊，無法編輯或移除。 如果卡片角落有橢圓，並選取它只會顯示移除卡片的選項，則卡片資訊為唯讀且無法編輯。

![編輯卡片下拉式清單會反白顯示。 這包括編輯或移除卡片的選項。](../images/profile-customization/edit-card.png)

選取 **[!UICONTROL 編輯]** 在下拉式清單中開啟 **[!UICONTROL 編輯Widget]** 工作區，您可以在其中更新卡片標題、重新排序或移除可見屬性，或使用 **[!UICONTROL 新增屬性]** 按鈕。

![隨即顯示「基本屬性」卡片。](../images/profile-customization/basic-attributes.png)

## 新增屬性 {#add-attributes}

從 **[!UICONTROL 編輯Widget]** 畫面，選取 **[!UICONTROL 新增屬性]** 以開始向該卡片新增屬性。

![「基本屬性」卡片中的「新增屬性」按鈕會反白顯示。](../images/profile-customization/add-attributes.png)

當 **[!UICONTROL 選取聯合結構描述欄位]** 對話方塊開啟，對話方塊的左側顯示完整的 [!UICONTROL XDM個別設定檔] 聯合結構描述，其欄位巢狀於下方。 如需聯合結構描述的詳細資訊，請參閱 [聯合結構描述區段 [!DNL Profile] 使用手冊](user-guide.md#union-schema).

此 **[!UICONTROL 選取的屬性]** 對話方塊右側的區段會顯示目前包含在您編輯的卡片中的屬性。 您也可以在此移除和重新排序屬性。 畫面會顯示選取的屬性總數，以及可新增至單一卡片的屬性數目上限(20)。

![目前構成卡片上的屬性的屬性會反白顯示。](../images/profile-customization/select-before.png)

您可以選取任何可用的聯合結構描述欄位，以自訂您正在編輯的卡片上的屬性。 選取的欄位旁邊會顯示勾號，並會自動新增至選取的屬性清單中。 新增您要顯示在卡片上的所有屬性後，請選擇 **[!UICONTROL 選取]** 以返回 **[!UICONTROL 編輯Widget]** 畫面。

![新加入的屬性會反白顯示。](../images/profile-customization/select-after.png)

當您返回 **[!UICONTROL 編輯Widget]** 熒幕上，現在應更新卡片上的屬性清單以反映您的選擇。 您仍然可以根據需要移除或重新排序卡片屬性或編輯卡片標題。 編輯完成後，選取 **[!UICONTROL 儲存]** 以儲存變更。

![新新增的屬性會顯示在編輯的卡片上。](../images/profile-customization/new-attributes.png)

儲存後，您會返回 **[!UICONTROL 詳細資訊]** 顯示更新卡片和屬性的標籤。

![新新增的屬性會顯示在「設定檔」控制面板的卡片上。](../images/profile-customization/added-attributes.png)

## 新增卡片 {#add-a-new-card}

若要進一步自訂Experience Platform中設定檔的外觀，您可以選取將新卡片新增至控制面板，並選取您想在這些卡片顯示的屬性。 若要開始，請選取 **[!UICONTROL 修改儀表板]** 於 **[!UICONTROL 詳細資訊]** 標籤。

![自訂設定檔詳細資訊按鈕會醒目提示。](../images/profile-customization/customize-profile-details.png)

接下來，選取 **[!UICONTROL 新增Widget]** 圖示板的左上角。

![「新增Widget」按鈕會反白顯示。](../images/profile-customization/add-widget.png)

選擇新增卡片會開啟 **[!UICONTROL 編輯Widget]** 此畫面可讓您為新卡片提供標題，並選擇您希望卡片顯示的屬性。 若要開始將屬性新增至卡片，請選取 **[!UICONTROL 新增屬性]**.

![「編輯Widget」畫面中會顯示空白的新Widget卡。](../images/profile-customization/edit-widget.png)

當 **[!UICONTROL 選取聯合結構描述欄位]** 對話方塊開啟，對話方塊的左側顯示完整的 [!UICONTROL XDM個別設定檔] 聯合結構描述和 **[!UICONTROL 選取的屬性]** 對話方塊右側的區段會顯示您為卡片選取的屬性。 如需新增屬性的詳細資訊，請參閱 [新增屬性的區段](#add-attributes) 即會出現在此檔案的前面。

畫面會顯示選取的屬性總數，以及可新增至單一卡片的屬性數目上限(20)。 您也可以從此畫面移除並重新排序您選取的屬性。 新增您要顯示在卡片上的所有屬性後，請選擇 **[!UICONTROL 選取]** 以返回 **[!UICONTROL 編輯Widget]** 畫面。

![您新增至卡片的欄位會反白顯示。](../images/profile-customization/add-widget-attributes.png)

當您返回 **[!UICONTROL 編輯Widget]** 熒幕上，卡片上的屬性清單應該會反映您在上一個熒幕所做的選擇。 您也可以視需要重新排序及移除卡片屬性。

若要儲存新卡片，您必須先提供 **[!UICONTROL 卡片標題]**，然後您便能夠選取 **[!UICONTROL 儲存]** 並完成卡片建立程式。

![新的Widget會在「編輯Widget」畫面中預覽。](../images/profile-customization/new-widget.png)

儲存後，您會返回 **[!UICONTROL 詳細資訊]** 顯示新卡片和屬性的索引標籤。

![新的Widget會新增至「設定檔」儀表板。](../images/profile-customization/added-widget.png)

## 還原預設卡片

如果在任何時候您決定要恢復已移除的預設卡片，您就可以快速輕鬆地這樣做。 首先，選取 **[!UICONTROL 修改儀表板]**，然後選取 **[!UICONTROL 還原預設卡片]**. 顯示預設卡片後，您可以選取 **[!UICONTROL 儲存]** 儲存變更或選取 **[!UICONTROL 取消]** 如果您不想還原預設卡片。

![「設定檔」儀表板中會反白顯示「還原預設卡片」按鈕。](../images/profile-customization/restore-default.png)

## 后续步骤

依照此檔案，您現在應該能夠更新您組織的設定檔檢視，包括新增和移除卡片、編輯卡片詳細資訊和屬性，以及重新排序卡片並重新調整卡片大小。 若要進一步瞭解使用 [!DNL Profile] Experience PlatformUI中的資料，請參閱 [[!DNL Profile] 使用手冊](user-guide.md).

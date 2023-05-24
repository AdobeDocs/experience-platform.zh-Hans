---
keywords: Experience Platform；首頁；熱門主題；分析；分類
description: 瞭解如何在UI中建立Adobe Analytics來源聯結器，以將分類資料帶入Adobe Experience Platform。
solution: Experience Platform
title: 在UI中建立分類資料的Adobe Analytics來源連線
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: f619bbf2c8d313eabc6444b4bd8c09615a00cc42
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 6%

---

# 在UI中建立分類資料的Adobe Analytics來源連線

本教學課程提供在UI中建立Adobe Analytics分類資料來源連線的步驟，以將分類資料帶入Adobe Experience Platform。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

Analytics Classifications Data Connector需要將您的資料移轉至新的 [!DNL Classifications] 使用前的Adobe Analytics基礎結構。 若要確認資料的移轉狀態，請聯絡您的Adobe客戶團隊。

## 選取您的分類

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 從左側導覽列存取「來源」工作區。 此 **[!UICONTROL 目錄]** 畫面會顯示用來建立輸入連線的可用來源。 每個來源卡片都會顯示選項，讓您設定新帳戶或新增資料至現有帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 **[!UICONTROL Adobe應用程式]** 類別，選取 **[!UICONTROL Adobe Analytics]** 卡片，然後選取 **[!UICONTROL 新增資料]** 以開始使用Analytics分類資料。

![](../../../../images/tutorials/create/classifications/catalog.png)

此 **[!UICONTROL Analytics來源新增資料]** 步驟隨即顯示。 選取 **[!UICONTROL 分類]** 從頂端標題檢視 [!DNL Classifications] 資料集，包括其維度ID、報表套裝名稱和報表套裝ID的相關資訊。

每個頁面最多可顯示10個不同的專案 [!DNL Classifications] 資料集供您選擇。 選取 **[!UICONTROL 下一個]** 頁面底部以瀏覽更多選項。 右邊的面板會顯示 [!DNL Classifications] 您所選取的資料集及其名稱。 此面板也可讓您移除任何 [!DNL Classifications] 您可能不小心選取了資料集，或只執行一個動作就清除所有選取專案。

您最多可以選取30種不同的方式 [!DNL Classifications] 要帶入的資料集 [!DNL Platform].

一旦您選取 [!DNL Classifications] 資料集，選取 **[!UICONTROL 下一個]** 頁面右上角。

![](../../../../images/tutorials/create/classifications/add-data.png)

## 檢閱您的分類

此 **[!UICONTROL 檢閱]** 步驟隨即顯示，讓您檢閱選取的專案 [!DNL Classifications] 建立資料集之前的資料。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示來源平台和連線狀態。
* **[!UICONTROL 資料型別]**：顯示已選取的數量 [!DNL Classifications].
* **[!UICONTROL 排程]**：顯示同步化的頻率 [!DNL Classifications] 資料。

檢閱資料流後，請按一下 **[!UICONTROL 完成]** 並留出一些時間來建立資料流。

![](../../../../images/tutorials/create/classifications/review.png)

## 監視您的分類資料流

建立資料流後，您可以監視透過該資料流擷取的資料。 從 **[!UICONTROL 目錄]** 畫面，選取 **[!UICONTROL 資料流]** 若要檢視與您建立關聯的已建立流程清單，請 [!DNL Classifications] 帳戶。

![](../../../../images/tutorials/create/classifications/dataflows.png)

此 **[!UICONTROL 資料流]** 畫面隨即顯示。 此頁面提供資料流清單，包含其名稱、來源資料和資料流執行狀態的資訊。 在右邊，是 **[!UICONTROL 屬性]** 包含中繼資料的面板 [!DNL Classifications] 資料流。

選取 **[!UICONTROL 目標資料集]** 您希望存取。

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

此 **[!UICONTROL 資料集活動]** 頁面會顯示您所選取目標資料集的資訊，包括其批次狀態、資料集ID和結構描述的詳細資訊。

>[!IMPORTANT]
>
>尽管其他源连接器可以删除数据集，但目前不支持 Analytics Classifications Data Connector 这样做。如果您误删除了一个数据集，请联系 Adobe 客户关怀部门。

![](../../../../images/tutorials/create/classifications/dataset.png)


## 后续步骤

依照本教學課程所述，您已建立Analytics Classifications Data Connector，可提供 [!DNL Classifications] 資料匯入 [!DNL Platform]. 請參閱下列檔案，瞭解更多關於 [!DNL Analytics] 和 [!DNL Classifications] 資料：

* [Analytics Data Connector概述](../../../../connectors/adobe-applications/analytics.md)
* [在使用者介面中建立Analytics資料連線](./analytics.md)
* [关于分类](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)

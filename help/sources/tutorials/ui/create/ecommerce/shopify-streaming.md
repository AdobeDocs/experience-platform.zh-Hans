---
title: 在UI中建立Shopify串流連線和資料流
description: 瞭解如何使用Platform使用者介面建立Shopify串流來源連線和資料流
badge: Beta
exl-id: 3368ecf6-0c61-49ce-bc9c-29ee50b3f037
source-git-commit: feb05d5bddc4135c5fe14d3ec5d8fad62c5e2236
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 1%

---

# 為以下專案建立來源連線和資料流： [!DNL Shopify Streaming] 使用UI的資料

本教學課程提供建立 [!DNL Shopify Streaming] 使用Platform使用者介面的來源連線和資料流。

## 快速入门 {#getting-started}

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

>[!IMPORTANT]
>
>本教學課程需要您完成先決條件設定，才能使用 [!DNL Shopify Streaming] 帳戶。 如需設定帳戶的步驟，請閱讀 [[!DNL Shopify Streaming] 概觀](../../../../connectors/ecommerce/shopify-streaming.md).

## 連線您的 [!DNL Shopify Streaming] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 以存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 **電子商務** 類別，選取 [!DNL Shopify Streaming]，然後選取 **[!UICONTROL 新增資料]**.

![Experience Platform來源目錄](../../../../images/tutorials/create/shopify-streaming/catalog.png)

## 选择数据

此 **[!UICONTROL 選取資料]** 步驟隨即顯示，提供介面供您選取要帶至Platform的資料。

* 介面的左側是瀏覽器，可讓您檢視帳戶內的可用資料流；
* 介面的右側部分可讓您預覽來自JSON檔案的最多100列資料。

選取 **[!UICONTROL 上傳檔案]** 以從您的本機系統上傳JSON檔案。 或者，您也可以將要上傳的JSON檔案拖放至 [!UICONTROL 拖放檔案] 面板。

![來源工作流程的新增資料步驟。](../../../../images/tutorials/create/shopify-streaming/select-data.png)

上傳檔案後，預覽介面會更新，以顯示您上傳的結構描述預覽。 預覽介面可讓您檢查檔案的內容和結構。 您也可以使用 [!UICONTROL 搜尋欄位] 用於從結構描述中存取特定專案的公用程式。

完成後，選取 **[!UICONTROL 下一個]**.

![來源工作流程的預覽步驟。](../../../../images/tutorials/create/shopify-streaming/preview.png)

## 数据流详细信息

此 **資料流詳細資料** 步驟隨即顯示，為您提供使用現有資料集或為資料流建立新資料集的選項，以及提供資料流名稱和說明的機會。 在此步驟中，您還可以配置設定檔擷取、錯誤診斷、部分擷取和警示的設定。

完成後，選取 **[!UICONTROL 下一個]**.

![來源工作流程的資料流詳細資料步驟。](../../../../images/tutorials/create/shopify-streaming/dataflow-detail.png)

## 映射

此 [!UICONTROL 對應] 步驟隨即顯示，為您提供介面，用於將來源結構描述中的來源欄位對應到目標結構描述中適當的目標XDM欄位。

Platform會根據您選取的目標結構描述或資料集，為自動對應的欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。 您可以視需要選擇直接對應欄位，或使用資料準備函式來轉換來源資料，以衍生計算值或計算值。 如需使用對應程式介面和計算欄位的完整步驟，請參閱 [資料準備UI指南](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

成功對應來源資料後，請選取 **[!UICONTROL 下一個]**.

![來源工作流程的對應步驟。](../../../../images/tutorials/create/shopify-streaming/mapping.png)

## 请查看

此 **[!UICONTROL 檢閱]** 步驟隨即顯示，可讓您在建立新資料流之前對其進行檢閱。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **[!UICONTROL 指派資料集和對應欄位]**：顯示要將來源資料擷取到哪個資料集中，包括資料集所堅持的結構描述。

檢閱資料流後，選取 **[!UICONTROL 完成]** 並留出一些時間來建立資料流。

![來源工作流程的稽核步驟。](../../../../images/tutorials/create/shopify-streaming/review.png)

## 取得您的串流端點URL

建立串流資料流後，您現在可以擷取串流端點URL。 此端點將用於訂閱您的webhook，允許您的串流來源與Experience Platform通訊。

若要擷取您的串流端點，請前往 [!UICONTROL 資料流活動] 您剛建立之資料流的頁面，並從底部複製端點 [!UICONTROL 屬性] 面板。

![資料流活動中的串流端點。](../../../../images/tutorials/create/shopify-streaming/endpoint.png)

## 后续步骤

依照本教學課程，您已建立與的來源連線和資料流 [!DNL Shopify Streaming] 帳戶。 如需如何連線的說明，請參閱： [!DNL Shopify Streaming] 帳戶使用API，請閱讀以下主題的教學課程： [建立來源連線和資料流以進行資料流 [!DNL Shopify] 使用流量服務API的資料](../../../api/create/ecommerce/shopify-streaming.md).

---
keywords: Experience Platform；首頁；熱門主題；客戶屬性
solution: Experience Platform
title: 在使用者介面中建立客戶屬性來源連線
type: Tutorial
description: 瞭解如何在UI中建立來源連線，以將客戶屬性設定檔資料匯入Adobe Experience Platform。
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 4%

---

# 在使用者介面中建立客戶屬性來源連線

本教學課程提供在UI中建立來源連線的步驟，以便將客戶屬性設定檔資料匯入Adobe Experience Platform。 如需客戶屬性的詳細資訊，請參閱 [客戶屬性總覽](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html).

>[!IMPORTANT]
>
>客戶屬性來源目前不支援啟用或停用資料流。

## 建立來源連線

>[!NOTE]
>
>如果您已建立客戶屬性設定檔資料的來源連線，則會停用與來源連線的選項。

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立連線的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列來尋找您要使用的特定來源。

在 [!UICONTROL Adobe應用程式] 類別，選取 **[!UICONTROL 客戶屬性]** 然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/customer-attributes/catalog.png)

### 選取客戶屬性資料來源

此 [!UICONTROL 新增資料] 畫面會列出客戶屬性的所有可用資料來源。 每個客戶屬性來源連線只能選取一個資料集。

>[!NOTE]
>
>欄位群組、結構描述和資料集是隨流量布建一起立即建立的。 這些檔案會維持原狀，如有需要，您必須手動刪除。

客戶屬性來源不支援結構描述演變。 如果客戶屬性資料來源的結構描述輸入變更，則會變得與Platform不相容。 做為因應措施，您可以刪除現有的客戶屬性資料流，及其關聯的資料集、結構描述和欄位群組，然後使用更新的結構描述和資料來源建立新的客戶屬性資料流。

>[!IMPORTANT]
>
>雖然您可以刪除客戶屬性資料流，但即使在刪除資料流後，其對應的資料集仍會保留。 請參閱指南： [刪除資料集](../../../../../catalog/datasets/user-guide.md) 瞭解如何手動刪除資料集的步驟。

若要建立新連線，請從清單中選取資料來源，然後選取 **[!UICONTROL 下一個]**.

![add-data](../../../../images/tutorials/create/customer-attributes/add-data.png)

### 提供資料流詳細資料

此 [!UICONTROL 資料流詳細資料] 步驟隨即顯示，讓您為資料流提供名稱和簡短說明。 在此程式中，您也可以為以下專案進行設定： [!UICONTROL 錯誤診斷]， [!UICONTROL 部分擷取]、和 [!UICONTROL 警報].

[!UICONTROL 錯誤診斷] 針對資料流中發生的任何錯誤記錄，啟用詳細的錯誤訊息產生，同時 [!UICONTROL 部分擷取] 可讓您擷取包含錯誤的資料，最多可擷取您手動定義的特定臨界值。 請參閱 [部分批次擷取概觀](../../../../../ingestion/batch-ingestion/partial.md) 以取得詳細資訊。

您可以啟用警報以接收有關資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱來源警報](../../alerts.md).

當您完成提供詳細資訊給資料流時，請選取「 」 **[!UICONTROL 下一個]**.

![資料流 — 詳細資料](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### 檢閱資料流

此 [!UICONTROL 檢閱] 步驟隨即顯示，可讓您在建立新資料流之前對其進行檢閱。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **[!UICONTROL 指派資料集和對應欄位]**：顯示要將來源資料擷取到哪個資料集中，包括資料集所堅持的結構描述。

![檢閱](../../../../images/tutorials/create/customer-attributes/review.png)

## 后续步骤

创建连接后，将自动创建目标架构和数据集，以包含传入数据。初始內嵌完成時，下游平台服務(例如 [!DNL Real-Time Customer Profile] 和 [!DNL Segmentation Service]. 如需更多詳細資訊，請參閱下列檔案：

* [[!DNL Real-Time Customer Profile] 概述](../../../../../profile/home.md)
* [[!DNL Segmentation Service] 概述](../../../../../segmentation/home.md)

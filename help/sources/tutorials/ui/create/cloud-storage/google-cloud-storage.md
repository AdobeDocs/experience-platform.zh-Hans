---
title: 在UI中建立Google雲端儲存空間來源連線
description: 瞭解如何使用Adobe Experience Platform UI建立Google雲端儲存空間來源連線。
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 7181cb92dd44d8005fe1054020ffeb36c309b42e
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---

# 建立 [!DNL Google Cloud Storage] ui中的來源連線

本教學課程提供建立 [!DNL Google Cloud Storage] 來源連線使用Adobe Experience Platform UI。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有有效的 [!DNL Google Cloud Storage] 連線時，您可以略過本檔案的其餘部分，並繼續進行上的教學課程 [設定資料流](../../dataflow/batch/cloud-storage.md).

### 支持的文件格式

[!DNL Experience Platform] 支援從外部儲存體擷取的下列檔案格式：

* 分隔符號分隔值(DSV)：任何單一字元值都可作為DSV格式資料檔案的分隔符號。
* JavaScript物件標籤法(JSON)： JSON格式資料檔案必須符合XDM規範。
* Apache Parquet： Parquet格式資料檔案必須符合XDM標準。

### 收集必要的認證

為了存取您的 [!DNL Google Cloud Storage] 資料，您必須提供下列值：

| 認證 | 描述 |
| ---------- | ----------- |
| 存取金鑰ID | 61個字元的英數字串，用於驗證您的 [!DNL Google Cloud Storage] 至平台的帳戶。 |
| 秘密存取金鑰 | 40個字元的base-64編碼字串，用於驗證您的 [!DNL Google Cloud Storage] 至平台的帳戶。 |
| 存储桶名称 | 您的名稱 [!DNL Google Cloud Storage] 貯體。 如果您想要提供雲端儲存空間中特定子資料夾的存取權，您必須指定貯體名稱。 |
| 文件夹路径 | 您要提供存取權的資料夾路徑。 |

如需這些值的詳細資訊，請參閱 [Google雲端儲存空間HMAC金鑰](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 指南。 有關如何產生您自己的存取金鑰ID和秘密存取金鑰的步驟，請參閱 [[!DNL Google Cloud Storage] 概觀](../../../../connectors/cloud-storage/google-cloud-storage.md).

收集完所需的認證後，您可以依照下列步驟連結 [!DNL Google Cloud Storage] 至平台的帳戶。

## 連線您的 [!DNL Google Cloud Storage] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 以存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 [!UICONTROL 雲端儲存空間] 類別，選取 **[!UICONTROL Google雲端儲存空間]** 然後選取 **[!UICONTROL 新增資料]**.

![Platform UI畫面會顯示來源目錄頁面。](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

此 **[!UICONTROL 連線至Google雲端儲存空間]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要連線現有帳戶，請選取 [!DNL Google Cloud Storage] 您要連線的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![Platform UI畫面會顯示Google Cloud Storage來源的現有帳戶頁面](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### 新帳戶

如果您使用新認證，請選取 **[!UICONTROL 新帳戶]**. 在出現的輸入表單上，提供名稱、選擇性說明，以及 [!DNL Google Cloud Storage] 認證。 在此步驟中，您還可以定義子資料夾的路徑名稱，以指定您的帳戶將有權存取的子資料夾。

完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![Platform UI畫面會顯示Google Cloud Storage來源的新帳戶頁面。](../../../../images/tutorials/create/google-cloud-storage/new.png)


## 后续步骤

依照本教學課程，您已建立與的連線， [!DNL Google Cloud Storage] 帳戶。 您現在可以繼續下一節教學課程和 [設定資料流，將雲端儲存空間中的資料匯入Platform](../../dataflow/batch/cloud-storage.md).

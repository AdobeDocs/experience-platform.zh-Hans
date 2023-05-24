---
keywords: Experience Platform；首頁；熱門主題；Azure Data Lake Storage Gen2；ADLS Gen2；adls gen2；adls聯結器
solution: Experience Platform
title: 在UI中建立Azure Data Lake Storage Gen2來源連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立Azure Data Lake Storage Gen2來源連線。
exl-id: d81b7593-08a3-43f8-a8bc-f5547a6cd55a
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 1%

---

# 建立 [!DNL Azure Data Lake Storage Gen2] ui中的來源連線

Adobe Experience Platform中的來源聯結器可讓您依排程擷取外部來源的資料。 本教學課程提供驗證 [!DNL Azure Data Lake Storage Gen2] (以下稱&quot;[!DNL ADLS Gen2]&quot;)來源聯結器使用 [!DNL Platform] 使用者介面。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   - [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   - [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的ADLS Gen2連線，您可以略過本檔案的其餘部分，並前往上的教學課程 [設定資料流](../../dataflow/batch/cloud-storage.md).

### 收集必要的認證

為了驗證您的 [!DNL ADLS Gen2] 來源聯結器，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `url` | 的端點 [!DNL ADLS Gen2]. |
| `servicePrincipalId` | 應用程式的使用者端ID。 |
| `servicePrincipalKey` | 應用程式的金鑰。 |
| `tenant` | 包含您應用程式的租使用者資訊。 |

如需這些值的詳細資訊，請參閱 [此 [!DNL ADLS Gen2] 檔案](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

## 連線您的 [!DNL ADLS Gen2] 帳戶

收集完所需的認證後，您可以依照下列步驟連結 [!DNL ADLS Gen2] 要連線的帳戶 [!DNL Platform].

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 以存取 **[!UICONTROL 來源]** 工作區。 此 **[!UICONTROL 目錄]** 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 **[!UICONTROL 資料庫]** 類別，選取 **[!UICONTROL Azure Data Lake Gen2]**. 如果您是第一次使用此聯結器，請選取 **[!UICONTROL 設定]**. 否則，請選取 **[!UICONTROL 新增資料]** 建立新的ADLS Gen2聯結器。

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

此 **[!UICONTROL 連線到Azure Data Lake Gen2]** 對話方塊隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 新帳戶

如果您使用新認證，請選取 **[!UICONTROL 新帳戶]**. 在出現的輸入表單上，提供名稱、選擇性說明，以及 [!DNL ADLS Gen2] 認證。 完成後，選取 **[!UICONTROL Connect]** 然後等待一段時間以建立新連線。

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### 現有帳戶

若要連線現有帳戶，請選取 [!DNL ADLS Gen2] 您要連線的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## 后续步骤

依照本教學課程，您已建立與的連線， [!DNL ADLS Gen2] 帳戶。 您現在可以繼續下一節教學課程和 [設定資料流以將雲端儲存空間中的資料帶入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md).

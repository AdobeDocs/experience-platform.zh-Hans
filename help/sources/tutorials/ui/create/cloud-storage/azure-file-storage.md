---
keywords: Experience Platform；首頁；熱門主題；Azure檔案儲存；Azure檔案儲存聯結器
solution: Experience Platform
title: 在UI中建立Azure檔案儲存體來源連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立Azure檔案儲存體來源連線。
exl-id: 25d483b6-3975-4e80-9dbe-28b7b91cb063
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# 建立 [!DNL Azure File Storage] ui中的來源連線

Adobe Experience Platform中的來源聯結器可讓您依排程擷取外部來源的資料。 本教學課程提供驗證 [!DNL Azure File Storage] 來源聯結器使用 [!DNL Platform] 使用者介面。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   - [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   - [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有有效的 [!DNL Azure File Storage] 連線時，您可以略過本檔案的其餘部分，並繼續進行上的教學課程 [設定資料流](../../dataflow/batch/cloud-storage.md).

### 收集必要的認證

為了驗證您的 [!DNL Azure File Storage] 來源聯結器，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `host` | 的端點 [!DNL Azure File Storage] 您正在存取的執行個體。 |
| `userId` | 具有足夠存取許可權的使用者 [!DNL Azure File Storage] 端點。 |
| `password` | 此 [!DNL Azure File Storage] 存取金鑰。 |

如需入門的詳細資訊，請參閱 [此 [!DNL Azure File Storage] 檔案](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

## 連線您的 [!DNL Azure File Storage] 帳戶

收集完所需的認證後，您可以依照下列步驟連結 [!DNL Azure File Storage] 帳戶至 [!DNL Platform].

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 以存取 **[!UICONTROL 來源]** 工作區。 此 **[!UICONTROL 目錄]** 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 **[!UICONTROL 資料庫]** 類別，選取 **[!UICONTROL Azure檔案儲存體]**. 如果您是第一次使用此聯結器，請選取 **[!UICONTROL 設定]**. 否則，請選取 **[!UICONTROL 新增資料]** 以建立新的 [!DNL Azure File Storage] 聯結器。

![目錄](../../../../images/tutorials/create/azure-file-storage/catalog.png)

此 **[!UICONTROL 連線到Azure檔案儲存體]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 新帳戶

如果您使用新認證，請選取 **[!UICONTROL 新帳戶]**. 在出現的輸入表單上，提供名稱、選擇性說明，以及 [!DNL Azure File Storage] 認證。 完成後，選取 **[!UICONTROL Connect]** 然後等待一段時間以建立新連線。

![connect](../../../../images/tutorials/create/azure-file-storage/new.png)

### 現有帳戶

若要連線現有帳戶，請選取 [!DNL Azure File Storage] 您要連線的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![現有](../../../../images/tutorials/create/azure-file-storage/existing.png)

## 后续步骤

依照本教學課程，您已建立與的連線， [!DNL Azure File Storage] 帳戶。 您現在可以繼續下一節教學課程和 [設定資料流以將雲端儲存空間中的資料帶入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md).

---
keywords: Experience Platform；首頁；熱門主題；Azure表格儲存體；Azure表格儲存體；ATS；ATS
solution: Experience Platform
title: 在UI中建立Azure資料表儲存體來源連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立Azure資料表儲存體來源連線。
exl-id: 045cb954-e3e1-439d-a3cd-170d688dfbc8
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# 建立 [!DNL Azure Table Storage] ui中的來源連線

Adobe Experience Platform中的來源聯結器可讓您依排程擷取外部來源的資料。 本教學課程提供建立 [!DNL Azure Table Storage] （以下稱為「ATS」）來源聯結器使用 [!DNL Platform] 使用者介面。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有有效的ATS連線，可以略過本檔案的其餘部分，並前往上的教學課程 [設定資料流](../../dataflow/databases.md).

### 收集必要的認證

若要存取您的ATS帳戶，請 [!DNL Platform]，您必須提供下列值：

| 認證 | 描述 |
| ---------- | ----------- |
| `connectionString` | 要連線至您的檔案的連線字串 [!DNL Azure Table Storage] 執行個體。 要連線至ATS執行個體的連線字串。 ATS的連線字串模式為 `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

如需入門的詳細資訊，請參閱 [此 [!DNL Azure Table Storage] 檔案](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

## 連線您的 [!DNL Azure Table Storage] 帳戶

收集所需的認證後，您可以依照下列步驟將ATS帳戶連結至 [!DNL Platform].

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 以存取 **[!UICONTROL 來源]** 工作區。 此 **[!UICONTROL 目錄]** 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 **[!UICONTROL 資料庫]** 類別，選取 **[!UICONTROL Azure資料表儲存體]**. 如果您是第一次使用此聯結器，請選取 **[!UICONTROL 設定]**. 否則，請選取 **[!UICONTROL 新增資料]** 建立新的ATS聯結器。

![目錄](../../../../images/tutorials/create/ats/catalog.png)

此 **[!UICONTROL 連線到Azure資料表儲存體]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 新帳戶

如果您使用新認證，請選取 **[!UICONTROL 新帳戶]**. 在出現的輸入表單上，提供名稱、選擇性說明和您的ATS認證。 完成後，選取 **[!UICONTROL Connect]** 然後等待一段時間以建立新連線。

![connect](../../../../images/tutorials/create/ats/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的ATS帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![現有](../../../../images/tutorials/create/ats/existing.png)

## 后续步骤

依照本教學課程，您已建立與ATS帳戶的連線。 您現在可以繼續下一節教學課程和 [設定資料流以將資料帶入 [!DNL Platform]](../../dataflow/databases.md).

---
keywords: Experience Platform；首頁；熱門主題；FTP；ftp
solution: Experience Platform
title: 在使用者介面中建立FTP來源連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立FTP來源連線。
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---

# 在使用者介面中建立FTP來源連線

>[!NOTE]
>
>FTP聯結器為Beta版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用Beta標籤聯結器的詳細資訊。

本教學課程提供使用Adobe Experience Platform UI建立FTP來源連線的步驟。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的FTP連線，可以略過本檔案的其餘部分，並前往上的教學課程 [設定資料流](../../dataflow/batch/cloud-storage.md).

### 收集必要的認證

若要連線至FTP，您必須提供下列連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `host` | 與您的FTP伺服器關聯的名稱或IP位址。 |
| `username` | 有權存取您FTP伺服器的使用者名稱。 |
| `password` | FTP伺服器的密碼。 |

## 連線至您的FTP伺服器

收集完所需的認證後，您可以依照下列步驟建立新的FTP帳戶以連線至平台。

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 以存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示各種來源，您可透過這些來源建立入站帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 [!UICONTROL 雲端儲存空間] 類別，選取 **[!UICONTROL FTP]**. 如果您是第一次使用此聯結器，請選取 **[!UICONTROL 設定]**. 否則，請選取 **[!UICONTROL 新增資料]** 以建立新的FTP連線。

![目錄](../../../../images/tutorials/create/ftp/catalog.png)

此 **[!UICONTROL 連線至FTP]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 新帳戶

如果您使用新認證，請選取 **[!UICONTROL 新帳戶]**. 在出現的輸入表單上，提供名稱、選擇性說明和您的認證。 完成後，選取 **[!UICONTROL Connect]** 然後等待一段時間以建立新連線。

![新](../../../../images/tutorials/create/ftp/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的FTP帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![現有](../../../../images/tutorials/create/ftp/existing.png)

## 后续步骤

依照本教學課程，您已建立與FTP帳戶的連線。 您現在可以繼續下一節教學課程和 [設定資料流，將雲端儲存空間中的資料匯入Platform](../../dataflow/batch/cloud-storage.md).

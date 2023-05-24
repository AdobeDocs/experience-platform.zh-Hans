---
keywords: Experience Platform；首頁；熱門主題；Maria DB；maria db
solution: Experience Platform
title: 在使用者介面中建立MariaDB來源連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立Maria DB來源連線。
exl-id: 259ca112-01f1-414a-bf9f-d94caf4c69df
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# 建立 [!DNL MariaDB] ui中的來源連線

Adobe Experience Platform中的來源聯結器可讓您依排程擷取外部來源的資料。 本教學課程提供使用「 」建立Maria DB來源聯結器的步驟。 [!DNL Platform] 使用者介面。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [即時客戶個人檔案](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有 [!DNL MariaDB] 連線時，您可以略過本檔案的其餘部分，並繼續進行上的教學課程 [設定資料流](../../dataflow/databases.md).

### 收集必要的認證

為了存取您的 [!DNL MariaDB] 帳戶於 [!DNL Platform]，您必須提供下列值：

| 認證 | 描述 |
| ---------- | ----------- |
| `connectionString` | 與您的MariaDB驗證相關聯的連線字串。 此 [!DNL MariaDB] 連線字串模式為： `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |

如需入門的詳細資訊，請參閱此 [[!DNL MariaDB] 檔案](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

## 連線您的 [!DNL Maria DB] 帳戶

收集完所需的認證後，您可以依照下列步驟連結 [!DNL Maria DB] 帳戶至 [!DNL Platform].

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 以存取 **[!UICONTROL 來源]** 工作區。 此 **[!UICONTROL 目錄]** 畫面會顯示您可以用來建立帳戶的各種來源。

在 **[!UICONTROL 資料庫]** 類別，選取 **[!UICONTROL Maria DB]**. 如果您是第一次使用此聯結器，請選取 **[!UICONTROL 設定]**. 否則，請選取 **[!UICONTROL 新增資料]** 以建立新的 [!DNL Maria DB] 聯結器。

![](../../../../images/tutorials/create/maria-db/catalog.png)

此 **[!UICONTROL 連線至Maria DB]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 新帳戶

如果您使用新認證，請選取 **[!UICONTROL 新帳戶]**. 在出現的輸入表單上，提供名稱、選擇性說明，以及 [!DNL MariaDB] 認證。 完成後，選取 **[!UICONTROL Connect]** 然後等待一段時間以建立新連線。

![](../../../../images/tutorials/create/maria-db/new.png)

### 現有帳戶

若要連線現有帳戶，請選取 [!DNL MariaDB] 您要連線的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![](../../../../images/tutorials/create/maria-db/existing.png)

## 后续步骤

依照本教學課程，您已建立與的連線， [!DNL MariaDB] 帳戶。 您現在可以繼續下一節教學課程和 [設定資料流以將資料帶入 [!DNL Platform]](../../dataflow/databases.md).

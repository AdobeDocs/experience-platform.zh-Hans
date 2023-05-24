---
keywords: Experience Platform；首頁；熱門主題；HP Vertica
solution: Experience Platform
title: 在使用者介面中建立HP Vertica來源連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立HP Vertica來源連線。
exl-id: d7315ad4-9250-4e66-be33-016efabb512e
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 1%

---

# 建立HP [!DNL Vertica] ui中的來源連線

>[!NOTE]
>
> HP [!DNL Vertica] 聯結器為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用Beta標籤聯結器的詳細資訊。

Adobe Experience Platform中的來源聯結器可讓您依排程擷取外部來源的資料。 本教學課程提供建立HP的步驟 [!DNL Vertica] 來源聯結器使用 [!DNL Platform] 使用者介面。

## 快速入门

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經擁有有效的HP [!DNL Vertica] 連線時，您可以略過本檔案的其餘部分，並繼續進行上的教學課程 [設定資料流](../../dataflow/databases.md).

### 收集必要的認證

下列章節提供您成功連線到HP所需的其他資訊 [!DNL Vertica] 使用 [!DNL Flow Service] API。

| 認證 | 描述 |
| ---------- | ----------- |
| `connectionString` | 用來連線至HP的連線字串 [!DNL Vertica] 執行個體。 HP的連線字串模式 [!DNL Vertica] 是 `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

如需入門的詳細資訊，請參閱 [此HP [!DNL Vertica] 檔案](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm).

## 連線您的HP [!DNL Vertica] 帳戶

收集所需的認證後，您可以依照下列步驟連結HP [!DNL Vertica] 帳戶至 [!DNL Platform].

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 以存取 **[!UICONTROL 來源]** 工作區。 此 **[!UICONTROL 目錄]** 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 **[!UICONTROL 資料庫]** 類別，選取 **[!UICONTROL HP Vertica]**. 如果您是第一次使用此聯結器，請選取 **[!UICONTROL 設定]**. 否則，請選取 **[!UICONTROL 新增資料]** 建立新的HP [!DNL Vertica] 聯結器。

![目錄](../../../../images/tutorials/create/hp-vertica/catalog.png)

此 **[!UICONTROL 連線到HP Vertica]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 新帳戶

如果您使用新認證，請選取 **[!UICONTROL 新帳戶]**. 在出現的輸入表單上，提供名稱、可選說明和您的HP [!DNL Vertica] 認證。 完成後，選取 **[!UICONTROL Connect]** 然後等待一段時間以建立新連線。

![connect](../../../../images/tutorials/create/hp-vertica/new.png)

### 現有帳戶

若要連線現有帳戶，請選取HP [!DNL Vertica] 您要連線的帳戶，然後選取 **[!UICONTROL 下一個]** 前往右上角以繼續。

![現有](../../../../images/tutorials/create/hp-vertica/existing.png)

## 后续步骤

依照本教學課程，您已建立與HP的連線 [!DNL Vertica] 帳戶。 您現在可以繼續下一節教學課程和 [設定資料流以將資料帶入 [!DNL Platform]](../../dataflow/databases.md).

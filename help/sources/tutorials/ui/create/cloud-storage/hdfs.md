---
keywords: Experience Platform；首頁；熱門主題；Apache HDFS；HDFS；hdfs
solution: Experience Platform
title: 在使用者介面中建立Apache HDFS來源連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立ApacheHadoop分散式檔案系統來源連線。
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# 建立 [!DNL Apache] UI中的HDFS來源連線

>[!NOTE]
>
>此 [!DNL Apache] HDFS聯結器為Beta版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用Beta標籤聯結器的詳細資訊。

中的來源聯結器 [!DNL Adobe Experience Platform] 提供依排程擷取外部來源資料的功能。 本教學課程提供驗證 [!DNL Apache Hadoop Distributed File System] （以下稱為「HDFS」）來源聯結器使用 [!DNL Platform] 使用者介面。

## 快速入门

本教學課程需要您深入瞭解下列元件 [!DNL Platform]：

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
   - [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   - [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的HDFS連線，您可以略過本檔案的其餘部分，並前往上的教學課程 [設定資料流](../../dataflow/batch/cloud-storage.md).

### 收集必要的認證

為了驗證您的HDFS來源聯結器，您必須提供以下連線屬性的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `url` | URL會定義匿名連線至HDFS所需的驗證引數。 如需如何取得此值的詳細資訊，請參閱以下檔案： [HDFS的HTTPS驗證](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## 連線您的HDFS帳戶

收集必要的認證後，您可以依照下列步驟將HDFS帳戶連結至 [!DNL Platform].

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 以存取 **[!UICONTROL 來源]** 工作區。 此 **[!UICONTROL 目錄]** 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 **[!UICONTROL 雲端儲存空間]** 類別，選取 **[!UICONTROL Apache HDFS]**. 如果您是第一次使用此聯結器，請選取 **[!UICONTROL 設定]**. 否則，請選取 **[!UICONTROL 新增資料]** 建立新的HDFS聯結器。

![目錄](../../../../images/tutorials/create/hdfs/catalog.png)

此 **[!UICONTROL 連線到HDFS]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 新帳戶

如果您使用新認證，請選取 **[!UICONTROL 新帳戶]**. 在出現的輸入表單上，提供名稱、選擇性說明和您的HDFS認證。 完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![connect](../../../../images/tutorials/create/hdfs/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的HDFS帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![現有](../../../../images/tutorials/create/hdfs/existing.png)

## 后续步骤

依照本教學課程，您已建立與HDFS帳戶的連線。 您現在可以繼續下一節教學課程和 [設定資料流以將雲端儲存空間中的資料帶入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md).

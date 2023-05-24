---
keywords: Experience Platform；首頁；熱門主題；Google Big Query；google big query；GBQ；gbq
solution: Experience Platform
title: 在UI中建立Google Big Query來源連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立Google Big Query來源連線。
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# 建立 [!DNL Google Big Query] ui中的來源連線

Adobe Experience Platform中的來源聯結器可讓您依排程擷取外部來源的資料。 本教學課程提供建立 [!DNL Google Big Query] 使用Platform使用者介面的來源連線。

## 快速入门

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置組塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器UI建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有有效的 [!DNL Google BigQuery] 連線時，您可以略過本檔案的其餘部分，並繼續進行上的教學課程 [設定資料流](../../dataflow/databases.md).

### 收集必要的認證

為了存取您的 [!DNL Google BigQuery] 帳戶，您必須提供下列OAuth 2.0驗證值：

| 認證 | 描述 |
| ---------- | ----------- |
| `project` | 預設的專案ID [!DNL Google BigQuery] 要查詢的專案。 |
| `clientID` | 用來產生重新整理權杖的ID值。 |
| `clientSecret` | 用來產生重新整理權杖的密碼值。 |
| `refreshToken` | 重新整理權杖取得自 [!DNL Google] 用於授權存取 [!DNL Google BigQuery]. |

如需這些值的詳細資訊，請參閱 [此 [!DNL Google BigQuery] 檔案](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## 連線您的Google BigQuery帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列來尋找您要使用的特定來源。

在 [!UICONTROL 資料庫] 類別，選取 **[!UICONTROL Google BigQuery]** 然後選取 **[!UICONTROL 新增資料]**.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

此 **[!UICONTROL 連線到Google Big Query]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要連線現有帳戶，請選取 [!DNL Google BigQuery] 您要連線的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![](../../../../images/tutorials/create/google-big-query/existing.png)

### 新帳戶

如果您使用新認證，請選取 **[!UICONTROL 新帳戶]**. 在出現的輸入表單上，提供名稱、選擇性說明，以及 [!DNL Google BigQuery] 認證。 完成後，選取 **[!UICONTROL 連線到來源]** 然後等待一段時間以建立新連線。

![](../../../../images/tutorials/create/google-big-query/new.png)

## 后续步骤

依照本教學課程，您已建立與的連線， [!DNL Google BigQuery] 帳戶。 您現在可以繼續下一節教學課程和 [設定資料流以將資料匯入Platform](../../dataflow/databases.md).

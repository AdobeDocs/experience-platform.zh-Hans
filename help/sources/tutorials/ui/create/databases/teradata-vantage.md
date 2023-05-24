---
keywords: Experience Platform；首頁；熱門主題；Teradata優勢
title: 在UI中建立Teradata Vantage來源連線
description: 瞭解如何使用Adobe Experience Platform UI建立Teradata Vantage來源連線。
exl-id: 3fdb09fa-128a-477b-9144-d4ef3ed18ea6
source-git-commit: 322b9aa5b817276eb4b56daf6e410944591c1d51
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# (Beta)建立 [!DNL Teradata Vantage] ui中的來源連線

>[!NOTE]
>
> 此 [!DNL Teradata Vantage] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

本教學課程提供建立 [!DNL Teradata Vantage] 使用Adobe Experience Platform使用者介面的來源聯結器。

## 快速入门

本教學課程需要深入瞭解下列Platform元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Experience Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 收集必要的認證

為了存取您的 [!DNL Teradata Vantage] 帳戶，您必須提供下列驗證值：

| 認證 | 描述 |
| ---------- | ----------- |
| 連線字串 | 連線字串是提供有關資料來源以及如何與其連線的資訊的字串。 的連線字串模式 [!DNL Teradata Vantage] 是 `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

如需入門的詳細資訊，請參閱此 [[!DNL Teradata Vantage] 檔案](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## 連線您的 [!DNL Teradata Vantage] 帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列來尋找您要使用的特定來源。

在 [!UICONTROL 資料庫] 類別，選取 **[!UICONTROL teradata優勢]** 然後選取 **[!UICONTROL 新增資料]**.

![](../../../../images/tutorials/create/teradata/catalog.png)

此 **[!UICONTROL 連線到Teradata Vantage]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要連線現有帳戶，請選取 [!DNL Teradata Vantage] 您要連線的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![](../../../../images/tutorials/create/teradata/existing.png)

### 新帳戶

如果您使用新認證，請選取 **[!UICONTROL 新帳戶]**. 在出現的輸入表單上，提供名稱、選擇性說明，以及 [!DNL Teradata Vantage] 認證。 完成後，選取 **[!UICONTROL Connect]** 然後等待一段時間以建立新連線。

![](../../../../images/tutorials/create/teradata/new.png)

## 后续步骤

依照本教學課程，您已建立與您的TeradataVantage帳戶的連線。 您現在可以繼續下一節教學課程和 [設定資料流以將資料匯入Platform](../../dataflow/databases.md).

---
keywords: Experience Platform；首頁；熱門主題；通用REST API
title: 在UI中建立通用REST API來源連線
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立通用REST API來源連線。
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 1%

---

# 建立 [!DNL Generic REST API] ui中的來源連線

>[!NOTE]
>
> 此 [!DNL Generic REST API] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用Beta標籤聯結器的詳細資訊。

本教學課程提供建立 [!DNL Generic REST API] 使用Adobe Experience Platform使用者介面的來源聯結器。

## 快速入门

本教學課程需要深入瞭解下列Platform元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 收集必要的認證

為了存取您的 [!DNL Generic REST API] Platform上的帳戶，您必須提供所選驗證型別的有效認證。 一般REST API支援OAuth 2重新整理程式碼和基本驗證。 請參閱下清單格，瞭解兩種支援的驗證型別之證明資料的資訊。

#### OAuth 2重新整理程式碼

| 認證 | 描述 |
| --- | --- |
| Host | 您向其提出請求的來源的主機URL。 此值為必填，且不能使用要求引數覆寫略過。 |
| 授權測試URL | （選用）建立基本連線時，會使用授權測試URL來驗證認證。 如果未提供，則會在來源連線建立步驟期間自動檢查認證。 |
| 使用者端ID | （選用）與您的使用者帳戶相關聯的使用者端ID。 |
| 使用者端密碼 | （選用）與您的使用者帳戶相關聯的使用者端密碼。 |
| 存取權杖 | 用來存取您的應用程式的主要驗證認證。 存取權杖代表應用程式的授權，可存取使用者資料的特定方面。 此值為必填，且不能使用要求引數覆寫略過。 |
| 重新整理Token | （選用）當存取權杖過期時，用來產生新存取權杖的權杖。 |
| 存取權杖URL | （選用）用來擷取存取權杖的URL端點。 |
| 要求引數覆寫 | （選用）屬性，可讓您指定要覆寫哪些認證引數。 |


#### 基本驗證

| 認證 | 描述 |
| --- | --- |
| Host | 您向其提出請求的來源的主機URL。 |
| 用户名 | 與您的使用者帳戶對應的使用者名稱。 |
| 密码 | 與您的使用者帳戶對應的密碼。 |

## 連線您的通用REST API帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 從左側導覽存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列來尋找您要使用的特定來源。

在 [!UICONTROL 通訊協定] 類別，選取 **[!UICONTROL 一般REST API]** 然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/generic-rest/catalog.png)

此 **[!UICONTROL 連線至一般REST API]** 頁面便會顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要連線現有帳戶，請選取您要連線的Generic REST API帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![現有](../../../../images/tutorials/create/generic-rest/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後為您的新提供名稱和選項說明 [!DNL Generic REST API] 帳戶。

![新](../../../../images/tutorials/create/generic-rest/new.png)

#### 使用OAuth 2重新整理代碼進行驗證

[!DNL Generic REST API] 支援OAuth 2重新整理程式碼和基本驗證。 若要使用OAuth2驗證進行驗證，請選取 **[!UICONTROL OAuth2RefreshCode]**，提供您的OAuth 2認證，然後選取 **[!UICONTROL 連線到來源]**.

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### 使用基本驗證進行驗證

若要使用基本驗證，請選取 **[!UICONTROL 基本驗證]**，提供您的主機、使用者名稱和密碼，然後選取 **[!UICONTROL 連線到來源]**.

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## 后续步骤

依照本教學課程，您已建立與通用REST API帳戶的連線。 您現在可以繼續下一節教學課程和 [設定資料流以將資料匯入Platform](../../dataflow/protocols.md).

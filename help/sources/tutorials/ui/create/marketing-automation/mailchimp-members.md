---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
solution: Experience Platform
title: 使用Platform UI建立MailChimp成員來源連線
description: 瞭解如何使用Platform UI將Adobe Experience Platform連線至MailChimp成員。
exl-id: dc620ef9-624d-4fc9-8475-bb475ea86eb7
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# 建立 [!DNL Mailchimp Members] 使用Platform UI的來源連線

本教學課程提供建立 [!DNL Mailchimp] 要內嵌的來源聯結器 [!DNL Mailchimp Members] 使用使用者介面將資料匯入Adobe Experience Platform。

## 快速入门

本指南需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../../../home.md)：Platform可從各種來源擷取資料，同時讓您能夠使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md)：Platform提供虛擬沙箱，可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 收集必要的認證

為了將您的 [!DNL Mailchimp Members] 資料傳送至Platform時，您必須先提供與您對應的適當驗證認證 [!DNL Mailchimp] 帳戶。

此 [!DNL Mailchimp Members] 原始碼支援OAuth 2重新整理程式碼和基本驗證。 如需這些驗證型別的詳細資訊，請參閱下表。

### OAuth 2重新整理程式碼

| 凭据 | 描述 |
| --- | --- |
| Domain | 用來連線至MailChimp API的根URL。 根URL的格式為 `https://{DC}.api.mailchimp.com`，其中 `{DC}` 代表與您的帳戶對應的資料中心。 |
| 授權測試URL | 授權測試URL用於驗證連線時的認證 [!DNL Mailchimp] 至平台。 如果未提供，則會在來源連線建立步驟期間自動檢查認證。 |
| 存取Token | 用於驗證您的來源的對應存取權杖。 這是OAuth型驗證的必要專案。 |

如需使用OAuth 2驗證您的身分的詳細資訊 [!DNL Mailchimp] Platform帳戶，請參閱此 [[!DNL Mailchimp] 有關使用OAuth 2的檔案](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/).

### 基本驗證

| 凭据 | 描述 |
| --- | --- |
| Domain | 用來連線至MailChimp API的根URL。 根URL的格式為 `https://{DC}.api.mailchimp.com`，其中 `{DC}` 代表與您的帳戶對應的資料中心。 |
| 用户名 | 與您的MailChimp帳戶對應的使用者名稱。 這是進行基本驗證所必需的。 |
| 密码 | 與您的MailChimp帳戶對應的密碼。 這是進行基本驗證所必需的。 |

## 連線您的 [!DNL Mailchimp Members] 平台帳戶

在Platform UI中選取 **[!UICONTROL 來源]** 以存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可以用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項來尋找您要使用的特定來源。

在 [!UICONTROL 行銷自動化] 類別，選取 **[!UICONTROL Mailchimp行銷活動]**，然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/mailchimp-members/catalog.png)

此 **[!UICONTROL 連線Mailchimp行銷活動帳戶]** 頁面便會顯示。 在此頁面中，您可以選取是要存取現有帳戶，還是選擇建立新帳戶。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Mailchimp Members] 要用來建立新資料流的帳戶，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![現有](../../../../images/tutorials/create/mailchimp-members/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後為提供名稱和說明 [!DNL Mailchimp Members] 來源連線詳細資料。

![新](../../../../images/tutorials/create/mailchimp-members/new.png)


#### 使用OAuth 2進行驗證

若要使用OAuth 2，請選取 [!UICONTROL OAuth 2重新整理程式碼]，為您的網域、授權測試URL和存取權杖提供值，然後選取 **[!UICONTROL 連線到來源]**. 請稍候片刻讓您的認證進行驗證，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![OAuth 身份验证](../../../../images/tutorials/create/mailchimp-members/oauth.png)

#### 使用基本驗證進行驗證

若要使用基本驗證，請選取 [!UICONTROL 基本驗證]，提供網域、使用者名稱和密碼的值，然後選取 **[!UICONTROL 連線到來源]**. 請稍候片刻讓您的認證進行驗證，然後選取 **[!UICONTROL 下一個]** 以繼續進行。

![基本](../../../../images/tutorials/create/mailchimp-members/basic.png)

### 選取 [!DNL Mailchimp Members] 資料

來源通過驗證後，您必須提供 `listId` 與您的 [!DNL Mailchimp Members] 帳戶。

於 [!UICONTROL 選取資料] 頁面，輸入您的 `listId` 然後選取 **[!UICONTROL 探索]**.

![探索](../../../../images/tutorials/create/mailchimp-members/explore.png)

頁面會更新為互動式結構描述樹狀結構，讓您探索及檢查資料的階層。 選取 **[!UICONTROL 下一個]** 以繼續進行。

![select-data](../../../../images/tutorials/create/mailchimp-members/select-data.png)

## 后续步骤

搭配您的 [!DNL Mailchimp] 帳戶已驗證，且 [!DNL Mailchimp Members] 選取的資料，您現在可以開始建立資料流，將您的資料匯入Platform。 如需建立資料流的詳細步驟，請參閱以下檔案： [建立資料流以將行銷自動化資料帶入Platform](../../dataflow/marketing-automation.md).

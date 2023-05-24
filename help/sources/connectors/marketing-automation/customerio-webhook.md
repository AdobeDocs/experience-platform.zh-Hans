---
title: Customer.io來源概觀
description: 瞭解如何使用API或使用者介面運用Webhook將Customer.io連線至Adobe Experience Platform
badge: Beta
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---

# [!DNL Customer.io]

>[!NOTE]
>
>此 [!DNL Customer.io] 來源為測試版。 請閱讀 [來源概觀](../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從串流應用程式擷取資料。 對串流提供者的支援包括 [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) 是自動化傳訊平台，適合需要更多控制和靈活性的行銷人員使用，以製作和傳送資料導向電子郵件、推播通知、應用程式內訊息和簡訊。

此 [!DNL Customer.io] 來源可讓您從擷取支援的webhook事件結構描述及其相關事件資料 [!DNL Customer.io] 使用 [[!DNL Customer.io] 報告Webhook](https://customer.io/docs/api/webhooks/).

支援的webhook事件結構描述包括：

* 客戶事件
* 電子郵件事件
* 簡訊事件
* 推播通知事件
* 應用程式內訊息事件
* Slack事件
* Webhook活動

如需可透過Webhook使用的事件清單，請參閱 [[!DNL Customer.io] 報告Webhook事件](https://customer.io/docs/webhooks/#events) 說明檔案。

## 先决条件 {#prerequisites}

建立之前 [!DNL Customer.io] 來源連線，您必須先確定您有以下專案：

* A [!DNL Customer.io] 帳戶。 如果您沒有許可權，請閱讀 [[!DNL Customer.io] 註冊頁面](https://fly.customer.io/signup) 以註冊及建立您的帳戶。
* 建立帳戶後，您還需要驗證帳戶。 請依照上所記錄的步驟操作 [[!DNL Customer.io] 帳戶驗證](https://customer.io/docs/account-verification/) 頁面以完成此程式。

### 設定 [!DNL Customer.io] Webhook {#set-up-webhook}

成功建立資料流後，您必須設定報表Webhook，以通知Platform以下事項 [!DNL Customer.io] 事件。 Webhook可在客戶屬性變更或有人開啟您的訊息時立即通知您，並將此資訊傳送至您的 [!DNL Customer.io] 來源。 如需詳細資訊，請閱讀上的教學課程 [取得您的串流端點URL](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) 和 [設定 [!DNL Customer.io] Webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## 正在連線 [!DNL Customer.io] 至平台 {#connect-to-platform}

以下檔案提供如何建立 [!DNL Customer.io] 要連線的串流連線 [!DNL Platform] 使用API或使用者介面：

### Connect [!DNL Customer.io] 使用API移至Platform {#connect-to-platform-using-api}

* [建立來源連線和資料流以帶來 [!DNL Customer.io] 使用API將資料傳輸至Platform。](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Connect [!DNL Customer.io] 使用UI移至Platform {#connect-to-platform-using-ui}

* [建立來源連線和資料流以帶來 [!DNL Customer.io] 使用使用者介面將資料傳送至Platform](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)

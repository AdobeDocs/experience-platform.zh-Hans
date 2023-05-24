---
title: Chatlio來源概觀
description: 瞭解如何使用API或使用者介面利用Webhook將Chatlio連線至Adobe Experience Platform
badge: Beta
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# [!DNL Chatlio]

>[!NOTE]
>
>此 [!DNL Chatlio] 來源為測試版。 請閱讀 [來源概觀](../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從串流應用程式擷取資料。 對串流提供者的支援包括 [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) 是與完全整合的即時聊天應用程式 [!DNL Slack] 和協助多位支援代理同時協助個別網站訪客。 [!DNL Chatlio] 使用 [!DNL Chatio Zapier App] 以連線 [!DNL Chatlio] 超過2000種不同的應用程式和服務。

此 [!DNL Chatlio] 來源可讓您從擷取支援的webhook事件結構描述及其相關事件資料 [!DNL Chatlio.com] 使用 [[!DNL Chatlio] Webhook](https://chatlio.com/docs/webhooks/).

支援的Webhook包括：

* 匯出聊天記錄
* 匯出離線訊息
* 新交談已開始
* 訪客未及時收到答案
* 訪客在聊天後留下意見回饋

## 先决条件 {#prerequisites}

建立之前 [!DNL Chatlio] 來源連線，您必須先確定您有以下專案：

* A [!DNL Chatlio] 帳戶。 如果您還沒有訪客，請前往 [[!DNL Chatlio] 註冊頁面](https://chatlio.com/app/#/signup) 以註冊及建立您的帳戶。
* 成功註冊帳戶後，請遵循 [[!DNL Chatlio] 設定檔案](https://chatlio.com/docs/setup/) 以完成您的帳戶設定。

### 設定 [!DNL Chatlio] webhook {#set-up-webhook}

成功建立資料流後，您必須設定webhook以通知Platform以下事項 [!DNL Chatlio] 事件。 Webhook可在客戶屬性變更或有人開啟您的訊息並將此資訊傳送給您的時立即通知您 [!DNL Chatlio] 來源。

如需詳細資訊，請閱讀上的教學課程 [取得您的串流端點URL](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) 和 [設定 [!DNL Chatlio] Webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Connect [!DNL Chatlio] 至平台 {#connect-to-platform}

以下檔案提供如何建立 [!DNL Chatlio] 要連線的串流聯結器 [!DNL Platform] 使用API或使用者介面：

### Connect [!DNL Chatlio] 使用API移至Platform {#connect-to-platform-using-api}

* [建立來源連線以帶來 [!DNL Chatlio] 使用API將資料傳輸至Platform。](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Connect [!DNL Chatlio] 使用UI移至Platform {#connect-to-platform-using-ui}

* [建立來源連線以帶來 [!DNL Chatlio] 使用使用者介面將資料傳送至Platform](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)

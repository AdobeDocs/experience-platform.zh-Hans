---
keywords: Experience Platform；首頁；熱門主題；Zendesk；zendesk
solution: Experience Platform
title: Zendesk來源聯結器概述
description: 瞭解如何使用API或使用者介面將Zendesk連線到Adobe Experience Platform。
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: 61b694ca5fbd3548243663b3f1bff06aaca72434
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 2%

---

# (Beta) [!DNL Zendesk]

>[!NOTE]
>
>此 [!DNL Zendesk] 來源為測試版。 請參閱 [來源概觀](../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform提供從協力廠商客戶成功應用程式擷取資料的支援。 對客戶成功提供者的支援包括 [!DNL Zendesk].

此Adobe Experience Platform [來源](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=zh-Hans) 可運用 [Zendesk Search API >匯出搜尋結果](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) 這會從Zendesk將使用者資訊傳回Experience Platform，以供進一步處理。

## IP位址允許清單

在使用來源聯結器之前，必須將IP位址清單新增至允許清單。 使用來源時，若未將您地區專屬的IP位址新增至允許清單，可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 驗證您的 [!DNL Zendesk] 帳戶

[!DNL Zendesk] 使用持有人權杖作為驗證機制，與 [!DNL Zendesk] API。

本節概述驗證您的憑證時需要完成的先決條件步驟。 [!DNL Zendesk] 帳戶。

* 驗證您的憑證的第一步 [!DNL Zendesk] 帳戶是為了確保您擁有 [!DNL Zendesk] 支援帳戶。 如果您還沒有這類檔案，請參閱 [[!DNL Zendesk] 註冊頁面](https://www.zendesk.com/register/) 以註冊及建立您的Zendesk帳戶。
* 註冊成功後，請導覽至 [[!DNL Zendesk] 網站](https://www.zendesk.com/login/) 並提供您的 **子網域**.
* 接下來，選取 **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* 最後，從擷取您的API Token **[!DNL API token]** 區段。

![Zendesk API權杖](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

請參閱 [[!DNL Zendesk documentation on subdomains]](https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain-) 以取得有關如何擷取子網域的資訊。 如需有關產生API權杖的資訊，請參閱 [[!DNL Zendesk] 產生新API權杖的指南](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token).

以下檔案提供有關如何連線的資訊 [!DNL Zendesk] 使用API或使用者介面的to Platform：

## Connect [!DNL Zendesk] 使用API移至Platform

* [建立來源連線和資料流，用於 [!DNL Zendesk] 使用流量服務API](../../tutorials/api/create/customer-success/zendesk.md)

## Connect [!DNL Zendesk] 使用UI移至Platform

* [建立 [!DNL Zendesk ]ui中的來源連線](../../tutorials/ui/create/customer-success/zendesk.md)
* [在UI中建立客戶成功來源連線的資料流](../../tutorials/ui/dataflow/customer-success.md)

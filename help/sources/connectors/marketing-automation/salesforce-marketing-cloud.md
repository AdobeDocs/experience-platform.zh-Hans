---
solution: Experience Platform
title: SalesforceMarketing Cloud來源概觀
description: 瞭解如何使用API或使用者介面將SalesforceMarketing Cloud連結至Adobe Experience Platform。
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
source-git-commit: 997a9dc70145a8cfd5d6da20ba788a4610e5c257
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform提供從協力廠商行銷自動化系統擷取資料的支援。 對行銷自動化提供者的支援包括 [!DNL Salesforce Marketing Cloud].

## 先决条件

連線之前 [!DNL Salesforce Marketing Cloud] platform的來源，您必須確保以下各項 **許可權範圍** 已布建至您的 [!DNL Salesforce Marketing Cloud] 使用者端ID和使用者端密碼組合：

* `campaign_read`
* `list_and_subscribers_read`

您可以呼叫 `v2/userinfo` 的資源 [!DNL Salesforce Marketing Cloud] API。 請參閱 [[!DNL Salesforce Marketing Cloud] API整合許可權範圍檔案](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) 以取得如何請求和比較範圍的指引。

如需有關範圍的詳細資訊，包括其相關許可權和行為清單，請參閱此 [[!DNL Salesforce Marketing Cloud] REST API檔案](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>自訂物件擷取目前不支援 [!DNL Salesforce Marketing Cloud] 來源整合。

## IP位址允許清單

在使用來源聯結器之前，必須將IP位址清單新增至允許清單。 使用來源時，若未將您地區專屬的IP位址新增至允許清單，可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## Connect [!DNL Salesforce Marketing Cloud] 使用API移至Platform

以下檔案提供有關如何連線的資訊 [!DNL Salesforce Marketing Cloud] 使用API移至Platform：

* [使用Flow Service API建立SalesforceMarketing Cloud基本連線](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [使用Flow Service API探索資料表](../../tutorials/api/explore/tabular.md)
* [使用流量服務API為行銷自動化來源建立資料流](../../tutorials/api/collect/marketing-automation.md)

## Connect [!DNL Salesforce Marketing Cloud] 使用UI移至Platform

以下檔案提供有關如何連線的資訊 [!DNL Salesforce Marketing Cloud] 至使用使用者介面的Platform：

* [在使用者介面中建立SalesforceMarketing Cloud來源連線](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [在UI中建立行銷自動化來源連線的資料流](../../tutorials/ui/dataflow/marketing-automation.md)

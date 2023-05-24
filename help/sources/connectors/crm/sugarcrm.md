---
title: SugarCRM來源概觀
description: 瞭解如何使用API或使用者介面將SugarCRM連線至Adobe Experience Platform。
badge: Beta
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# (Beta) [!DNL SugarCRM]

>[!NOTE]
>
>此 [!DNL SugarCRM] 來源為測試版。 請參閱 [來源概觀](../../home.md#terms-and-conditions) 以取得有關使用測試版標籤來源的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從協力廠商CRM應用程式擷取資料。 CRM提供者的支援包括 [!DNL SugarCRM].

[[!DNL SugarCRM]](https://www.sugarcrm.com/) 是客戶關係管理(CRM)系統。 [!DNL SugarCRM]的功能包括銷售人員自動化、行銷活動、客戶支援、共同作業、Mobile CRM、Social CRM和報表。

此 [!DNL SugarCRM] 來源可讓您從下列API端點擷取帳戶、聯絡人和事件資料：

* [帐户](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [連絡人](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [事件](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)


[!DNL SugarCRM] 使用持有人權杖作為驗證機制，與 [!DNL SugarCRM] 帳戶和連絡人API以及 [!DNL SugarCRM] 事件API。

## IP位址允許清單

在使用來源聯結器之前，必須將IP位址清單新增至允許清單。 使用來源時，若未將您地區專屬的IP位址新增至允許清單，可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 先决条件

建立之前 [!DNL SugarCRM] 來源連線，您必須先確定您有以下專案：

* A [!DNL SugarMarket] 帳戶。 您必須聯絡 [!DNL SugarCRM] 帳戶管理員以取得有效的 [!DNL SugarMarket] 帳戶（如果尚未擁有）。

* 與行銷或銷售程式相關之任何使用者帳戶分開的唯一API使用者名稱和帳戶。 此唯一使用者名稱和帳戶組合必須具有API存取許可權。 如需設定帳戶的詳細資訊，請瀏覽 [[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro) 說明檔案。

## Connect [!DNL SugarCRM Accounts & Contacts] 至平台

* [建立來源連線以帶來 [!DNL SugarCRM Accounts & Contacts] 使用API將資料匯入Platform](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md).
* [建立來源連線以帶來 [!DNL SugarCRM Accounts & Contacts] 使用使用者介面將資料傳送至Platform](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md).
* [使用流量服務API為CRM來源建立資料流](../../tutorials/api/collect/crm.md)


## Connect [!DNL SugarCRM Events] 至平台

* [建立來源連線以帶來 [!DNL SugarCRM Events] 使用API將資料匯入Platform](../../tutorials/api/create/crm/sugarcrm-events.md).
* [建立來源連線以帶來 [!DNL SugarCRM Events] 使用使用者介面將資料傳送至Platform](../../tutorials/ui/create/crm/sugarcrm-events.md).
* [在UI中為CRM來源連線建立資料流](../../tutorials/ui/dataflow/crm.md)

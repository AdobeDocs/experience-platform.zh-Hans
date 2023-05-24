---
keywords: Experience Platform；首頁；熱門主題；Zoho CRM；zoho crm；Zoho；zoho
solution: Experience Platform
title: Zoho CRM來源聯結器概述
description: 瞭解如何使用API或使用者介面將Zoho CRM連線至Adobe Experience Platform。
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# [!DNL Zoho CRM]

Adobe Experience Platform可從外部來源擷取資料，同時讓您能夠使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform提供從協力廠商CRM系統擷取資料的支援。 CRM提供者的支援包括 [!DNL Zoho CRM].

## IP位址允許清單

在使用來源聯結器之前，必須將IP位址清單新增至允許清單。 使用來源時，若未將您地區專屬的IP位址新增至允許清單，可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 擷取您的驗證認證 [!DNL Zoho CRM]

在您從帶入資料之前 [!DNL Zoho CRM] Platform的帳戶，您必須先擷取認證以驗證您的 [!DNL Zoho CRM] 來源。 請依照下列步驟擷取您的使用者端ID、使用者端密碼、存取權杖和重新整理權杖。

### 註冊您的應用程式

擷取驗證認證的第一步，是使用 [[!DNL Zoho CRM] 開發人員主控台](https://accounts.zoho.com/). 若要註冊您的應用程式，您必須從下列專案選取使用者端型別：Java Script、網頁式、行動裝置、非瀏覽器行動應用程式或自行使用者端。 接下來，提供應用程式名稱、網頁URL及授權重新導向URI的值， [!DNL Zoho CRM] 然後可以使用以授與Token來重新導向。

成功註冊會傳回您的使用者端ID和使用者端密碼。

### 建立授權請求

接下來，您必須建立 [授權請求](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) 使用網頁式應用程式或自我使用者端。 授權請求會傳回您的授與Token，讓您擷取存取Token。

建立授權請求時，您必須填寫兩者的值 **範圍** 和 **存取型別**. 請參閱此 [[!DNL Zoho CRM] 檔案](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) 以取得有關範圍的詳細資訊，而 **存取型別** 應一律設為 `offline`.

### 產生存取權並重新整理Token

擷取您的授權Token後，您就可以產生 [存取和重新整理Token](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) 向發出POST請求 `{ACCOUNTS_URL}/oauth/v2/token` 提供使用者端ID、使用者端密碼、授與權杖和重新導向URI時。 在此步驟中，您還必須包含 `grant_type` 作為引數，並將值設定為 `"authorization_code"`.

成功的請求會傳回您的存取和重新整理Token，然後您可使用它進行驗證。

如需取得認證的詳細步驟，請參閱 [[!DNL Zoho CRM] 驗證指南](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Connect [!DNL Zoho CRM] 至 [!DNL Platform] 使用API

以下檔案提供有關如何連線的資訊 [!DNL Zoho CRM] 使用API或使用者介面的to Platform：

- [建立 [!DNL Zoho CRM] 使用流量服務API的基礎連線](../../tutorials/api/create/crm/zoho.md)
- [使用Flow Service API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流量服務API為CRM來源建立資料流](../../tutorials/api/collect/crm.md)

## Connect [!DNL Zoho CRM] 至 [!DNL Platform] 使用UI

- [建立 [!DNL Zoho CRM] ui中的來源連線](../../tutorials/ui/create/crm/zoho.md)
- [在UI中為CRM來源連線建立資料流](../../tutorials/ui/dataflow/crm.md)

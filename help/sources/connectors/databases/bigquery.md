---
keywords: Experience Platform；首頁；熱門主題；BigQuery；bigquery；Google BigQuery；google bigquery
solution: Experience Platform
title: Google BigQuery來源聯結器概述
description: 瞭解如何使用API或使用者介面將Google BigQuery連線至Adobe Experience Platform。
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# [!DNL Google BigQuery]

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

[!DNL Experience Platform] 支援從第三方資料庫擷取資料。 Platform可以連線到不同型別的資料庫，例如關聯式、NoSQL或資料倉儲。 對資料庫提供者的支援包括 [!DNL Google BigQuery].

## IP位址允許清單

在使用來源聯結器之前，必須將IP位址清單新增至允許清單。 使用來源時，若未將您地區專屬的IP位址新增至允許清單，可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## 先决条件

下節提供建立之前所需的先決條件設定的進一步資訊 [!DNL Google BigQuery] 來源連線。

### 產生您的 [!DNL Google BigQuery] 認證

若要連線 [!DNL Google BigQuery] 若使用Platform，您必須產生下列認證的值：

| 認證 | 描述 |
| ---------- | ----------- |
| `project` | 專案是您的的基本層級組織實體。 [!DNL Google Cloud] 資源，包括 [!DNL Google BigQuery]. |
| `clientID` | 使用者端ID是 [!DNL Google BigQuery] OAuth 2.0認證。 |
| `clientSecret` | 使用者端密碼是您的密碼的另一半， [!DNL Google BigQuery] OAuth 2.0認證。 |
| `refreshToken` | 重新整理權杖可讓您取得API的新存取權杖。 存取Token的生命週期有限，可在您的專案期間過期。 您可以視需要使用重新整理權杖來驗證及請求專案的後續存取權杖。 |
| `largeResultsDataSetId` | 預先建立的  [!DNL Google BigQuery] 啟用大型結果集支援所需的資料集ID。 |

有關如何為產生OAuth 2.0憑證的詳細說明 [!DNL Google] API，請參閱下列內容 [[!DNL Google] OAuth 2.0驗證指南](https://developers.google.com/identity/protocols/oauth2).

## Connect [!DNL Google BigQuery] 至平台

以下檔案提供有關如何連線的資訊 [!DNL Google BigQuery] 使用API或使用者介面的to Platform：

### 使用API

- [使用Flow Service API建立Google BigQuery基本連線](../../tutorials/api/create/databases/bigquery.md)
- [使用Flow Service API探索資料表](../../tutorials/api/explore/tabular.md)
- [使用流程服務API為資料庫來源建立資料流](../../tutorials/api/collect/database-nosql.md)

### 使用UI

- [在使用者介面中建立Google BigQuery來源連線](../../tutorials/ui/create/databases/bigquery.md)
- [在UI中建立資料庫來源連線的資料流](../../tutorials/ui/dataflow/databases.md)

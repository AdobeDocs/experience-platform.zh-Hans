---
title: Adobe Experience Platform發行說明2021年9月
description: Adobe Experience Platform 2021年9月發行說明。
exl-id: 96375409-803f-45af-805e-900207d972e4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 8%

---

# Adobe Experience Platform 发行说明

**发布日期：2021 年 9 月 29 日**

Adobe Experience Platform 现有功能的更新包括：

- [数据引入](#ingestion)
- [[!DNL Data Prep]](#data-prep)
- [源](#sources)

## 数据引入 {#ingestion}

Adobe Experience Platform Data Ingestion代表Platform從各種來源擷取資料的多種方法，以及該資料如何儲存在Data Lake中，以供下游平台服務使用。

**新增功能**

| 功能 | 描述 |
|------- | -----------|
| 使用批次擷取更新插入或修補設定檔記錄 | 即時客戶個人檔案現在允許透過批次擷取，更新個別個人檔案記錄資料中的個人檔案屬性。 若要進一步瞭解，請參閱 [批次擷取開發人員指南](../../ingestion/batch-ingestion/api-overview.md). |

若要進一步瞭解將資料擷取至Platform，請造訪 [資料擷取檔案](../../ingestion/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 支援串流資料流 | 您現在可以在建立串流資料流時使用「資料準備」功能 [!DNL Amazon Kinesis]， [!DNL Azure Event Hubs]、和 [!DNL Google PubSub]. 請參閱教學課程，位置如下： [為雲端儲存空間來源建立串流資料流](../../sources/tutorials/ui/dataflow/streaming/cloud-storage-streaming.md) 以取得詳細資訊。 |

若要深入瞭解 [!DNL Data Prep] 請參閱 [[!DNL Data Prep] 概觀](../../data-prep/home.md).

## 源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

| 功能 | 描述 |
| --- | --- |
| [!DNL Data Landing Zone] | 您現在可以建立 [!DNL Data Landing Zone] 來源連線使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) 或 [使用者介面](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). [!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Platform布建的儲存體介面，可授予您存取安全、雲端式的檔案儲存設施，以將檔案帶入Platform。 請參閱 [[!DNL Data Landing Zone] 概觀](../../sources/connectors/cloud-storage/data-landing-zone.md) 以取得詳細資訊。 |
| [!DNL Snowflake] | 您現在可以建立 [!DNL Snowflake] 來源連線使用 [[!DNL Flow Service] API](../../sources/tutorials/api/create/databases/snowflake.md) 或 [使用者介面](../../sources/tutorials/ui/create/databases/snowflake.md) 將資料從您的 [!DNL Snowflake] 資料庫至平台。 請參閱 [[!DNL Snowflake] 概觀](../../sources/connectors/databases/snowflake.md) 以取得詳細資訊。 |
| [!DNL SFTP] 來源增強功能 | 您可以在建立連線埠時手動設定自訂連線埠號碼 [!DNL SFTP] 來源連線。 請參閱 [[!DNL SFTP] 概觀](../../sources/connectors/cloud-storage/sftp.md) 以取得詳細資訊。 |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md).

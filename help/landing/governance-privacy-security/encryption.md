---
title: Adobe Experience Platform中的資料加密
description: 瞭解如何在Adobe Experience Platform中加密傳輸中和閒置的資料。
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 3%

---

# Adobe Experience Platform中的資料加密

Adobe Experience Platform是功能強大且可擴充的系統，可集中化及標準化企業解決方案中的客戶體驗資料。 Platform使用的所有資料都會在傳輸和存放時加密，以確保您的資料安全。 本檔案主要說明Platform的加密程式。

下列程式流程圖說明如何擷取、加密及儲存資料 [!DNL Experience Platform]：

![](../images/governance-privacy-security/encryption/flow.png)

## 傳輸中的資料 {#in-transit}

Platform與任何外部元件之間傳輸的所有資料都會使用HTTPS透過安全、加密的連線進行 [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

一般而言，資料會透過三種方式帶入Platform：

* [資料彙集](../../collection/home.md) 功能可讓網站和行動應用程式將資料傳送至Platform Edge Network，以進行測試和擷取準備。
* [來源聯結器](../../sources/home.md) 從Adobe Experience Cloud應用程式和其他企業資料來源將資料直接串流到Platform。
* 非AdobeETL （擷取、轉換、載入）工具會將資料傳送至 [批次擷取API](../../ingestion/batch-ingestion/overview.md) 以利使用。

將資料帶入系統之後，以及 [已加密休息](#at-rest)之後，即可透過Platform服務加以擴充，並透過下列方式從系統中移除：

* [目的地](../../destinations/home.md) 可讓您啟用資料以Adobe應用程式和合作夥伴應用程式。
* 原生平台應用程式，例如 [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=zh-Hans) 和 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) 也可以使用資料。

## 靜態資料 {#at-rest}

Platform所擷取和使用的資料會儲存在Data Lake中，這是一個高度精細的資料存放區，包含系統管理的所有資料，無論來源或檔案格式為何。 儲存在資料湖中的所有資料都會經過加密、儲存，並在隔離環境中進行管理 [[!DNL Microsoft Azure Data Lake] 儲存](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) 貴組織專屬的例項。

如需如何在Azure Data Lake Storage中加密閒置資料的詳細資訊，請參閱 [Azure官方檔案](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## 后续步骤

本檔案提供Platform中資料加密方式的高層級概觀。 如需Platform安全性程式的詳細資訊，請參閱以下文章的概觀： [治理、隱私和安全性](./overview.md) Experience League時，或檢視 [平台安全性白皮書](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).

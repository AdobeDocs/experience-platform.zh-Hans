---
keywords: Experience Platform；首頁；熱門主題；目錄服務；目錄；目錄服務；目錄
solution: Experience Platform
title: 目錄服務API指南
description: 目錄服務API可讓開發人員管理Adobe Experience Platform中的資料集中繼資料。 参阅本指南，了解如何使用 API 执行关键操作。
exl-id: 812fcdae-ed0e-4f2b-84d7-26f2f79e71b9
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 3%

---

# [!DNL Catalog Service] API指南

[!DNL Catalog Service] 是Adobe Experience Platform中資料位置和譜系的記錄系統。 [!DNL Catalog] 充當中繼資料存放區或「目錄」，您可在其中找到有關您資料的資訊 [!DNL Experience Platform]，不需存取資料本身。 請參閱 [[!DNL Catalog] 概觀](../home.md) 以取得詳細資訊。

本開發人員指南提供步驟，協助您開始使用 [!DNL Catalog] API。 接著，指南會提供範例API呼叫，以使用執行關鍵作業 [!DNL Catalog].

## 先决条件

[!DNL Catalog] 在中追蹤多種資源與作業的中繼資料 [!DNL Experience Platform]. 本開發人員指南需要深入瞭解各種 [!DNL Experience Platform] 與建立和管理這些資源相關的服務：

* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Platform] 組織客戶體驗資料。
* [批次擷取](../../ingestion/batch-ingestion/overview.md)：如何 [!DNL Experience Platform] 從資料檔案擷取及儲存資料，例如CSV和Parquet。
* [串流擷取](../../ingestion/streaming-ingestion/overview.md)：如何 [!DNL Experience Platform] 從使用者端和伺服器端裝置即時擷取及儲存資料。

以下小節提供您需瞭解或掌握的其他資訊，才能成功呼叫 [!DNL Catalog Service] API。

## 讀取範例API呼叫

本指南提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭，以及正確格式化的請求裝載。 此外，也提供API回應中傳回的範例JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

## 收集必要標題的值

為了呼叫 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程後，會在所有標題中提供每個必要標題的值 [!DNL Experience Platform] API呼叫，如下所示：

* 授權：持有人 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 隔離至特定的虛擬沙箱。 的所有要求 [!DNL Platform] API需要標頭，用於指定將在其中執行操作的沙箱名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的標頭：

* Content-Type： application/json

## 以下專案的最佳實務 [!DNL Catalog] API呼叫

對「 」執行GET請求時 [!DNL Catalog] api的最佳作法是在您的要求中包含查詢引數，以便只傳回您需要的物件和屬性。 未篩選的請求可能會導致回應裝載的大小超過3GB，這會降低整體效能。

您可以在請求路徑中包含特定物件的ID來檢視這些物件，或使用查詢引數，例如 `properties` 和 `limit` 以篩選回應。 篩選器可作為標題和查詢引數傳遞，而作為查詢引數傳遞的篩選器優先。 檢視檔案： [篩選目錄資料](filter-data.md) 以取得詳細資訊。

由於某些查詢可能會對API造成大量負載，因此已在上實施全域限制 [!DNL Catalog] 以進一步支援最佳實務。

## 后续步骤

本檔案說明呼叫「 」所需的必要條件知識。 [!DNL Catalog] API。 您現在可以繼續本開發人員指南中提供的範例呼叫，並依照其指示操作。

本指南中的大多數範例都使用 `/dataSets` 端點，但原則可套用至內的其他端點 [!DNL Catalog] (例如 `/batches` 和 `/accounts`)。 請參閱 [目錄服務API參考](https://www.adobe.io/experience-platform-apis/references/catalog/) 以取得每個端點所有可用呼叫和作業的完整清單。

如需逐步工作流程，說明如何 [!DNL Catalog] API與資料擷取有關，請參閱以下主題的相關教學課程： [建立資料集](../datasets/create.md).

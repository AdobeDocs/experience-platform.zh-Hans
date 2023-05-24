---
keywords: Experience Platform；首頁；熱門主題；目錄服務；目錄；目錄服務；資料位置；資料位置；資料管理；資料管理；譜系；譜系；目錄；啟用資料集
solution: Experience Platform
title: 目錄服務概觀
description: 目錄服務是Adobe Experience Platform中資料位置和譜系的記錄系統。 雖然所有內嵌至Experience Platform的資料都會以檔案和目錄的形式儲存在Data Lake中，但Catalog仍會儲存這些檔案和目錄的中繼資料和說明，以供查閱和監視。
exl-id: ef0c173b-607b-41b8-8676-c54ae9472e23
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 5%

---

# [!DNL Catalog Service] 概述

[!DNL Catalog Service] 是Adobe Experience Platform中資料位置和譜系的記錄系統。 雖然所有資料已擷取至 [!DNL Experience Platform] 儲存在 [!DNL Data Lake] 作為檔案和目錄， [!DNL Catalog] 儲存這些檔案和目錄的中繼資料和說明，以供查閱和監視。

簡言之， [!DNL Catalog] 充當中繼資料存放區或「目錄」，您可在其中找到有關您資料的資訊 [!DNL Experience Platform]. 您可以使用 [!DNL Catalog] 回答下列問題：

* 我的資料位於何處？
* 此資料處於哪個處理階段？
* 哪些系統或程式對我的資料採取行動？
* 已成功處理多少資料？
* 處理期間發生什麼錯誤？

[!DNL Catalog] 提供RESTful API，可讓您以程式設計方式管理 [!DNL Platform] 使用基本CRUD作業的中繼資料。 請參閱 [目錄開發人員指南](api/getting-started.md) 以取得詳細資訊。

## [!DNL Catalog] 和 [!DNL Experience Platform] 服務

符合以下條件的資源： [!DNL Catalog Service] 多個曲目使用 [!DNL Experience Platform] 服務。 為了充分利用 [!DNL Catalog's] 功能，建議您熟悉這些服務及其互動方式 [!DNL Catalog].

### [!DNL Experience Data Model] (XDM)系統

[!DNL Experience Data Model] (XDM)系統是一種標準化的架構，其中 [!DNL Platform] 組織客戶體驗資料。 [!DNL Experience Platform] 運用XDM結構描述，以一致且可重複使用的方式描述資料結構。

當資料被擷取到 [!DNL Platform]，則該資料的結構會對映至XDM結構描述並儲存在 [!DNL Data Lake] 做為資料集的一部分。 每個資料集的中繼資料由追蹤 [!DNL Catalog Service]，其中包含資料集符合的XDM結構描述參考。

如需XDM系統的一般資訊，請參閱 [XDM系統總覽](../xdm/home.md).

### [!DNL Data Ingestion]

[!DNL Experience Platform] 從多個來源擷取資料，並將記錄作為資料集儲存在中 [!DNL Data Lake]. [!DNL Catalog] 追蹤這些資料集的中繼資料，無論其來源或擷取方法為何。

使用批次擷取方法時， [!DNL Catalog] 也會追蹤批次檔案的其他中繼資料。 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。[!DNL Catalog] 追蹤這些批次檔案的中繼資料，以及擷取後它們持續存在的資料集。 批次中繼資料包含有關成功擷取的記錄數，以及任何失敗記錄和關聯的錯誤訊息的資訊。

請參閱 [資料擷取概觀](../ingestion/home.md) 以取得詳細資訊。

## [!DNL Catalog] 物件

如上一節所述， [!DNL Catalog] 追蹤其他使用者使用的多種資源和作業的中繼資料 [!DNL Platform] 服務。 [!DNL Catalog] 會維護自己封裝此中繼資料的「物件」存放區。 [!DNL Catalog] 物件是可查詢的 [!DNL Platform] 可讓您搜尋、監控及標示資料，而不需要存取資料本身的資料。

下表概述支援的不同物件型別 [!DNL Catalog]：

| 对象 | API端點 | 定义 |
|---|---|---|
| 帐户 | `/accounts` | 建立來源連線時，必須提供驗證認證。 帳戶代表用來建立特定型別連線的驗證憑證集合。 每個連線都有一組唯一引數，這些引數會由儲存在 [!DNL Catalog] 並在以下位置提供保護： [!DNL Azure Key Vault]. |
| 批次 | `/batches` | 批量是由一个或多个要作为单个单位摄取的文件组成的数据单位。中的批次物件 [!DNL Catalog] 概述批次的擷取量度（例如處理的記錄數或磁碟大小），並且可能包含資料集、檢視和其他受批次作業影響的資源的連結。 |
| Connection | `/connections` | 連線是來源聯結器的單一執行個體，對您的組織而言是唯一的，並使用聯結器型別的適當驗證憑證進行設定。 |
| 连接器 | `/connectors` | 聯結器會定義來源連線如何從其他Adobe應用程式(例如Adobe Analytics和Adobe Audience Manager)、協力廠商雲端儲存空間(例如 [!DNL Azure Blob]， [!DNL Amazon S3]、FTP伺服器和SFTP伺服器)以及協力廠商CRM系統(例如 [!DNL Microsoft Dynamics] 和 [!DNL Salesforce])。 |
| 数据集 | `/dataSets` | 資料集是一種儲存和管理結構，用於收集包含方案（欄）和欄位（列）的資料（通常是表格）。 請參閱 [資料集總覽](./datasets/overview.md) 以取得詳細資訊。 |
| 資料集檔案 | `/datasetFiles` | 資料集檔案代表已儲存的資料區塊 [!DNL Platform]. 作為常值檔案的記錄，您可以在這裡找到檔案的大小、檔案包含的記錄數，以及對擷取檔案之批次的參照。 |

## 后续步骤

本檔案提供以下內容的簡介： [!DNL Catalog Service] 以及它如何在 [!DNL Experience Platform]. 請參閱 [[!DNL Catalog] 開發人員指南](api/getting-started.md) 有關與不同端點互動的步驟 [!DNL Catalog] API。 建議您也參閱以下專案的指南： [篩選目錄資料](api/filter-data.md) 以遵循最佳實務來限制API回應中傳回的資料。

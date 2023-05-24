---
title: Adobe Experience Platform發行說明2021年1月
description: Adobe Experience Platform的2021年1月發行說明。
doc-type: release notes
last-update: January 27, 2021
author: ens60013
exl-id: 6fb92e35-922c-47ba-8cf4-44edd92acfa1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 5%

---

# Adobe Experience Platform 发行说明

**发行日期：2021 年 1 月 27 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 規則運算式函式 | [!DNL Data Prep] 對應程式現在支援根據規則運算式比對及擷取部分輸入欄位。 |

如需詳細資訊，請參閱 [[!DNL Data Prep] 概觀](../../data-prep/home.md).

## 目标 {#destinations}

[!DNL Destinations] 是預先建立的與目標平台的整合，可無縫啟用Adobe Experience Platform的資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。

**新目的地**

| 目标 | 描述 |
| ----------- | ----------- |
| [!DNL Azure Blob] | [!DNL Azure Blob] 是Microsoft的雲端物件儲存解決方案。 |

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 進階識別碼比對 | 中的受眾符合率功能增強 [!DNL Facebook Custom Audiences] 和 [!DNL Google Customer Match]，即可新增對其他身分比對的支援，例如外部ID、電話號碼和行動裝置ID。 如需更多詳細資訊，請參閱下列檔案： <ul><li>[facebook目的地](../../destinations/catalog/social/facebook.md)</li><li>[Google Customer Match目的地](../../destinations/catalog/advertising/google-customer-match.md)</li><li>[啟用串流區段匯出目的地的受眾資料](../../destinations/ui/activate-segment-streaming-destinations.md)</li></ul> |

若要進一步瞭解，請造訪 [目的地概觀](../../destinations/home.md).

## 实时客户资料 {#profile}

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，無論客戶在哪裡或何時與您的品牌互動。 透過即時客戶個人檔案，您可以檢視結合來自多個管道（包括線上、離線、CRM和第三方資料）之資料的每個個別客戶的整體檢視。 [!DNL Profile] 可讓您將客戶資料合併成統一的檢視，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 從設定檔存放區中刪除資料集 | 當您從Experience Platform資料湖中刪除資料集時，該資料集也會自動從設定檔存放區中刪除。 您不再需要使用設定檔系統作業API端點來提出刪除請求，以明確從設定檔存放區中刪除資料集。 如需詳細資訊，請參閱 [設定檔系統作業API端點指南](../../profile/api/profile-system-jobs.md). |
| 特定區段的估計ID名稱空間計數 | 對於預估的設定檔計數，預覽API現在會報告：<ul><li>指定名稱空間之區段中的預估設定檔總數。</li><li>在指定名稱空間的設定檔聯合結構描述中預估的設定檔總數。</li></ul>若要進一步瞭解，請參閱 [設定檔預覽API端點指南](../../profile/api/preview-sample-status.md). |

如需即時客戶個人檔案的詳細資訊，包括使用的教學課程和最佳實務 [!DNL Profile] 資料，請先閱讀 [即時客戶個人檔案總覽](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| Adobe Audience Manager來源聯結器增強功能 | 您現在可以從Audience Manager中篩選及選取個別的第一方區段，以擷取至Platform，並篩選掉第一方特徵。 請參閱教學課程，位置如下： [建立Audience Manager來源聯結器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) 以取得詳細資訊。 |
| [!DNL Google BigQuery] 來源聯結器增強功能 | 您現在可以使用將大於10GB的檔案內嵌於單一資料流執行 [!DNL BigQuery] 來源聯結器。 請參閱 [[!DNL BigQuery] 來源聯結器概述](../../sources/connectors/databases/bigquery.md) 以取得詳細資訊。 |
| 支援雲端儲存的複雜資料型別 | 現在使用雲端儲存空間來源聯結器時，您可以內嵌複雜的資料型別，例如JSON檔案中的陣列。 請參閱有關建立雲端儲存資料流的教學課程 [在UI中](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 或 [使用 [!DNL Flow Service] API](../../sources/tutorials/api/collect/cloud-storage.md) 以取得詳細資訊。 |
| 支援以下專案的服務主體金鑰型驗證： [!DNL Microsoft Dynamics] source | 您現在可以驗證您的 [!DNL Dynamics] 使用服務主體金鑰作為密碼式驗證替代的帳戶。 請參閱 [[!DNL Dynamics] 來源聯結器概述](../../sources/connectors/crm/ms-dynamics.md) 以取得詳細資訊。 |
| 雲端儲存空間來源中的自訂分隔符號的UI支援 | 您現在可以設定自訂欄分隔符號，例如逗號(`,`)，標籤(`\t`)或垂直號(`|`)，以在UI中收集分隔檔案。 請參閱教學課程，位置如下： [使用雲端儲存空間來源聯結器建立資料流](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) 以取得詳細資訊 |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md).

---
title: Adobe Experience Platform發行說明2020年3月
description: Adobe Experience Platform的2020年3月發行說明。
doc-type: release notes
last-update: March 10, 2020
author: ens71067
keywords: 发行说明;
exl-id: 407c2bac-4c8a-4939-b3dd-788250f15650
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发布日期：2020 年 3 月 11 日**

Adobe Experience Platform 现有功能的更新包括：

* [数据治理](#governance)
* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Destinations]](#destinations)
* [[!DNL Identity Service]](#identity)
* [[!DNL Sources]](#sources)

## 数据治理 {#governance}

[!DNL Experience Platform] 可讓公司整合來自多個企業系統的資料，讓行銷人員更能識別、瞭解客戶並與客戶互動。 [!DNL Experience Platform] 包括端對端的資料控管基礎架構，以確保資料在 [!DNL Platform] 在系統之間共用時。

Adobe Experience Platform資料控管是用於管理客戶資料並確保遵守適用於資料使用的法規、限制和政策的一系列策略與技術。 它在以下方面發揮著關鍵作用 [!DNL Experience Platform] 包括目錄、資料譜系、資料使用標籤、資料存取原則，以及行銷動作資料的存取控制。

**新增功能**

>[!NOTE]
>
>以下部分新功能目前為測試版，並未開放所有使用者使用。 Beta版功能可能會有變動。

| 功能 | 描述 |
| ------- | ----------- |
| 自動強制資料使用原則 [!DNL Real-Time Customer Data Platform] | 在啟用資料至目的地的工作流程中，現在會強制執行資料使用原則。 資料控管也會內嵌在並對現有啟用產生影響時（例如變更資料集標籤、合併原則、區段定義等），強制執行。 |
| 用於強制執行的資料譜系 | 在Real-Time CDP中違反資料使用原則時，UI會顯示包含資料譜系資訊的通知，以協助使用者瞭解違反原則的原因以及他們可以採取哪些行動來解決違規。 |


**已知问题**

* None

如需資料控管的詳細資訊，請參閱 [資料控管概觀](../../data-governance/home.md).

## 数据引入 {#ingestion}

Adobe Experience Platform提供豐富的功能，可擷取任何型別和延遲的資料。 Adobe Experience Platform [!DNL Data Ingestion] 提供多種擷取資料的替代方案，包括批次API、串流API、原生Adobe聯結器、資料整合合作夥伴或Adobe Experience Platform UI。

**新增功能**

| 功能 | 描述 |
|------- | -----------|
| 部分批次擷取 | 部分批次擷取是擷取包含錯誤的資料的能力，上限為特定臨界值。 透過此功能，使用者可成功將其所有正確資料擷取到Adobe Experience Platform，同時將其所有不正確的資料單獨分批處理。 會將詳細資料新增至失敗的批次，以說明這些批次未通過驗證的原因。 如需部分批次擷取的詳細資訊，請參閱 [部分批次擷取檔案](../../ingestion/batch-ingestion/partial.md). |

**已知问题**

* None

若要進一步瞭解將資料擷取至Platform，請造訪 [資料擷取檔案](../../ingestion/home.md).


## 目标 {#destinations}

在 [Real-time Customer Data Platform](../../rtcdp/overview.md)，目的地是預先建立的與目的地平台的整合，可透過順暢的方式為這些合作夥伴啟用資料。

**新目的地**

有新的目的地可供您啟用Adobe Experience Platform資料。 如需詳細資訊，請參閱下文：

| 目标 | 描述 |
|--- | ---|
| 雲端儲存空間目的地 | Real-Time CDP現在可以將區段以資料檔案的形式傳送至您的 [!DNL Amazon S3] 或SFTP雲端儲存位置。 這可讓您透過CSV或定位字元分隔檔案，將對象及其設定檔屬性傳送至您的內部系統。 |
| 廣告目的地 | 此 [!DNL Google] 目的地卡現在分割為三個目的地卡（針對三個不同的目的地卡） [!DNL Google] Real-Time CDP目前支援的平台： [!DNL Google Ads]， [!DNL Google Ad Manager]， [!DNL Google] 顯示和視訊360。 |

若要進一步瞭解，請造訪 [目的地概觀](../../destinations/home.md)

## [!DNL Identity Service] {#identity}

提供相關的數位體驗需要完全瞭解您的客戶。 當您的客戶資料分散於不同的系統時，這會使情況更困難，導致每個個別客戶似乎有多個「身分」。

Adobe Experience Platform [!DNL Identity Service] 透過跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，協助您更好地瞭解客戶及其行為。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 增強式私密圖表 | 已增強專用圖表功能，將圖表產生延遲從每週批次程式縮短為每日重新整理圖表，允許 [!DNL Identity Service] 客戶存取更多最新的身分圖表和連結。 |

**已知问题**

* None

如需有關的詳細資訊 [!DNL Identity Service]，請參閱 [Identity Service概觀](../../identity-service/home.md).

## 源 {#sources}

Adobe Experience Platform可從外部來源內嵌資料，同時允許您使用建構、加標籤及增強該資料 [!DNL Platform] 服務。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

[!DNL Experience Platform] 提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| Adobe Audience Manager聯結器已棄用的訊號 | 將不再傳送來自Audience Manger的訊號層級資料。 請注意，仍會包含特徵和區段的區段會籍。 由於此變更，將不再產生傳入資料集。 |
| 已重新命名資料集 | Audience Manger聯結器產生的資料集將具有更新的名稱和說明。 |
| 啟用 [!DNL Profile] 在Audience Manger中切換 | [!DNL Profile] 可啟用或停用切換以將資料集提升至 [!DNL Real-Time Customer Profile]. 切換預設為啟用。 |
| 雲端儲存系統的UI支援 | 新的來源聯結器 [!DNL Azure Data Lake Storage Gen2] 在UI中。 |
| CRM系統的UI支援 | 新的來源聯結器 [!DNL HubSpot]， [!DNL Salesforce Service Cloud]、和 [!DNL ServiceNow] 在UI中。 |
| 資料庫系統的UI支援 | 新的來源聯結器 [!DNL AWS Redshift]， [!DNL Google BigQuery]， [!DNL MariaDB]， [!DNL Microsoft SQL Server]、和 [!DNL MySQL] 在UI中。 |

**已知问题**

* None

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md).

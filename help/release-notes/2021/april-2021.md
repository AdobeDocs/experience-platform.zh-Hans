---
title: Adobe Experience Platform發行說明2021年4月
description: Adobe Experience Platform 2021年4月發行說明。
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: cc78e48a-3578-4c55-ae86-1946d62bddb9
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 12%

---

# Adobe Experience Platform 发行说明

**发布日期：2021 年 4 月 21 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支援編輯現有資料流的對應 | 您現在可以更新現有資料流的對應集。 您無法更新排程為一次內嵌之資料流的對應集。 HTTP API、Adobe Analytics、Adobe Audience Manager和伺服器不支援此功能 [!DNL Marketo Engage]. 如需詳細資訊，請參閱以下教學課程： [在UI中更新來源資料流程](../../sources/tutorials/ui/update-dataflows.md). |
| 支援串流擷取 | 您現在可以在建立串流來源連線時使用資料準備功能。 如需詳細資訊，請參閱以下教學課程： [在使用者介面中建立串流來源連線](../../sources/tutorials/ui/create/streaming/http.md). |

如需詳細資訊，請參閱 [[!DNL Data Prep] 概觀](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

Experience Data Model (XDM)是開放原始碼規格，旨在改善數位體驗的力量。 它為任何應用程式提供通用結構和定義，以便與Adobe Experience Platform上的服務通訊。 藉由遵守XDM標準，所有客戶體驗資料都可以整合到通用表示中，以更快、更整合的方式提供深入分析。 您可以從客戶動作獲得有價值的深入分析、透過區段定義客戶對象，以及使用客戶屬性進行個人化。

| 功能 | 描述 |
| --- | --- |
| 依產業區分的結構描述建議 | 在結構描述編輯器UI中選取類別和結構描述欄位群組時，您可以使用新的篩選器來根據您的特定產業檢視建議的標準元件。 請參閱以下說明檔案： [產業資料模型](https://www.adobe.com/go/xdm-industry-erds-en) 以取得有關不同產業使用案例中這些元件如何相互關聯的詳細資訊。 |

## [!DNL Intelligent Services] {#intelligent-services}

Intelligent Services可讓行銷分析師和從業人員運用客戶體驗使用案例中人工智慧和機器學習的強大功能。 借助此功能，营销分析人员可使用商业级别配置来设置特定于公司需求的预测，而无需具备数据科学专业知识。

### Customer AI

Real-time Customer Data Platform中提供的Customer AI可產生自訂傾向評分，例如大規模個別設定檔的流失和轉換情形。 这无需通过将业务需求转变为机器学习问题、选择算法、培训或部署即可完成。

| 功能 | 描述 |
| ------- | ----------- |
| 支援Adobe Analytics資料 | 更新功能，透過Analytics來源聯結器支援Adobe Analytics資料集，無需ETL您的資料，以符合消費者體驗事件(CEE)結構描述。 |
| 支援Adobe Audience Manager資料 | 更新功能，透過Audience Manager來源聯結器支援Adobe Audience Manager資料集，無需ETL您的資料，以符合消費者體驗事件(CEE)結構描述。 |
| 模型效能摘要 | Customer AI現在擁有 [模型效能摘要標籤](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) 在「服務執行個體分析」頁面中。 模型效能索引標籤會顯示所有實際轉換率和流失率。 這可讓您解密並瞭解每個傾向值區中發生的事情。 |

如需支援資料集的詳細資訊，請參閱 [[!DNL Intelligent Services] 資料準備檔案](../../intelligent-services/data-preparation.md).

### 归因人工智能

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户旅程中每个营销接触点的营销影响。

| 功能 | 描述 |
| ------- | ----------- |
| 支援Adobe Analytics資料 | 更新功能，透過Analytics來源聯結器支援Adobe Analytics資料集，無需ETL您的資料，以符合消費者體驗事件(CEE)結構描述。 |

如需支援資料集的詳細資訊，請參閱 [[!DNL Intelligent Services] 資料準備檔案](../../intelligent-services/data-preparation.md).

## 分段服务 {#segmentation}

Adobe Experience Platform Segmentation Service提供使用者介面和RESTful API，可讓您建立區段並從 [!DNL Real-Time Customer Profile] 資料。 這些區段會集中設定並維護在Platform上，讓任何Adobe應用程式都能輕鬆存取。

[!DNL Segmentation Service] 透過描述可區分客戶群內可銷售人員群組的條件，來定義設定檔的特定子集。 區段能以記錄資料（例如人口資訊）或代表客戶與品牌互動的時間序列事件為基礎。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 其他彙總函式 | 區段產生器中已新增計數函式。 計數函式可讓您計算指定事件的完成次數。 如需有關計數函式的詳細資訊，請參閱 [區段產生器指南](../../segmentation/ui/segment-builder.md#count-functions) |

如需詳細資訊，請參閱 [!DNL Segmentation Service]，請參閱 [區段概觀](../../segmentation/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

| 功能 | 描述 |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | 您現在可以建立 [!DNL Marketo Engage] 來源連線使用UI，將B2B資料帶到Platform，並使用平台連線的應用程式保持這些資料在最新狀態。 如需詳細資訊，請參閱 [[!DNL Marketo Engage] 來源聯結器檔案](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| Beta版來源移至GA | 下列來源已從Beta版升級至GA版： <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md).

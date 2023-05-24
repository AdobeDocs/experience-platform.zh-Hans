---
title: Adobe Experience Platform發行說明2022年8月
description: Adobe Experience Platform的2022年8月發行說明。
exl-id: dbf1e7a3-8599-4991-8932-f57d3b1c640d
source-git-commit: edd285c3d0638b606876c015dffb18309887dfb5
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发行日期：2022 年 8 月 24 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [體驗資料模型(XDM)](#xdm)
- [实时客户资料](#profile)
- [分段服务](#segmentation)
- [源](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML服務可讓行銷分析師和從業人員運用客戶體驗使用案例中人工智慧和機器學習的力量。 這可讓行銷分析人員使用商業層級的設定，針對公司的需求設定模型，而不需要資料科學的專業知識。

### 归因人工智能

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户旅程中每个营销接触点的营销影响。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 隱私權支援 | <ul><li> Attribution AI現在支援定義使用者角色和存取原則，以便管理 [許可權](../../../help/access-control/abac/ui/permissions.md) 產品應用程式內的功能和物件。 </li><li>當活動發生時，會自動記錄稽核記錄資源。</li><li> 到 [基於屬性的存取控制](../../access-control/abac/overview.md)，管理員可以根據特定屬性控制對特定物件和/或權能的存取，這些屬性可以是新增到物件的中繼資料，例如標籤。管理員也可以定義只有特定欄位和對應至這些欄位之資料存取權的使用者角色。</li><li>Attribution AI會利用Platform資料集。 為支援品牌可能收到的消費者權利請求，品牌應使用平台Privacy Service提交消費者存取和刪除請求，以透過Data Lake、Identity Service和即時客戶設定檔移除其資料。  </li><li>所有用於模型輸入/輸出的資料集都將遵循Platform准則。 平台資料加密適用於待用和傳輸中的資料。 請參閱檔案以深入瞭解 [資料加密](../../../help/landing/governance-privacy-security/encryption.md).</li></ul> |

{style="table-layout:auto"}

**注意**：在進一步通知之前，現有Healthcare Shield客戶將無法使用Attribution AI。

如需Attribution AI的詳細資訊，請參閱 [Attribution AI](../../intelligent-services/attribution-ai/overview.md) 概述。

### Customer AI

Real-time Customer Data Platform中提供的Customer AI可產生自訂傾向評分，例如大規模個別設定檔的流失和轉換情形。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 隱私權支援 | <ul><li> Customer AI現在支援定義使用者角色和存取原則，以便管理 [許可權](../../../help/access-control/abac/ui/permissions.md) 產品應用程式內的功能和物件。 </li><li>當活動發生時，會自動記錄稽核記錄資源。</li><li> 到 [基於屬性的存取控制](../../access-control/abac/overview.md)，管理員可以根據特定屬性控制對特定物件和/或權能的存取。 这些属性可以是添加到对象的元数据，如标签。管理員也可以定義只有對應至特定欄位和資料之存取權的使用者角色。</li><li>Customer AI可運用Platform資料集。 為支援品牌可能收到的消費者權利請求，品牌應使用平台Privacy Service提交消費者存取和刪除請求，以透過Data Lake、Identity Service和即時客戶設定檔移除其資料。 </li><li>所有用於模型輸入/輸出的資料集都將遵循Platform准則。 平台資料加密適用於待用和傳輸中的資料。 請參閱檔案以深入瞭解 [資料加密](../../../help/landing/governance-privacy-security/encryption.md).</li></ul> |

{style="table-layout:auto"}

**注意**：現有Healthcare Shield客戶將無法使用Customer AI，直到另行通知為止。

如需Customer AI的詳細資訊，請參閱 [Customer AI](../../intelligent-services/customer-ai/overview.md) 概述。

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供多個 [!DNL dashboards] 您可以透過它檢視有關您組織資料的重要深入分析，如每日快照期間所擷取。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 排定的啟用Widget | 此 [!UICONTROL 已排程的啟用] Widget以表格化方式提供最近啟用目的地的檢視。 每個區段都包含名稱、目的地平台，以及啟動開始和結束日期。 此Widget可讓您一目瞭然地發現正在啟用對象的位置和時間，並讓重複或不必要的啟用更加透明。 此累積資訊也會反白標示任何啟用被遺漏的位置。 |

如需詳細資訊，請參閱 [!DNL Dashboards]，請參閱 [[!DNL Dashboards] 概觀](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支援擷取有警告的記錄 | 「資料準備」現在會將警告（非嚴重錯誤）當地語系化至欄位，並允許擷取列的其餘部分。 現在，所有對應程式轉換錯誤都會回報為警告，而部分擷取的列會被視為成功，但有警告。  含有警告和診斷詳細資訊的記錄也支援監視。 部分擷取有警告的記錄目前僅適用於串流資料。 檢閱以下專案的檔案： [擷取有警告的記錄](../../sources/tutorials/ui/monitor-streaming.md) 以取得詳細資訊。 |

{style="table-layout:auto"}

若要深入瞭解 [!DNL Data Prep]，請參閱 [[!DNL Data Prep] 概觀](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先建立的與目標平台的整合，可無縫啟用Adobe Experience Platform的資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。

**新功能或更新功能**

| 功能 | 描述 |
| ----------- | ----------- |
| （測試版）個人化目的地的屬性型個人化支援 | 隨著屬性型個人化測試版的推出，您將會在 [目的地目錄](../../destinations/catalog/overview.md)： <ul><li>**[!UICONTROL Adobe Target V2]**：此聯結器目前為測試版，僅供特定數量的客戶使用。 除了Adobe Target V1卡提供的功能外，Target V2聯結器還新增了 [對應步驟](/help/destinations/ui/activate-profile-request-destinations.md#map-attributes) 至啟用工作流程，可讓您將設定檔屬性對應至Adobe Target，啟用以屬性為基礎的相同頁面和下一頁個人化。</li><li>**[!UICONTROL 使用屬性自訂個人化]**：此聯結器目前為測試版，僅供特定數量的客戶使用。 除了 **[!UICONTROL 自訂個人化]**，則 **[!UICONTROL 使用屬性自訂個人化]** 聯結器新增選購專案 [對應步驟](../../destinations/ui/activate-profile-request-destinations.md#map-attributes) 至啟用工作流程，可讓您將設定檔屬性對應至自訂個人化目的地，啟用以屬性為基礎的相同頁面和下一頁個人化。</li></ul> <br> 設定檔屬性可能包含敏感資料。 為了保護此資料， **[!UICONTROL 使用屬性自訂個人化]** 目的地要求您使用 [Edge Network Server API](../../server-api/overview.md) 用於資料彙集。 此外，所有伺服器API呼叫都必須在 [已驗證的內容](../../server-api/authentication.md). |

{style="table-layout:auto"}

**新目的地**

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/) 是一個銷售執行平台，擁有全球最豐富的B2B買方與賣方互動資料，並在專有AI技術方面投入巨資，以將銷售資料轉換為情報。 [!DNL Outreach] 協助組織自動化銷售參與度並據以行動實現收入情報，以改善其效率、可預測性和成長。 |

{style="table-layout:auto"}

如需有關目的地的詳細一般資訊，請參閱 [目的地概觀](../../destinations/home.md).

## 體驗資料模型(XDM) {#xdm}

XDM是開放原始碼規格，針對帶入Adobe Experience Platform的資料提供通用結構和定義（結構描述）。 藉由遵守XDM標準，所有客戶體驗資料都可以整合到通用表示中，以更快、更整合的方式提供深入分析。 您可以從客戶動作獲得有價值的深入分析、透過區段定義客戶對象，以及使用客戶屬性進行個人化。

**新XDM元件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 类 | [[!UICONTROL AJO實體類別]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity.schema.json) | 用於建立Adobe Journey Optimizer查閱結構描述的記錄型類別。 |
| 字段组 | [[!UICONTROL Workfront工作物件]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | 參考Adobe Workfront所有較低層級物件特定欄位群組的包裝函式欄位群組。 |

{style="table-layout:auto"}

**已更新XDM元件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 字段组 | [[!UICONTROL Journey Orchestration步驟事件常見欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | 已新增兩個新屬性： `origTimeStamp` 和 `experienceID`. |
| 字段组 | [[!UICONTROL 區段會籍細節]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | 除了 [!UICONTROL XDM個別設定檔]，此欄位群組現在也可用於根據XDM商業帳戶類別的結構描述。 |
| 字段组 | （多個） | 與Marketo B2B活動相關的數個欄位群組已更新為穩定狀態。 請參閱下列內容 [提取請求](https://github.com/adobe/xdm/pull/1593/files) 以取得詳細資訊。 |
| 字段组 | （多個） | 已更新數個與天氣相關的欄位群組，以修正下列專案發生的錯誤： `uvIndex` 和 `sunsetTime`. 請參閱下列內容 [提取請求](https://github.com/adobe/xdm/pull/1602/files) 以取得詳細資訊。 |
| 資料型別 | [[!UICONTROL 產品清單專案]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 新屬性 `productImageUrl` 已新增。 |
| 資料型別 | [[!UICONTROL Qoe資料詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 新屬性 `framesPerSecond` 已新增。 |
| 資料型別 | [[!UICONTROL 工作階段詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` 已更名为 `appVersion`。`meta:enum` 和 `description` 欄位也已更新。 |
| 資料型別和欄位群組 | （多個） | 數個媒體資料型別和欄位群組有新欄位和更新的說明。 請參閱下列內容 [提取請求](https://github.com/adobe/xdm/pull/1582/files) 以取得詳細資訊。 |
| (全部) | （多個） | 所有包含 `enum` 欄位現在也包含對應的 `meta:enum` 表示每個限制之顯示值的欄位。 請參閱下列內容 [提取請求](https://github.com/adobe/xdm/pull/1601/files) 以取得詳細資訊。 |

{style="table-layout:auto"}

如需有關Platform中XDM的詳細資訊，請參閱 [XDM系統總覽](../../xdm/home.md).

## 实时客户资料 {#profile}

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，無論客戶在哪裡或何時與您的品牌互動。 透過即時客戶個人檔案，您可以檢視結合來自多個管道（包括線上、離線、CRM和第三方資料）之資料的每個個別客戶的整體檢視。 設定檔可讓您將客戶資料整合到統一的檢視中，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

| 功能 | 描述 |
| ------- | ----------- |
| 合併原則硬性限制 | Platform現在將強制執行 **五** 每個沙箱的合併原則。 如果您的沙箱目前有超過五個合併原則，您將 **not** 能夠建立新的合併原則，直到沙箱具有少於五個合併原則為止。 |
| 孤立的設定檔邊緣屬性清理 | 對於所有組織，設定檔服務現在會每天移除使用者活動區域的剩餘邊緣屬性，以在系統中更準確地表示您的設定檔。 此清理會在刪除給定設定檔的所有設定檔片段後發生，並且應該會影響從以下資料集中合併的設定檔： `com_adobe_aep_profile_region_dataset` 標籤為 `true`. 授權使用儀表板中的「可定址對象」量度可能會下降，而設定檔儀表板中的「設定檔計數」量度可能會下降，因為這些量度包含此版本之前的剩餘邊緣屬性片段。 |

{style="table-layout:auto"}

若要進一步瞭解即時客戶個人檔案，包括使用個人檔案資料的教學課程和最佳實務，請先閱讀 [即時客戶個人檔案總覽](../../profile/home.md).

## 分段服务 {#segmentation}

[!DNL Segmentation Service] 透過描述可區分客戶群內可銷售人員群組的條件，來定義設定檔的特定子集。 區段能以記錄資料（例如人口資訊）或代表客戶與品牌互動的時間序列事件為基礎。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支援4000個區段 | 所有使用Platform的組織現在最多可支援4000個區段定義。 如需此變更如何影響區段工作API的詳細資訊，請參閱 [區段作業端點指南](../../segmentation/api/segment-jobs.md) |

如需詳細資訊，請參閱 [!DNL Segmentation Service]，請參閱 [區段概觀](../../segmentation/home.md).

## 源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 自助式來源的一般可用性（批次SDK） | 開發、測試和整合您的REST API型資料來源，以使用易於設定的來源規格將批次資料擷取到Experience Platform。 使用Sources SDK，您可以： <ul><li>設定Experience Platform目錄的新來源。</li><li>定義來源的規格，包括與支援的驗證型別、排程和如何擷取資源資料相關的資訊。</li><li>為您的新來源建立使用者導向的檔案。</li></ul> 如需詳細資訊，請閱讀以下檔案： [自助來源（批次SDK）](../../sources/sources-sdk/overview.md). |
| 正式發行 [!DNL Google BigQuery] source | 使用 [!DNL Google BigQuery] 從您的擷取資料的來源 [!DNL Google BigQuery] Data Warehouse至Experience Platform。 如需詳細資訊，請參閱以下連結的相關檔案： [[!DNL Google BigQuery] source](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] 來源（測試版） | 使用 [!DNL Teradata Vantage] 從混合多雲端環境擷取資料至Experience Platform的來源。 如需詳細資訊，請參閱以下連結的相關檔案： [[!DNL Teradata Vantage] source](../../sources/connectors/databases/teradata-vantage.md). |
| Adobe Analytics來源的跨區域支援 | 您现在可以接收来自任何地区（美国、英国或新加坡）的报告包。 報告套裝必須對應至與來源連線所在的Experience Platform沙箱例項相同的組織。 如需詳細資訊，請閱讀以下指南： [在使用者介面中建立Adobe Analytics來源連線](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style="table-layout:auto"}

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md).

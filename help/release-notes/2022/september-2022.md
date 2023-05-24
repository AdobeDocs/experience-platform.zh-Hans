---
title: Adobe Experience Platform發行說明2022年9月
description: Adobe Experience Platform 2022年9月版本注意事項。
exl-id: a7a4dcf8-2cf3-4e39-879d-bdfcbacb737a
source-git-commit: 8904d44cc8d289d103ec6d65116b8385ed615c4d
workflow-type: tm+mt
source-wordcount: '2940'
ht-degree: 5%

---

# Adobe Experience Platform 发行说明

**发布日期：2022 年 9 月 28 日**

Adobe Experience Platform中的新功能：

- [基于属性的访问控制](#abac)

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [审核日志](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [資料彙集](#data-collection)
- [目标](#destinations)
- [體驗資料模型(XDM)](#xdm)
- [Identity Service](#identity-service)
- [查询服务](#query-service)
- [源](#sources)

## 基于属性的访问控制 {#abac}

>[!IMPORTANT]
>
>以屬性為基礎的存取控制將從2022年10月開始啟用。 如果您想要成為率先採用者，請聯絡您的Adobe代表。

以屬性為基礎的存取控制是Adobe Experience Platform的一項功能，可讓注重隱私權的品牌在管理使用者存取許可權時擁有更大的彈性。 可將個別物件（例如結構描述欄位和區段）指派給使用者角色。 此功能可讓您為貴組織中的特定Platform使用者授予或撤銷個別物件的存取權。

透過屬性型存取控制，貴組織的管理員可控制使用者對所有Platform工作流程與資源的機密個人資料(SPD)、個人識別資訊(PII)及其他自訂資料型別的存取。 管理員可以定義僅能存取特定欄位的使用者角色，以及對應至這些欄位的資料。

| 功能 | 描述 |
| --- | --- |
| 基于属性的访问控制 | 屬性型存取控制可讓您使用可定義組織或資料使用範圍的標籤，來標籤Experience Data Model (XDM)結構描述欄位和區段。 同時，管理員可以使用使用者和角色管理介面來定義涵蓋XDM結構描述欄位和區段的存取原則，以便更好地管理使用者或使用者群組（內部、外部或第三方使用者）的存取許可權。 如需詳細資訊，請參閱 [屬性型存取控制概觀](../../access-control/abac/overview.md). |
| 权限 | 許可權是Experience Cloud的區域，管理員可以在其中定義使用者角色和存取原則，以管理產品應用程式內功能和物件的存取許可權。 透過許可權，您可以建立和管理角色、為這些角色指派所需的資源許可權，以及建立原則以運用標籤，並定義哪些使用者角色有權存取特定Platform資源。 权限还允许您管理与特定角色关联的标签、沙盒和用户。如需詳細資訊，請參閱 [許可權UI指南](../../access-control/abac/ui/browse.md). |

如需以屬性為基礎的存取控制的詳細資訊，請參閱 [屬性型存取控制概觀](../../access-control/abac/overview.md). 如需以屬性為基礎的存取控制工作流程的完整指南，請閱讀 [屬性型存取控制端對端指南](../../access-control/abac/end-to-end-guide.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML服務可讓行銷分析師和從業人員運用客戶體驗使用案例中人工智慧和機器學習的力量。 這可讓行銷分析人員使用商業層級的設定，針對公司的需求設定模型，而不需要資料科學的專業知識。

### 归因人工智能

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户旅程中每个营销接触点的营销影响。

| 功能 | 描述 |
| --- | --- |
| 儲存草稿執行個體 | 此新功能可讓行銷分析師將模型設定儲存為草稿執行個體，並繼續編輯直到完成訓練和評分為止。 此功能有用的情況包括：使用者在工作流程中有多個要定義的欄位，但由於時間限制而無法完成。 另一個案例是正在處理一個或多個資料集統計資料，但還不能使用。 閱讀 [Attribution AI使用手冊](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) 以深入瞭解。 |
| 治理原則 | 使用者透過設定工作流程提交以建立執行個體後，新的原則執行服務會檢查是否有任何違反資料使用的原則並在彈出視窗中顯示詳細資訊。 它可確保資料作業和行銷動作符合Adobe Experience Platform上設定的資料使用原則。 |

如需Attribution AI的詳細資訊，請參閱 [Attribution AI概觀](../../intelligent-services/attribution-ai/overview.md). 如需資料控管原則的資訊，請閱讀 [原則概觀](../../data-governance/policies/overview.md).

### Customer AI

Real-time Customer Data Platform中提供的Customer AI可產生自訂傾向評分，例如大規模個別設定檔的流失和轉換情形。

| 功能 | 描述 |
| --- | --- |
| 儲存草稿執行個體 | 此新功能可讓行銷分析師將模型設定儲存為草稿執行個體，並繼續編輯直到完成訓練和評分為止。 此功能有用的情況包括：使用者在工作流程中有多個要定義的欄位，但由於時間限制而無法完成。 另一個案例是正在處理一個或多個資料集統計資料，但還不能使用。 閱讀 [Customer AI使用手冊](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) 以深入瞭解。 |
| 治理原則 | 使用者透過設定工作流程提交以建立執行個體後，新的原則執行服務會檢查是否有任何違反資料使用的原則並在彈出視窗中顯示詳細資訊。 它可確保資料作業和行銷動作符合Adobe Experience Platform上設定的資料使用原則。 |

如需Customer AI的詳細資訊，請閱讀 [Customer AI概述](../../intelligent-services/customer-ai/overview.md). 如需資料控管原則的資訊，請閱讀 [原則概觀](../../data-governance/policies/overview.md).

## 审核日志 {#audit-logs}

Experience Platform可讓您稽核各種服務和功能的使用者活動。 稽核記錄會提供有關誰做了哪些事、何時做的資訊。

**更新的功能**

| 功能 | 名称 | 描述 |
| --- | --- | --- |
| 已新增資源 | <ul><li>Attribution AI執行個體</li><li>Customer AI執行個體</li><li>資料流</li></ul> | 當活動發生時，會自動記錄稽核記錄資源。 如果已啟用此功能，您就不需要手動啟用記錄收集。 |

{style="table-layout:auto"}

如需Platform中稽核記錄所追蹤之不同資源特定事件型別的詳細資訊，請參閱 [稽核記錄概觀](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供多個儀表板，您可以透過這些儀表板檢視有關您組織資料的重要深入分析，如每日快照期間所擷取。

| 功能 | 描述 |
| --- | --- |
| 使用中標籤 | 在Widget資料庫中檢視時，使用中標籤可輕鬆識別儀表板中現有Widget的存在。 這可讓您輕鬆避免重複，不過您仍然可以新增相同的Widget多次。 |
| 使用者定義儀表板 | 使用者定義儀表板可讓您建置和管理自訂儀表板，有助於加速深入分析和自訂視覺效果。 透過使用者定義儀表板，您可以建立、新增和編輯自訂的Widget，以視覺化方式呈現與貴組織相關的關鍵量度。 閱讀 [功能指南](../../dashboards/user-defined-dashboards.md) 以深入瞭解。 |
| Customer Data Platform分析資料模型 | Customer Data Platform (CDP) Insights資料模型功能可公開資料模型和SQL，以支援各種設定檔、目的地和分段Widget的深入分析。 您可以自訂這些SQL查詢範本，為您的行銷和關鍵績效指標使用案例建立CDP報表。 這些見解然後可用作使用者定義儀表板的自訂Widget。 閱讀 [CDP Insights資料模型功能指南](../../dashboards/cdp-insights-data-model.md) 以深入瞭解。 |
| 對象重疊報表Widget | 此Widget同時適用於兩者 [!UICONTROL 設定檔] 和 [!UICONTROL 區段] 儀表板。 報表提供依所選區段之最高或最低重疊百分比排名的有序對象清單。 從 [!UICONTROL 設定檔] 控制面板您可以透過所有可用區段的合併原則，篩選及檢視對象重疊。 此 [!UICONTROL 區段] 控制面板可讓您依特定區段篩選對象重疊。<br>使用此分析來建立新的、高效能區段，並避免將相同的對象傳送至不同的目的地。 報表也有助於識別隱藏的深入分析，以改善細分或找出要追求的不重複設定檔。 閱讀個別 [設定檔](../../dashboards/guides/profiles.md#audience-overlap-report) 和 [區段](../../dashboards/guides/segments.md#audience-overlap-report) Widget指南以瞭解更多資訊。 |

如需詳細資訊，請參閱 [!DNL Dashboards]，請參閱 [[!DNL Dashboards] 概觀](../../dashboards/home.md).

## 資料彙集 {#data-collection}

Adobe Experience Platform提供了一套技術，可讓您收集使用者端客戶體驗資料，並將其傳送至Adobe Experience Platform Edge Network，在那裡可以擴充和轉換資料，並將其分發到Adobe或非Adobe目的地。

**新功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| 平台UI中的左側導覽整合 | 先前專屬於資料收集UI的所有功能（包括標籤、事件轉送和資料串流）現在也可透過Experience Platform左側導覽的類別下取得 **[!UICONTROL 資料彙集]**. 如此一來，當您在Platform中使用資料收集功能時，便不需要在UI之間切換。 |
| 標籤和事件轉送中的使用者歸因 | 清單可用時 [!UICONTROL 屬性] 在標籤和事件轉送中，每個列出的屬性現在會顯示其上次更新時間，以及進行更新的使用者。 |
| [[!DNL Snap Conversions API] 擴充功能](https://exchange.adobe.com/apps/ec/108550) 用於事件轉送 | 您現在可以將資料傳送至 [!DNL Snapchat Conversions API] 使用 [事件轉送](../../tags/ui/event-forwarding/overview.md) 副檔名。 有關如何驗證和使用API的詳細資訊，請參閱 [[!DNL Snapchat Marketing API] 檔案](https://marketingapi.snapchat.com/docs/conversion.html). |
| [[!DNL User-Agent Client Hints] 在Web SDK中](../../edge/fundamentals/user-agent-client-hints.md) | Web SDK現在支援 [[!DNL User-Agent Client Hints]](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). 使用者端提示可讓網站擁有者存取 [!DNL User-Agent] 字串，但採用更能保護隱私的方式。 |
| [Web SDK逐頁移轉](../../edge/home.md#migrating-to-web-sdk) | 您現在可以從其他Experience Cloud程式庫移轉現有的Web屬性，例如 [!DNL at.js]，一次一個頁面。 如此可分階段移轉Web SDK，而不需要一次移轉所有頁面。 |
| [[!DNL Adobe Journey Optimizer] 支援資料串流](../../edge/datastreams/overview.md#aep) | 適用於資料串流的Adobe Experience Platform服務現在支援 [!DNL Adobe Journey Optimizer]. 此選項可讓您在中使用網頁和應用程式型傳入頻道 [!DNL Adobe Journey Optimizer]. |

{style="table-layout:auto"}

如需Platform資料收集的詳細資訊，請參閱 [資料彙集概觀](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先建立的與目標平台的整合，可無縫啟用Adobe Experience Platform的資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。

**新功能或更新功能**

| 功能 | 描述 |
| ----------- | ----------- |
| 目标 SDK | Destination SDK現在為建立批次（或檔案式）生產或私人目的地的合作夥伴和客戶提供完整支援。 如需詳細資訊，請參閱下列檔案頁面： <ul><li>[Destination SDK概觀](../../destinations/destination-sdk/overview.md)</li><li>[設定以檔案為基礎的目的地](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)</li><li>[設定檔案型目的地的檔案格式選項](../../destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)</li><li>[測試您的檔案型目的地](../../destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)</li></ul> |

{style="table-layout:auto"}

**新的或更新目的地**

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services為跨頻道客戶體驗設計提供平台，並為視覺行銷活動的策劃、即時互動管理和跨頻道執行提供環境。 [開始使用行銷活動](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). 請注意，這項整合可搭配使用 [Adobe Campaign 8.4或更高版本](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html?lang=en#release-8-4-1). |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | 此 [!DNL Salesforce CRM] 目的地已更新，可支援聯絡人和潛在客戶更新，以及效能改善，以更快更新。 |

{style="table-layout:auto"}

**新增或更新後的檔案**

| 文档 | 描述 |
| ----------- | ----------- |
| 目的地流程服務API檔案 | 此 [目的地API參考檔案](https://developer.adobe.com/experience-platform-apis/references/destinations/) 已更新，加入如何對檔案型目的地執行作業的指引。 稍後將新增串流目的地的作業。 |

如需有關目的地的詳細一般資訊，請參閱 [目的地概觀](../../destinations/home.md).

## 體驗資料模型(XDM) {#xdm}

XDM是開放原始碼規格，針對帶入Adobe Experience Platform的資料提供通用結構和定義（結構描述）。 藉由遵守XDM標準，所有客戶體驗資料都可以整合到通用表示中，以更快、更整合的方式提供深入分析。 您可以從客戶動作獲得有價值的深入分析、透過區段定義客戶對象，以及使用客戶屬性進行個人化。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| UI支援列舉和建議值 | 除了啟用資料驗證的列舉之外，您現在還可以 [新增或移除建議值](../../xdm/ui/fields/enum.md) 標準或自訂字串欄位，好讓Platform使用者在建立區段時可以從中選擇好記的值清單。 |

**新XDM元件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 字段组 | [[!UICONTROL AJO分類欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | 與互動導致主張事件觸發的特定元素的屬性。 |
| 字段组 | [[!UICONTROL MediaAnalytics互動細節]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | 追蹤一段時間內的媒體互動。 |
| 字段组 | [[!UICONTROL 媒體詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | 追蹤媒體詳細資訊。 |
| 字段组 | [[!UICONTROL AdobeCJM ExperienceEvent — 表面]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | 說明Adobe Journey Optimizer中體驗事件的介面。 |

{style="table-layout:auto"}

**已更新XDM元件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 行为 | [[!UICONTROL 時間序列]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>已新增以下專案的值： `eventType`：<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>已移除下列專案的值： `eventType`：<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| 字段组 | （多個） | [已更新數個欄位說明](https://github.com/adobe/xdm/pull/1628/files) 橫跨Journey Orchestration元件。 |
| 字段组 | （多個） | [更新數個Adobe Workfront元件的標題](https://github.com/adobe/xdm/pull/1634/files) 以保持一致性。 |
| 字段组 | [[!UICONTROL AJO分類欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | 將數個欄位的名稱空間更新為 `xdm`. |
| 字段组 | [[!UICONTROL Journey Orchestration步驟事件常見欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | 新增欄位， `isReadSegmentTriggerStartEvent`. |
| 字段组 | [[!UICONTROL 預測性氣象]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | 已變更 `xdm:uvIndex` 欄位新增至整數型別，並新增 `xdm` 名稱空間至缺少的多個欄位。 |
| 字段组 | [[!UICONTROL 媒體詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` 和 `xdm:implementationDetails` 已從欄位群組中移除。 |
| 資料型別 | （多個） | [已更新數個媒體屬性名稱](https://github.com/adobe/xdm/pull/1626/files) 資料型別之間的一致性。 |
| 資料型別 | [[!UICONTROL 實作詳細資料]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | 新增顫振的已知名稱。 |
| 資料型別 | [[!UICONTROL 興趣點細節]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | 資料型別現在可以接受與地標關聯的中繼資料索引鍵/值組清單。 |
| 資料型別 | [[!UICONTROL 主張動作]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] 已重新命名為 [!UICONTROL 主張動作]. |
| 資料型別 | [[!UICONTROL 主張事件型別]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] 已重新命名為 [!UICONTROL 主張動作]. |
| （多個） | （多個） | 實驗性質已經過 [已在所有B2B元件上穩定](https://github.com/adobe/xdm/pull/1617/files). |
| （多個） | （多個） | Adobe Journey Optimizer實體已 [已穩定](https://github.com/adobe/xdm/pull/1625/files). |
| （多個） | （多個） | 跨多個實驗元件的特定欄位名稱空間已 [已更新以保持一致性](https://github.com/adobe/xdm/pull/1626/files). |

{style="table-layout:auto"}

如需有關Platform中XDM的詳細資訊，請參閱 [XDM系統總覽](../../xdm/home.md).

## Identity Service {#identity-service}

提供相關的數位體驗需要完全瞭解您的客戶。 當您的客戶資料分散於不同的系統時，這會使情況更困難，導致每個客戶似乎都有多個「身分」。

Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，協助您更清楚瞭解客戶及其行為。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支援資料集刪除 | Identity Service現在支援透過請求資料集時刪除資料集 [目錄服務API](https://developer.adobe.com/experience-platform-apis/references/catalog/)、UI或資料衛生。 閱讀指南： [刪除UI中的資料集](../../catalog/datasets/user-guide.md#delete-a-dataset) 以取得詳細資訊。 |

若要進一步瞭解Identity Service，請閱讀 [Identity Service概觀](../../identity-service/home.md).

## 查询服务 {#query-service}

查詢服務可讓您使用標準SQL在Adobe Experience Platform中查詢資料 [!DNL Data Lake]. 您可以從以下位置聯結任何資料集： [!DNL Data Lake] 並將查詢結果擷取為新資料集，以用於報表、資料科學工作區或內嵌至即時客戶個人檔案。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 警報訂閱API | Adobe Experience Platform查詢服務可讓您針對隨選和已排程的查詢訂閱警示。 警報可透過電子郵件、Platform UI內或兩者來接收。 目前，查詢警報只能使用訂閱 [查詢服務API](https://developer.adobe.com/experience-platform-apis/references/query-service/). |
| 資料集範例 | 查詢服務資料集範例可讓您對大資料執行探索性查詢，並大幅縮短處理時間，但代價是查詢準確性。 請參閱 [資料集範例指南](../../query-service/essential-concepts/dataset-samples.md) 以深入瞭解。 |

如需詳細資訊，請參閱 [!DNL Query Service]，請參閱 [[!DNL Query Service] 概觀](../../query-service/home.md).

請參閱 [查詢警示檔案](../../query-service/api/alert-subscriptions.md) 以深入瞭解。

## 源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| Audience Manager區段母體對即時客戶個人檔案的影響 | 當您首次使用Audience Manager來源將Audience Manager區段傳送至Platform時，大量的Audience Manager區段母體的擷取會直接影響您的總設定檔計數。 這表示選取所有區段可能會導致「設定檔」計數超過您的授權使用權益。 如需詳細資訊，請閱讀 [Audience Manager來源概觀](../../sources/connectors/adobe-applications/audience-manager.md). 如需授權使用方式的詳細資訊，請閱讀以下檔案： [使用授權使用情況儀表板](../../dashboards/guides/license-usage.md). |
| 支援Adobe Campaign託管Cloud Service | 使用Adobe Campaign託管Cloud Service來源，將您的Adobe Campaign v8.4傳遞和追蹤記錄資料帶入Experience Platform。 閱讀指南： [在UI中建立Adobe Campaign ManagedCloud Service來源連線](../../sources/tutorials/ui/create/adobe-applications/campaign.md) 以取得詳細資訊。 |
| 批次來源的隨選擷取的API支援 | 使用隨選擷取為具有的指定資料流建立隨選資料流執行 [!DNL Flow Service] API。 建立的流程執行必須設定為一次性內嵌。 如需詳細資訊，請閱讀以下指南： [使用API建立隨選擷取的流程執行](../../sources/tutorials/api/on-demand-ingestion.md) 以取得詳細資訊。 |
| API支援重試批次來源的失敗資料流執行 | 使用 `re-trigger` 操作，透過API重試失敗的資料流。 閱讀指南： [使用API重試失敗的資料流執行](../../sources/tutorials/api/retry-flows.md) 以取得詳細資訊。 |
| API支援篩選的列層級資料 [!DNL Google BigQuery] 和 [!DNL Snowflake] 來源 | 使用邏輯和比較運運算元來篩選的列層級資料 [!DNL Google BigQuery] 和 [!DNL Snowflake] 來源。 閱讀指南： [使用API篩選來源的資料](../../sources/tutorials/api/filter.md) 以取得詳細資訊。 |

若要進一步瞭解來源，請閱讀 [來源概觀](../../sources/home.md).

---
title: Adobe Experience Platform發行說明2022年4月
description: Adobe Experience Platform的2022年4月發行說明。
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2904'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发布日期：2022 年 4 月 27 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [[!DNL Dashboards]](#dashboards)
- [数据流](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [目标](#destinations)
- [體驗資料模型(XDM)](#xdm)
- [Real-Time Customer Data Platform B2B 版](#B2B)
- [源](#sources)

## [!DNL Dashboards] {#dashboards}

Platform提供多個儀表板，您可以透過這些儀表板檢視有關您組織資料的重要資訊，這些資料是在每日快照期間擷取的。

儀表板會為貴組織的資料提供預先設定的報告選項，並直接內建在Platform的行銷人員工作流程中。 這些儀表板不需要額外的IT支援，也不需要透過其他資料倉儲設計與實作匯出及處理資料所需的時間和精力。

下列Widget可透過Widget資料庫存取，並位於其各自的儀表板上。 如需有關的詳細資訊，請參閱檔案： [如何透過Widget資料庫新增Widget](../../dashboards/customize/widget-library.md).

**新增Widget**

| Widget | 功能板 | 描述 |
| ------ | --------- | ----------- |
| [!UICONTROL 設定檔新增趨勢] | 用户档案 | 此Widget使用線圖來說明過去30天、90天或12個月每日新增至設定檔存放區的合併設定檔總數。 |
| [!UICONTROL 對應到目的地狀態的對象] | 用户档案 | 此Widget會顯示單一量度中已對應和未對應的對象總數，並使用環圈圖來說明總數之間的比例差異。 |
| [!UICONTROL 對象人數] | 用户档案 | 此Widget提供兩欄表格，列出最多20個區段及每個區段中包含的對象總數。 此清單取決於根據對象總數從高到低套用和排序的合併原則。 |
| [!UICONTROL 設定檔計數趨勢] | 用户档案 | 此Widget使用線圖來說明系統中包含的設定檔總數隨時間變化的趨勢。 30天、90天和12個月期間的資料都可視覺化。 |
| [!UICONTROL 依身分割槽分的單一身分設定檔] | 用户档案 | 此Widget使用長條圖來說明僅以單一唯一識別碼識別的設定檔總數。 Widget支援最多五個最常發生的身分識別。 |
| [!UICONTROL 目的地狀態] | 目标 | 此Widget會將啟用的目的地總數顯示為單一量度，並使用環圈圖來說明啟用和停用目的地之間的比例差異。 |
| [!UICONTROL 依目的地平台區分的有效目的地] | 目标 | 此Widget使用兩欄表格來顯示作用中目的地平台的清單，以及每個目的地平台的有效目的地總數。 |
| [!UICONTROL 所有目的地中的啟用對象] | 目标 | 此Widget提供在單一量度中跨所有目的地啟用的對象總數。 |
| [!UICONTROL Audience啟用順序] | 区段 | 此Widget提供三欄表格，列出目的地名稱、平台和受眾的啟用日期。 |
| [!UICONTROL 受众规模趋势] | 区段 | 此Widget以30天、90天及12個月期間內，符合任何區段定義條件的設定檔總數，提供線圖插圖。 |
| [!UICONTROL 對象人數變化趨勢] | 区段 | 此Widget提供線圖，說明最近每日快照之間符合指定區段資格的設定檔總數差異。 趨勢分析的期間可以視覺化地呈現超過30天、90天和12個月的期間。 |
| [!UICONTROL 依身分割槽分的對象人數趨勢] | 区段 | 此Widget會根據選取的身分型別，說明特定區段的對象人數趨勢。 趨勢分析的期間可以視覺化地呈現超過30天、90天和12個月的期間。 |

**新增功能** {#new-features}

| 功能 | 功能板 | 描述 |
| ------- | --------- | ----------- |
| 孤立的設定檔區段會籍清理 | 設定檔與授權使用情況 | 設定檔服務現在會每天移除剩餘的區段成員，以在您的系統中提供更準確的設定檔表示。 刪除指定設定檔的所有設定檔片段後，就會進行這項清理。 授權使用儀表板中的「可定址對象」量度可能會下降，而設定檔儀表板中的「設定檔計數」量度可能會下降，因為這些量度包含此版本之前的遺留區段片段。 |

{style="table-layout:auto"}

如需有關的詳細資訊，請參閱檔案： [[!DNL Profiles]](../../dashboards/guides/profiles.md)， [[!DNL Destinations]](../../dashboards/guides/destinations.md)、和 [[!DNL Segments]](../../dashboards/guides/segments.md) 儀表板。

## 数据流 {#dataflows}

在Platform中，資料會從許多不同的來源擷取、在系統內分析，並啟用至各種不同的目的地。 Platform藉由提供資料流透明度，讓追蹤這種潛在非線性資料流的程式變得更輕鬆。

資料流可呈現在Platform上行動資料的作業。 這些資料流會在不同的服務中設定，有助於將資料從來源聯結器移動到目標資料集，然後由Identity Service和即時客戶個人檔案使用，最後啟用到目的地。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 區段控制面板 | 您現在可以使用監視儀表板來監視區段的資料流。 若要深入瞭解，請閱讀以下指南： [在UI中監視區段](../../dataflows/ui/monitor-segments.md) |

如需資料流的詳細一般資訊，請參閱 [資料流概觀](../../dataflows/home.md). 若要深入瞭解細分，請參閱 [區段概述](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支援Adobe Analytics來源 | Adobe Analytics來源現在支援「資料準備」功能，可讓您在建立資料流時，將Analytics報表套裝資料對應至目標XDM結構描述。 請參閱教學課程，位置如下： [建立Analytics來源連線](../../sources/tutorials/ui/create/adobe-applications/analytics.md) 以取得詳細資訊。 |
| 支援匯入現有的對應規則 | 您現在可以從現有資料流匯入對應規則，以加速資料流設定並限制錯誤。 請參閱教學課程，位置如下： [匯入現有的對應規則](../../data-prep/ui/mapping.md) 以取得詳細資訊。 |

如需詳細資訊，請參閱 [!DNL Data Prep]，請參閱 [[!DNL Data Prep] 概觀](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先建立的與目標平台的整合，可無縫啟用Adobe Experience Platform的資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。

**新功能或更新功能**

| 功能 | 描述 |
| ----------- | ----------- |
| 進階企業目的地聯結器 | 現在一般提供三個企業目的地聯結器： [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md)， [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)、和 [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md). <br> 企業目的地聯結器的一般可用性包括先前在Beta階段提供的所有功能，以及更多： <ul><li>新的驗證功能，包括 [Azure事件中樞中的共用存取簽章](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) 及更多內容 [驗證型別](../../destinations/catalog/streaming/http-destination.md#authentication-information) （持有人權杖、OAuth 2）在HTTP API目的地中；</li><li>[正在回填歷史設定檔資料](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) （首次啟動時傳送符合區段資格的歷史設定檔）；</li><li>這些目的地現在支援資料流執行量度；</li><li>[其他區段中繼資料](../../destinations/catalog/streaming/http-destination.md#destination-details) 包含在資料裝載中，包括區段名稱和區段時間戳記；</li><li>支援 [靜態IP位址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 適用於需要將Experience Platform加入允許清單的客戶。</li></ul> |
| 目的地資料流的內容感知警報 | 您現在可以 [訂閱警示](../../destinations/ui/alerts.md) 建立目的地資料流時，接收資料流執行狀態、成功或失敗的警示訊息。 您可以選擇在Experience PlatformUI中或透過電子郵件接收警報。 |

### 進階企業目的地聯結器的發行程式 {#release-process-enterprise-destinations}

對於Amazon Kinesis、Azure事件中樞和HTTP API目的地，在發行程式（從4月27日開始）期間，您會在目的地目錄中看到舊的Beta版目的地卡，以及新的一般可用(GA)目的地卡。 客戶使用Beta版目的地設定的任何資料流將在未來幾天內移轉至相同目的地的GA版本。 此移轉作業應於4月29日星期五結束前完成。 在這段短暫的時間內，測試版目的地仍會持續可見，並標示為 **已棄用**.

如果您一直在Beta版階段使用這些目的地，請注意下列事項：

- 如果之前已在測試版中使用了3個目的地的任一個，則無需採取任何動作。 所有在Beta版中設定的資料流將繼續正常運作，並將移轉至GA版本。
- 如果您想從4月27日起設定這些目的地，請使用目的地的新GA版本進行設定。
- 預計在4月29日星期五當天結束時，發行作業完成後，會移除標示為已過時的Beta版卡片。 Experience Platform工程團隊正在密切監控發行作業是否成功。

**新目的地**

| 目标 | 描述 |
| ----------- | ----------- |
| [!DNL Criteo] | 將資料連線並啟動至 [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md) 廣告平台。 |
| [!DNL Sendgrid] | 將資料連線並啟動至 [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) 交易和行銷電子郵件的平台。 |

如需有關目的地的詳細一般資訊，請參閱 [目的地概觀](../../destinations/home.md).

## 體驗資料模型(XDM) {#xdm}

XDM是開放原始碼規格，針對帶入Adobe Experience Platform的資料提供通用結構和定義（結構描述）。 藉由遵守XDM標準，所有客戶體驗資料都可以整合到通用表示中，以更快、更整合的方式提供深入分析。 您可以從客戶動作獲得有價值的深入分析、透過區段定義客戶對象，以及使用客戶屬性進行個人化。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 新增或移除結構描述的個別標準欄位 | 結構描述編輯器UI現在可讓您將標準欄位群組的部分新增到結構描述，為您選擇包含的欄位提供更大的靈活性，而無需從頭開始建立自訂資源。<br><br>您現在也可以直接在結構描述結構中定義臨時自訂欄位，並將其指派給新的或現有的自訂欄位群組，而無需預先建立或編輯欄位群組。<br><br>請參閱指南： [在UI中建立和編輯方案](../../xdm/ui/resources/schemas.md) 以取得這些新工作流程的詳細資訊。 |

{style="table-layout:auto"}

**新XDM元件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 全域結構描述 | [[!UICONTROL 資料衛生操作請求]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | 擷取資料清理請求的詳細資料，以刪除或修改指定資料集或沙箱中的記錄。 |
| 描述項 | [[!UICONTROL 時間序列詳細程度描述項]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | 表示時間序列和摘要資料的詳細程度。 套用至結構描述時，該結構描述的 `timestamp` 欄位是此詳細程度期間中的第一個時間戳記。 |
| 类 | [[!UICONTROL xdm摘要量度]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | 提供具有分組維度的預先摘要量度，例如具有GROUP BY的SQL SELECT的結果。 |
| 字段组 | [[!UICONTROL 同意原則評估結果對應]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResults.schema.json) | 擷取個人的同意原則評估結果。 |
| 字段组 | [[!UICONTROL 網站搜尋]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 擷取網站搜尋的相關資訊，例如搜尋查詢、篩選和訂購。 |
| 字段组 | [[!UICONTROL 合併銷售機會]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | 擷取兩個或多個潛在客戶合併之事件的詳細資訊。 |
| 字段组 | [[!UICONTROL 已发送电子邮件]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | 擷取傳送電子郵件給收件者之事件的詳細資料。 |
| 字段组 | [[!UICONTROL 拼接欄位]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | 擷取透過事件的身分拼接流程運算的值。 |
| 字段组 | [[!UICONTROL 稽核的次要收件者詳細資訊]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | 擷取稽核次要收件者詳細資料的Adobe Journey Optimizer欄位群組。 |
| 字段组 | [[!UICONTROL XDM商業帳戶個人關係細節]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 擷取和帳戶 — 個人關係相關的細節。 |
| 字段组 | [[!UICONTROL 帳戶個人詳細資訊]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 擷取和帳戶 — 個人關係相關的細節。 |
| 資料型別 | [[!UICONTROL 購物車]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | 擷取有關電子商務購物車的資訊。 |
| 資料型別 | [[!UICONTROL 送貨]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 擷取一或多個產品的送貨資訊。 |
| 資料型別 | [[!UICONTROL 網站搜尋]](https://github.com/adobe/xdm/blob/master/components/datatypes/sitesearch.schema.json) | 擷取網站搜尋活動的資訊。 |
| 擴充功能(Workfront) | [[!UICONTROL 作業任務屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | 擷取與作業任務相關的細節。 |
| 擴充功能(Workfront) | [[!UICONTROL 工作Portfolio屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | 擷取與工作組合相關的細節。 |
| 擴充功能(Workfront) | [[!UICONTROL 工作計畫屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | 擷取與工作方案相關的細節。 |
| 擴充功能(Workfront) | [[!UICONTROL 工作專案屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | 擷取與工作專案相關的細節。 |

{style="table-layout:auto"}

**已更新XDM元件**

| 组件类型 | 名称 | 更新描述 |
| --- | --- | --- |
| 全域結構描述 | [[!UICONTROL 目标]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | 新的列舉值 `destinationCategory`. |
| 描述項 | [[!UICONTROL 易記名稱描述項]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | 新增對移除建議值的支援(`meta:enum`)。 |
| 字段组 | [[!UICONTROL 使用者登入程式]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` 欄位已新增。 |
| 資料型別 | [[!UICONTROL 商务]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | 已新增多個與購物車相關的欄位。 |
| 資料型別 | [[!UICONTROL 產品清單專案]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 針對選取的選項和折扣金額新增欄位。 |
| 擴充功能（智慧型服務） | [[!UICONTROL Intelligent Services JourneyAI傳送時間最佳化]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | 針對傳送時間分數最佳化儲存格式。 |
| 擴充功能(Workfront) | [[!UICONTROL Workfront變更事件]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | 數個欄位已取代為 `workfront:customData` 自訂表單欄位的欄位。 |
| 擴充功能(Workfront) | [[!UICONTROL 工作任務屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | 新增了數個欄位。 |
| 擴充功能(Workfront) | [[!UICONTROL 工作物件]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | 父物件型別和自訂表單欄位的新欄位。 |

{style="table-layout:auto"}

如需有關Platform中XDM的詳細資訊，請參閱 [XDM系統總覽](../../xdm/home.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai/ml-services}

AI/ML服務可讓行銷分析師和從業人員運用客戶體驗使用案例中人工智慧和機器學習的力量。 借助此功能，营销分析人员可使用商业级别配置来设置特定于公司需求的预测，而无需具备数据科学专业知识。

### 归因人工智能

Attribution AI 用于将点数归因于导致转化事件的接触点。营销人员可利用此功能，促进量化客户旅程中每个营销接触点的营销影响。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支援多個資料集 | 多資料集功能現在支援所有體驗事件資料集，以及選擇「身分對應」作為身分。 只要資料集間有共同的身分名稱空間，客戶就可以選取「身分對應」和任何相關聯的ID。 Attribution AI支援下列結構描述： Adobe Analytics、體驗事件、消費者體驗事件。 如需Attribution AI中支援多資料集的詳細資訊，請參閱 [Attribution AI使用手冊](../../intelligent-services/attribution-ai/user-guide.md). |

如需詳細資訊，請參閱 [!DNL Intelligent Services]，請參閱 [[!DNL Intelligent Services] 概觀](../../intelligent-services/home.md).

### Customer AI

Real-time Customer Data Platform中提供的Customer AI可產生自訂傾向評分，例如大規模個別設定檔的流失和轉換情形。 这无需通过将业务需求转变为机器学习问题、选择算法、培训或部署即可完成。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 支援多個資料集 | 多資料集功能現在支援所有體驗事件資料集，以及選擇「身分對應」作為身分。 只要資料集間有共同的身分名稱空間，客戶就可以選取「身分對應」和任何相關聯的ID。 Customer AI支援下列結構描述： Adobe Analytics、體驗事件、消費者體驗事件和Adobe Audience Manager結構描述。 如需Customer AI多資料集支援的詳細資訊，請參閱 [Customer AI使用手冊](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Customer AI中的新模型評估量度 | Customer AI中的新收益圖表可讓行銷人員根據其預算和ROI目標決定要定位的群組規模。 新的提升圖可測量模型的品質，可更清楚瞭解其超越隨機鎖定目標的提升度。 如需詳細資訊，請參閱 [探索Customer AI的深入分析](../../intelligent-services/customer-ai/user-guide/discover-insights.md) 檔案。 |

如需詳細資訊，請參閱 [!DNL Intelligent Services]，請參閱 [[!DNL Intelligent Services] 概觀](../../intelligent-services/home.md).

## Real-Time Customer Data Platform B2B 版 {#B2B}

Real-Time CDP B2B Edition以Real-time Customer Data Platform (Real-Time CDP)為基礎，專為以B2B服務模式運作的行銷人員所打造。 它會整合來自多個來源的資料，並將其合併為單一檢視的人員與帳戶設定檔。 此統一的資料可讓行銷人員精準鎖定特定對象，並透過所有可用管道吸引這些對象。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支援 `isDeleted` 功能 | 全部 [!DNL Marketo] 資料集不包括 `Activities` 現在支援 `isDeleted` 對應。 新對應會自動新增至您現有的B2B資料流。 您可以使用 `isDeleted` 對應，以篩選掉已刪除的記錄，好讓您的資料位於 [!DNL Data Lake] 與您的來源資料一致。 請參閱 [[!DNL Marketo] 對應欄位指南](../../sources/connectors/adobe-applications/mapping/marketo.md) 有關下列專案的詳細資訊： `isDeleted`. |

若要進一步瞭解Real-time Customer Data Platform B2B版本，請參閱 [B2B概覽](../../rtcdp/b2b-overview.md).

## 源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 支持 [!DNL OneTrust Integration] | 您現在可以使用 [!DNL OneTrust Integration] 從您的來源擷取同意和偏好設定資料的來源 [!DNL OneTrust] 至平台的帳戶。 請參閱以下說明檔案： [建立 [!DNL OneTrust Integration] 來源連線](../../sources/connectors/consent-and-preferences/onetrust.md) 以取得詳細資訊。 |
| 支持 [!DNL Square] | 您現在可以使用 [!DNL Square] 從中擷取付款資料的來源 [!DNL Square] 至平台的帳戶。 |
| 支援刪除客戶屬性資料流 | 您現在可以刪除使用客戶屬性來源聯結器建立的資料流。 |

若要進一步瞭解來源，請參閱 [來源概觀](../../sources/home.md).

---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform的2023年4月發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: e3fc587d924b2183806918f91e5ae3aa3fee52f3
workflow-type: tm+mt
source-wordcount: '2094'
ht-degree: 4%

---

# Adobe Experience Platform 发行说明

>[!IMPORTANT]
>
>自2023年5月15日起， `Existing` 為了移除區段會籍生命週期中的備援，狀態將從區段會籍對應中淘汰。 進行此變更後，區段中符合資格的設定檔將呈現為 `Realized` 而不符合資格的設定檔將繼續顯示為 `Exited`. 如需此變更的詳細資訊，請參閱 [區段服務區段](#segmentation).

**发布日期：2023 年 4 月 26 日**

Adobe Experience Platform 现有功能的更新包括：

- [仪表板](#dashboards)
- [数据准备](#data-prep)
- [数据收集](#data-collection)
- [目标](#destinations)
- [Experience Data Model](#xdm)
- [Real-Time Customer Data Platform](#rtcdp)
- [实时客户资料](#profile)
- [分段服务](#segmentation)
- [源](#sources)

## 仪表板 {#dashboards}

Adobe Experience Platform提供多個儀表板，您可以透過這些儀表板檢視有關您組織資料的重要深入分析，如每日快照期間所擷取。

**新功能或更新功能** {#dashboards-new-updated-features}

| 功能 | 描述 |
| --- | --- |
| 使用者定義儀表板 | 您現在可以 **篩選歷史資料** 從Widget深入分析中，使用最近的資料或自訂分析期間。 請參閱 [使用者定義儀表板指南](../../dashboards/user-defined-dashboards.md#filter-historical-data) 以取得詳細資訊。<br>您現在也可以 **複製您現有的Widget**. 透過自訂重複專案並編輯其屬性，您可以避免在建立新的唯一Widget時從頭重新啟動。 閱讀 [widget複製指南](../../dashboards/user-defined-dashboards.md#duplicate-a-widget) 以深入瞭解。 |

{style="table-layout:auto"}

如需儀表板的詳細資訊，包括如何授予存取許可權及建立自訂Widget，請從閱讀 [儀表板概觀](../../dashboards/home.md).

## 数据准备 {#data-prep}

「資料準備」可讓資料工程師對應、轉換和驗證與Experience Data Model (XDM)之間的資料。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 更新非生產沙箱中Adobe Analytics的回填期間 | 非生產沙箱中Adobe Analytics的回填期間已縮短至三個月。 生產沙箱的回填在13個月時保持不變。 此變更僅適用於新流程，不會影響現有流程。 如需詳細資訊，請閱讀 [Adobe Analytics概觀](../../sources/connectors/adobe-applications/analytics.md). |
| 新對應程式函式，可將FPID字串轉換為ECID | 使用 `fpid_to_ecid` 函式將FPID字串轉換為ECID，以用於Experience Platform和Experience Cloud應用程式。 如需詳細資訊，請閱讀 [資料準備函式指南](../../data-prep/functions.md). |

{style="table-layout:auto"}

如需「資料準備」的詳細資訊，請閱讀 [資料準備總覽](../../data-prep/home.md).

## 数据收集 {#data-collection}

Adobe Experience Platform提供了一套技術，可讓您收集使用者端客戶體驗資料，並將其傳送至Adobe Experience Platform Edge Network，在那裡可以擴充和轉換資料，並將其分發到Adobe或非Adobe目的地。

**新功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| 資料串流的IP位址模糊化 | 您現在可以在中定義部分或完整資料流層級IP模糊化選項 [資料流設定UI](../../edge/datastreams/configure.md). <br><br>資料流層級IP模糊化設定的優先順序高於Adobe Target和Audience Manager中設定的任何IP模糊化。 <br><br>傳送至Adobe Analytics的資料不受資料流層級的影響 [!UICONTROL IP模糊化] 設定。 Adobe Analytics目前會接收未經過模糊處理的IP位址。 若要讓Analytics接收模糊化的IP位址，您必須在Adobe Analytics中個別設定IP模糊化。 此行為將在未來版本中更新。<br><br> 如需有關IP模糊化的詳細資訊和如何設定的說明，請參閱 [資料流設定檔案](../../edge/datastreams/configure.md#advanced-options). |
| [資料流設定覆寫](../../edge/datastreams/overrides.md) | 您現在可以為資料串流定義其他設定選項，以便用來覆寫特定設定，例如事件資料集、Target屬性Token、ID同步容器和Analytics報表套裝。 <br><br>覆寫資料串流設定是兩個步驟的程式： <ol><li>首先，您必須在以下位置定義資料流設定覆寫： [資料流設定頁面](../../edge/datastreams/configure.md).</li><li>接著，您必須透過Web SDK命令或使用Web SDK將覆寫傳送至Edge Network [標籤延伸模組](../../edge/extension/web-sdk-extension-configuration.md).</li></ol> |
| OAuth JWT密碼 | 此 [OAuth JWT密碼](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) 可讓客戶使用Adobe和Google服務權杖，在事件轉送中支援伺服器對伺服器的互動。 |
| [!DNL Pinterest Conversions API] 扩展 | 此 [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) 事件轉送擴充功能可讓您運用Adobe Experience Platform Edge Network中擷取的資料，並將其傳送至 [!DNL Pinterest] 以伺服器端事件的形式使用 [!DNL Pinterest Conversions API]. |

{style="table-layout:auto"}

## 目标 {#destinations}

[!DNL Destinations] 是預先建立的與目標平台的整合，可無縫啟用Adobe Experience Platform的資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。

**新目的地** {#new-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] 連線](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | 使用SalesforceMarketing Cloud帳戶參與（前身為Pardot）目的地來擷取、追蹤、評分和評等潛在客戶。 針對涉及多個部門及決策者（需要較長的銷售和決策週期）的B2B使用案例，請使用此目的地。 |

{style="table-layout:auto"}

**新功能或更新功能** {#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 的資料流監視 [!DNL Custom Personalization] 和 [!DNL Adobe Commerce] 目的地 | <p> 您現在可以看到以下專案的啟用量度 [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md)， [自訂個人化](../../destinations/catalog/personalization/custom-personalization.md) 和 [使用屬性自訂個人化](../../destinations/catalog/personalization/custom-personalization.md) 連線。 </p> <p>![Adobe Commerce圖片](/help/destinations/assets/common/adobe-commerce-metrics.png "Adobe Commerce度量"){width="100" zoomable="yes"}</p>  另請參閱 [監視目的地工作區中的資料流](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) 以取得更多詳細資料。 |
| 新增 **[!UICONTROL 將區段ID附加至區段名稱]** 的欄位 [!DNL Google Ad Manager] 和 [!DNL Google Ad Manager 360] 目的地 | <p>您現在可以在以下位置取得區段名稱： [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) 和 [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 納入Experience Platform的區段ID，如下所示： `Segment Name (Segment ID)`.</p><p>![附加區段ID影像](/help/destinations/assets/common/append-segment-id-to-segment-name.png "新增將區段ID附加至區段名稱欄位 "){width="100" zoomable="yes"}</p> |
| 已排程的對象回填 | <p>對於 [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) 目的地，在區段首次對應至目的地連線後24到48小時，會排程啟用對象回填至目的地。 此更新是為了回應Google等待24小時直到擷取資料的原則，並將提高Real-time CDP和之間的匹配率 [!DNL Google Display & Video 360].</p> <p>請注意，這是隻適用於此目的地的後端設定，與UI中任何可由客戶設定的排程選項無關。</p> |

{style="table-layout:auto"}

**修正和增強功能** {#destinations-fixes-and-enhancements}

- 我們已修正 **身分已排除** 檔案型目的地匯出的報告量度。 客戶正如預期從啟用的匯出中接收所有匯出的ID。 不過， **身分已排除** 由於不正確計算絕不應該匯出的身分，UI中的報告量度錯誤地顯示大量排除的身分。 (PLAT-149774)
- 我們已修正 **排程** 啟動工作流程的步驟。 對於需要對應ID的目的地，客戶無法為新增到現有目的地連線的區段新增對應ID。 (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

如需有關目的地的詳細一般資訊，請參閱 [目的地概觀](../../destinations/home.md).

## 體驗資料模型(XDM) {#xdm}

XDM是開放原始碼規格，針對帶入Adobe Experience Platform的資料提供通用結構和定義（結構描述）。 藉由遵守XDM標準，所有客戶體驗資料都可以整合到通用表示中，以更快、更整合的方式提供深入分析。 您可以從客戶動作獲得有價值的深入分析、透過區段定義客戶對象，以及使用客戶屬性進行個人化。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 顯示名稱切換 | 結構描述編輯器現在提供切換功能，以在原始欄位名稱與較容易讀取的顯示名稱之間變更。<br>![反白顯示名稱切換的結構描述編輯器。](../../xdm/images/ui/resources/schemas/display-name-toggle.png "結構描述編輯器顯示名稱切換"){width="100" zoomable="yes"}<br>此靈活性可改善欄位可發現性和結構描述的編輯。 標準欄位群組的顯示名稱由系統產生，但如有需要，也可以透過UI自訂。 請閱讀 [顯示名稱切換檔案](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle) 以深入瞭解。 |

{style="table-layout:auto"}

**新XDM元件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 架构 | [[!UICONTROL Adobe Target分類欄位]](https://github.com/adobe/xdm/pull/1719/files) | 目標分類資料集的新XDM結構描述包含一組中繼資料欄位，可用於分類Target活動和體驗。 |

{style="table-layout:auto"}

**已更新XDM元件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 欄位群組 | [[!UICONTROL Adobe統一設定檔服務帳戶聯合擴充功能]](https://github.com/adobe/xdm/pull/1696/files) | 新增即時客戶設定檔的帳戶延伸欄位群組，讓使用者可在帳戶聯合上新增區段成員資格。 |
| 架构 | [[!UICONTROL 計算屬性系統結構描述]](https://github.com/adobe/xdm/pull/1696/files) | 即時客戶設定檔使用的計算屬性欄位群組已更新為系統唯讀全域結構描述。 |
| 欄位群組 | 多個 | 新增多個事件作為的欄位 [[!UICONTROL 時間序列結構描述]](https://github.com/adobe/xdm/pull/1718/files). |
| 欄位群組 | 設定檔熟客方案細節 | [已修正標題](https://github.com/adobe/xdm/pull/1717/files) 的 `xdm:upgradeDate` 從「計畫名稱」到「升級日期」。 |
| 欄位群組 | 多個 | 中的多個欄位 [[!UICONTROL 決定專案]](https://github.com/adobe/xdm/pull/1714/files) 已更新以移除雙重巢狀階層。 |

{style="table-layout:auto"}

如需Platform中XDM的詳細資訊，請閱讀 [XDM系統總覽](../../xdm/home.md).

## Real-Time Customer Data Platform

以Experience Platform為基礎，Real-time Customer Data Platform ([!DNL Real-Time CDP])可協助公司整合已知和未知的資料，透過整個客戶歷程的智慧型決策來啟用客戶設定檔。 [!DNL Real-Time CDP] 結合多個企業資料來源，即時建立客戶設定檔。 然後，根據這些設定檔建立的區段可傳送至下游目的地，以跨所有管道和裝置提供一對一的個人化客戶體驗。

**新增功能**

| 功能 | 描述 |
| ------- | ----------- |
| 增強型Real-Time CDP首頁 | 此 [Real-Time CDP首頁](https://experience.adobe.com) 已透過重新整理的外觀和改善的效能來增強。 首頁現在具有許可權感知功能，並顯示與您有權存取的功能相關的Widget。 如需詳細資訊，請閱讀 [Real-Time CDP首頁控制面板概觀](../../rtcdp/home-page-dashboards.md). |
| 自我識別調查 | 自我識別問卷是提供在Adobe Experience Platform UI首頁的簡短問卷。 使用自我識別調查來建立您的Experience Platform個人設定檔，並根據您的選擇接收量身打造的指引。 如需詳細資訊，請閱讀 [自我識別調查概觀](../../landing/self-identification.md). |

如需詳細資訊，請參閱 [!DNL Real-Time CDP]，請參閱 [[!DNL Real-Time CDP] 概觀](../../rtcdp/overview.md).

## 实时客户资料 {#profile}

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，無論客戶在哪裡或何時與您的品牌互動。 透過即時客戶個人檔案，您可以檢視結合來自多個管道（包括線上、離線、CRM和第三方資料）之資料的每個個別客戶的整體檢視。 設定檔可讓您將客戶資料整合到統一的檢視中，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| 假名設定檔資料到期日 | 假名設定檔資料到期現在可普遍使用！ 此版本會在啟用後，持續從Experience Platform執行個體中移除過時的假名設定檔。 若要進一步瞭解此功能及假名設定檔，請閱讀 [假名設定檔資料到期指南](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## 分段服务 {#segmentation}

[!DNL Segmentation Service] 透過描述可區分客戶群內可銷售人員群組的條件，來定義設定檔的特定子集。 區段能以記錄資料（例如人口資訊）或代表客戶與品牌互動的時間序列事件為基礎。

**新功能或更新功能**

| 功能 | 描述 |
| ------- | ----------- |
| 區塊會籍對應 | 之前於2023年2月15日所發佈公告的後續內容， `Existing` 為了移除區段會籍生命週期中的備援，狀態將從區段會籍對應中淘汰。 進行此變更後，區段中符合資格的設定檔將呈現為 `Realized` 而不符合資格的設定檔將繼續顯示為 `Exited`.<br/><br/> 此變更可能會影響您，如果您使用 [企業目的地](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis、Azure事件中樞、HTTP API)，而且可能根據 `Existing` 狀態。 若您有此需要，請檢閱您的下游整合。 如果您想要在超過特定時間後識別新合格的設定檔，請考慮使用以下組合 `Realized` 狀態和 `lastQualificationTime` 區段會籍對映中的。 如需詳細資訊，請洽詢您的Adobe代表。 |

{style="table-layout:auto"}

如需詳細資訊，請參閱 [!DNL Segmentation Service]，請參閱 [區段概觀](../../segmentation/home.md).

## 源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，並允許您使用Platform服務來建構、加標籤及增強這些資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 篩選Microsoft Dynamics、Salesforce CRM和SalesforceMarketing Cloud的列層級資料的API支援 | 使用邏輯和比較運運算元來篩選Microsoft Dynamics、Salesforce CRM和SalesforceMarketing Cloud來源的列層級資料。 閱讀指南： [使用API篩選來源的資料](../../sources/tutorials/api/filter.md) 以取得詳細資訊。 |
| Shopify Streaming的Beta版 | 此 [Shopify串流來源](../../sources/connectors/ecommerce/shopify-streaming.md) 現已推出測試版。 使用Shopify串流來源，從您的Shopify合作夥伴帳戶串流資料以進行Experience Platform。 |
| OneTrust整合正式發行 | 此 [OneTrust整合來源](../../sources/connectors/consent-and-preferences/onetrust.md) 現在為GA。 使用OneTrust整合來源，將您OneTrust整合帳戶的同意和偏好設定資料帶入Experience Platform。 |
| oracle Service Cloud正式發行 | 此 [oracle服務雲端來源](../../sources/connectors/customer-success/oracle-service-cloud.md) 現在為GA。 使用Oracle服務雲端來源，將您的Oracle服務雲端資料帶入Experience Platform。 |

{style="table-layout:auto"}

若要進一步瞭解來源，請閱讀 [來源概觀](../../sources/home.md).
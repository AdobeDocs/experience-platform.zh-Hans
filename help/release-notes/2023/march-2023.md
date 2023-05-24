---
title: Adobe Experience Platform發行說明2023年3月
description: Adobe Experience Platform的2023年3月發行說明。
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '2206'
ht-degree: 4%

---

# Adobe Experience Platform 发行说明

**发布日期：2023 年 3 月 29 日**

Adobe Experience Platform 现有功能的更新包括：

- [仪表板](#dashboards)
- [資料彙集](#data-collection)
- [数据准备](#data-prep)
- [目标](#destinations)
- [Experience Data Model](#xdm)
- [查询服务](#query-service)
- [Real-Time Customer Data Platform B2B 版](#b2b)
- [分段服务](#segmentation)
- [源](#sources)

## 仪表板 {#dashboards}

Adobe Experience Platform提供多個儀表板，您可以透過這些儀表板檢視有關您組織資料的重要深入分析，如每日快照期間所擷取。

**新功能或更新功能** {#dashboards-new-updated-features}

| 功能 | 描述 |
| --- | --- |
| 使用者定義儀表板 | 您現在可以 **範例屬性值** 將屬性新增至使用者定義儀表板widget撰寫器中的widget之前。 建立Widget時，該屬性欄中的幾個範例值可用於個別屬性。<br>您現在可以 **交換X和Y軸** 使用「交換軸」按鈕切換至您的Widget。 這可節省時間，並在將屬性新增至Widget時提供更符合人體工學的體驗。 此儲存需要再次從屬性面板尋找兩個屬性。<br> 您現在可以 **變更圖例的位置和標題** 在您的Widget中。 當圖例出現在Widget上後，您可以將該圖例重新放置到圖表周圍的任何位置，並且重新命名圖例標題，如同使用座標軸標籤和Widget標題一樣。 |

{style="table-layout:auto"}

如需儀表板的詳細資訊，包括如何授予存取許可權及建立自訂Widget，請從閱讀 [儀表板概觀](../../dashboards/home.md).

## 資料彙集 {#data-collection}

Adobe Experience Platform提供了一套技術，可讓您收集使用者端客戶體驗資料，並將其傳送至Adobe Experience Platform Edge Network，在那裡可以擴充和轉換資料，並將其分發到Adobe或非Adobe目的地。

**新功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| 中繼轉換API （測試版）的全新快速入門工作流程 | 從資料收集首頁畫面存取「快速入門」底下的全新快速入門工作流程！ 此 [中繼轉換API的快速入門工作流程](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) 讓客戶能快速收集並轉送事件資料，從伺服器端轉送至Meta，以便透過幾個簡單的步驟進行廣告轉換。 |
| 行動SDK全新快速入門工作流程（測試版） | 從資料收集首頁畫面存取「快速入門」底下的全新快速入門工作流程！ 此 [行動SDK快速入門工作流程](https://developer.adobe.com/client-sdks/documentation/) 可讓您快速實作Mobile SDK，並只需幾個簡單步驟即可驗證基本行動事件。 |
| [!DNL Braze] 事件轉送擴充功能 | 此 [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 事件轉送擴充功能可讓您運用Adobe Experience Platform Edge Network中擷取的資料，並將其傳送至 [!DNL Braze] 以伺服器端事件的形式使用 [!DNL Braze] 使用者追蹤API。 |
| [!DNL Epsilon] 事件轉送擴充功能 | 此 [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html) 擴充功能可讓您運用事件轉送，擷取Adobe Experience Platform Edge Network中的事件資訊，並將其傳送至 [!DNL Epsilon] 使用 [!DNL Epsilon] 事件API。 |
| [!DNL Mixpanel] 事件轉送擴充功能 | 此 [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 擴充功能可讓客戶運用事件轉送功能，擷取Adobe Experience Platform Edge Network中的事件資訊，並使用「追蹤事件」API將其傳送至Mixpanel。 |

{style="table-layout:auto"}

## 数据准备 {#data-prep}

「資料準備」可讓資料工程師對應、轉換和驗證與Experience Data Model (XDM)之間的資料。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 篩選Adobe Analytics資料的一般可用性 | 您現在可以使用資料準備功能套用規則和條件，在將Analytics資料擷取到即時客戶設定檔中之前篩選這些資料。 如需詳細資訊，請閱讀以下指南： [篩選設定檔擷取的Analytics資料](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| 用於編碼和解碼URL字串的新函式 | <ul><li>此 `get_url_encoded` 函式以URL作為輸入，並使用ASCII字元取代或編碼特殊字元。</li><li>此 `get_url_decoded` 函式以URL作為輸入，並將ASCII字元解碼為特殊字元。</li></ul> 如需詳細資訊，請閱讀 [資料準備函式指南](../../data-prep/functions.md). 如需保留字元及其對應編碼字元的完整清單，請閱讀以下指南： [特殊字元](../../data-prep/functions.md#special-characters). |

如需「資料準備」的詳細資訊，請閱讀 [資料準備總覽](../../data-prep/home.md).

## 目标 {#destinations}

[!DNL Destinations] 是預先建立的與目標平台的整合，可無縫啟用Adobe Experience Platform的資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。

**新目的地** {#new-destinations}

| 目标 | 描述 |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] 連線GA](../../destinations/catalog/personalization/adobe-commerce.md) | 此 [!DNL Adobe Commerce] 目的地聯結器（現已正式推出）可讓您選取一或多個Real-Time CDP對象，以啟用至 [!DNL Adobe Commerce] 帳戶，為購物者提供動態的個人化體驗。 |
| [[!DNL Snap Inc] 連線GA](../../destinations/catalog/advertising/snap-inc.md) | 此 [!DNL Snap Inc] 目的地聯結器（現已正式推出）可讓行銷人員將Experience Platform中建立的使用者區段匯入 [!DNL Snapchat Ads] 並使用它們來鎖定其廣告。 |
| [(API) Oracle Eloqua連線](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | 使用API型連線來 [!DNL Oracle Eloqua] 規劃及執行行銷活動，同時為中的潛在客戶提供個人化的客戶體驗 [!DNL Oracle Eloqua]. |
| [(Beta) [!DNL Amazon Ads] 連線](../../destinations/catalog/advertising/amazon-ads.md) | 此 [!DNL Amazon Ads] 與Adobe Experience Platform整合提供以下專案的統包整合： [!DNL Amazon Ads] 產品，包括 [!DNL Amazon DSP (ADSP)]. 使用 [!DNL Amazon Ads] 目的地：在Adobe Experience Platform中，使用者能定義廣告商對象，以在 [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] 連線](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] （前身為Bizible）可讓行銷人員深入瞭解哪些行銷手法最能有效提升公司收入，實現投資報酬最大化。 目的地可讓企業對企業(B2B)資料從Adobe Experience Platform傳輸至 [!DNL Marketo Measure]. 此卡僅適用於 [!DNL Marketo Measure Ultimate] 客戶。 |
| [TikTok連線](../../destinations/catalog/social/tiktok.md) | 使用您的資料在TikTok上建立自訂對象，以使用您的廣告促銷活動進行目標定位。 |
| [Zendesk連線](../../destinations/catalog/crm/zendesk.md) | 使用此目的地可在區段內建立身分識別並將其更新為內的聯絡人 [!DNL Zendesk]. |

{style="table-layout:auto"}

**新功能或更新功能** {#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 目的地的新存取控制許可權： [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | 新許可權可讓使用者啟用現有目的地的區段，而不會顯示 [對應步驟](../../destinations/ui/activate-batch-profile-destinations.md#mapping). 使用者可以在啟動工作流程中新增和移除區段，但無法新增或移除對應的屬性或身分。 |

{style="table-layout:auto"}

**修正和增強功能** {#destinations-fixes-and-enhancements}

我們正在針對Real-time CDP的檔案型目的地中PGP/GPG加密發行錯誤修正。 透過這項變更，目前使用加密的現有檔案型目的地將會產生副檔名與之前不同的檔案名稱。

- 使用加密時目前的擴充功能： `filename.csv`
- 未來使用加密時的擴充功能： `filename.csv.gpg`

如需有關目的地的詳細一般資訊，請參閱 [目的地概觀](../../destinations/home.md).

## 體驗資料模型(XDM) {#xdm}

XDM是開放原始碼規格，針對帶入Adobe Experience Platform的資料提供通用結構和定義（結構描述）。 藉由遵守XDM標準，所有客戶體驗資料都可以整合到通用表示中，以更快、更整合的方式提供深入分析。 您可以從客戶動作獲得有價值的深入分析、透過區段定義客戶對象，以及使用客戶屬性進行個人化。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| CSV至結構描述推薦 | 您現在可以上傳本機檔案，建立機器學習產生的結構描述，而無需手動建立結構描述。 從 [!UICONTROL 來源] 工作區、上傳範例CSV檔案，以及Adobe機器學習演演算法會根據目標欄位為您建議結構描述。 請參閱 [檔案](../../ingestion/tutorials/map-csv/recommendations.md) 以取得詳細資訊。」 |

{style="table-layout:auto"}

**新XDM元件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 类 | [[!UICONTROL 選件專案]](https://github.com/adobe/xdm/pull/1678/files) | 代表選件的類別。 |
| 类 | [[!UICONTROL 決定專案]](https://github.com/adobe/xdm/pull/1678/files) | 可進行決策的專案。 決策程式的輸出是一或多個決策專案。 |
| 类 | [[!UICONTROL 媒體工作階段伺服器逾時]](https://github.com/adobe/xdm/pull/1676/files) | 這表示在使用者最後一次已知互動和工作階段關閉時刻之間經過的時間量（以秒為單位）。 |
| 欄位群組 | [[!UICONTROL XDM設定檔計算屬性]](https://github.com/adobe/xdm/pull/1686/files) | 這會將內部Adobe服務的計算屬性新增至傳入的客戶資料。 客戶不應使用此項來擷取資料。 |
| 数据类型 | [[!UICONTROL 退款專案]](https://github.com/adobe/xdm/pull/1685/files) | 指出退款是否與訂單相關聯，並定義退款型別、金額和相關聯的幣別。 |
| 数据类型 | [[!UICONTROL 類別資料]](https://github.com/adobe/xdm/pull/1677/files) | 此新資料型別代表產品的類別。 |
| 架构 | [[!UICONTROL Adobe Target分類欄位]](https://github.com/adobe/xdm/pull/1682/files) | 已為目標分類資料集建立新的XDM結構描述。 它包含一組中繼資料欄位，可分類Target活動和體驗。 |

{style="table-layout:auto"}

**已更新XDM元件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 欄位群組 | [[!UICONTROL 內容元件詳細資料]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` 「 」已移除 [!UICONTROL 內容元件詳細資料] |
| 欄位群組 | [[!UICONTROL AJO實體標籤]](https://github.com/adobe/xdm/pull/1672/files) | 已新增AJO實體標籤至 [!UICONTROL ajo實體欄位]，對應至歷程或行銷活動 |
| 欄位群組 | （多個） | 已新增多個欄位 [[!UICONTROL Journey Orchestration步驟事件常見欄位]](https://github.com/adobe/xdm/pull/1671/files) |
| 欄位群組 | （多個） | [已新增多個XDM事件型別 [!UICONTROL 媒體報告]](https://github.com/adobe/xdm/pull/1670/files). |
| 字段组 | [!UICONTROL Workfront變更事件] | 此 `Full Record` 和 `Accessor Employee Ids` 欄位群組已新增。 |
| 数据类型 | [[!UICONTROL 產品清單專案]](https://github.com/adobe/xdm/pull/1685/files) | 此 [!UICONTROL 退款金額] 已新增，以表示該料號的退款金額（若有的話）。 |
| 数据类型 | [[!UICONTROL 訂購 ]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL 退款清單] 已新增至此訂單的退款清單。 |
| 数据类型 | [[!UICONTROL 產品清單專案 ]](https://github.com/adobe/xdm/pull/1677/files) | 已將產品類別新增到此產品的類別資料清單中。 |
| 資料型別 | [!UICONTROL 工作階段詳細資訊] | 已新增 `pev3` 字串欄位， [表示用於報告的媒體資料流的型別](https://github.com/adobe/xdm/pull/1676/files). 另外新增 `pccr` 屬性指出是否發生重新導向。 |
| 資料型別 | [!UICONTROL 請購單清單] | 提供 [請購單清單屬性](https://github.com/adobe/xdm/pull/1675/files). 包括名稱、ID和說明。 |
| 資料型別 | [!UICONTROL Commerce] | 此 [Commerce資料型別已更新](https://github.com/adobe/xdm/pull/1675/files) 要包含 `requisitionListOpens`， `requisitionListAdds`， `requisitionListRemovals`、和 `requisitionList`. |

{style="table-layout:auto"}

如需Platform中XDM的詳細資訊，請閱讀 [XDM系統總覽](../../xdm/home.md).

## 查询服务 {#query-service}

查詢服務可讓您使用標準SQL在Adobe Experience Platform中查詢資料 [!DNL Data Lake]. 您可以聯結Data Lake的任何資料集，並將查詢結果擷取為新資料集，以用於報表、Data Science Workspace或內嵌到即時客戶個人檔案中。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 加速存放區上以屬性為基礎的存取控制 | 使用屬性式存取控制搭配Data Distiller來定義對加速存放區上所有資料集的存取控制。 這可控制對由使用者建立並儲存在加速存放區的自訂資料模型的存取，以便支援自訂儀表板。 |

{style="table-layout:auto"}

如需查詢服務的詳細資訊，請參閱 [查詢服務總覽](../../query-service/home.md).

## Real-Time Customer Data Platform B2B 版 {#b2b}

Real-Time CDP B2B Edition以Real-time Customer Data Platform (Real-Time CDP)為基礎，專為以B2B服務模式運作的行銷人員所打造。 它會整合來自多個來源的資料，並將其合併為單一檢視的人員與帳戶設定檔。 此統一的資料可讓行銷人員精準鎖定特定對象，並透過所有可用管道吸引這些對象。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| Bugfix | 為了更準確地呈現您系統中的設定檔，系統不再將內部設定檔納入Real-time Customer Data Platform B2B版本的總設定檔計數或可定址對象量度中。 從今天開始，您可能會看到設定檔總數/可定址對象量度有一次性的下降。 未清除任何資料，這只是計數變更。 如有任何疑問，請聯絡您的Adobe主管 |

{style="table-layout:auto"}

若要進一步瞭解Real-Time CDP B2B版本，請閱讀 [Real-Time CDP B2B版本概觀](../../rtcdp/overview.md).

## 分段服务 {#segmentation}

[!DNL Segmentation Service] 透過描述可區分客戶群內可銷售人員群組的條件，來定義設定檔的特定子集。 區段能以記錄資料（例如人口資訊）或代表客戶與品牌互動的時間序列事件為基礎。

**新功能或更新功能**

| 功能 | 描述 |
| ------- | ----------- |
| 設定檔量度 | 為了讓您更準確地表示設定檔量度，會合併成員資格劃分和流失量度，而且計算期間為24小時。 如需詳細資訊，請參閱 [分段UI指南](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

如需詳細資訊，請參閱 [!DNL Segmentation Service]，請參閱 [區段概觀](../../segmentation/home.md).

## 源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，並允許您使用Platform服務來建構、加標籤及增強這些資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 的Beta版可用性 [!DNL Chatlio] | 此 [!DNL Chatlio] 來源現在提供測試版。 使用 [!DNL Chatlio] 串流的來源 [!DNL Chatlio] 要Experience Platform的事件資料。 如需詳細資訊，請閱讀 [[!DNL Chatlio] 概觀](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| 的Beta版可用性 [!DNL Customer.io] | 此 [!DNL Customer.io] 來源現在提供測試版。 使用 [!DNL Customer.io] 將您的客戶事件資料串流到Experience Platform的來源。 如需詳細資訊，請閱讀 [[!DNL Customer.io] 概觀](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| 的Beta版可用性 [!DNL Pendo] | 此 [!DNL Pendo] 來源現在提供測試版。 使用 [!DNL Pendo] 將您的產品分析資料串流到Experience Platform的來源。 如需詳細資訊，請閱讀 [[!DNL Pendo] 概觀](../../sources/connectors/analytics/pendo-webhook.md). |
| 支援草稿資料流 | 您現在可以使用流量服務API將資料流設定為草稿狀態。 草擬的資料流稍後可以更新並發佈新資訊。 如需詳細資訊，請閱讀以下指南： [將您的來源資料流設定為草稿](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

若要進一步瞭解來源，請閱讀 [來源概觀](../../sources/home.md).

---
title: Adobe Experience Platform發行說明2023年2月
description: Adobe Experience Platform的2023年2月發行說明。
exl-id: 1c30a646-d9f8-4749-ac25-40bc48365a40
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1293'
ht-degree: 4%

---

# Adobe Experience Platform 发行说明

**发行日期：2023 年 2 月 22 日**

Adobe Experience Platform 现有功能的更新包括：

- [資料彙集](#data-collection)
- [[!DNL Destinations]](#destinations)
- [體驗資料模型(XDM)](#xdm)
- [查询服务](#query-service)
- [Real-Time Customer Data Platform B2B 版](#b2b)
- [源](#sources)

## 資料彙集 {#data-collection}

Adobe Experience Platform提供了一套技術，可讓您收集使用者端客戶體驗資料，並將其傳送至Adobe Experience Platform Edge Network，在那裡可以擴充和轉換資料，並將其分發到Adobe或非Adobe目的地。

### Assurance {#assurance}

Adobe保證可讓您檢查、校樣、模擬及驗證在您的行動應用程式中收集資料或提供體驗的方式。

**新功能或更新功能**

| 功能 | 描述 |
| ------- | ----------- |
| 公用API | Adobe保證API現已可用。 Assurance API是API的集合，可讓使用者在裝備Mobile SDK的Adobe保證擴充功能時，測試並偵錯自己的網頁和行動應用程式。 若要進一步瞭解Assurance API，請閱讀 [Assurance API概述](https://developer.adobe.com/adobe-assurance-public-apis/). |

{style="table-layout:auto"}

如需Assurance的詳細資訊，請閱讀 [保證檔案](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先建立的與目標平台的整合，可無縫啟用Adobe Experience Platform的資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。

**新功能或更新功能** {#destinations-new-updated-features}

| 功能 | 描述 |
| ----------- | ----------- |
| [同意原則增強功能](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) 與整合 [檔案型（批次）目的地](/help/destinations/destination-types.md#file-based) | <p> 當設定檔不再符合約意原則時，Experience Platform現在會主動將其原則退出傳達給檔案型目的地。 此程式遵循 [2023年2月發行](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) 串流目的地的相同功能。 </p> <p> <b>注意</b>：此功能僅適用於 **[!UICONTROL 隱私權與安全遮蔽]**，以及 **[!UICONTROL Healthcare Shield]**. </p> |

{style="table-layout:auto"}

**新增或更新後的檔案** {#destinations-new-updated-documentation}

| 文档 | 描述 |
| ----------- | ----------- |
| 目的地如何運作檔案 | <p>我們根據使用者的常見問題，發表了三篇說明目標如何運作的新文章：</p> <p><ul><li>[目的地中可設定和常用的匯出設定](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[不同目的地型別的設定檔匯出行為](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[目的地啟用工作流程中的身分處理](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

如需有關目的地的詳細一般資訊，請參閱 [目的地概觀](../../destinations/home.md).

## 體驗資料模型(XDM) {#xdm}

XDM是開放原始碼規格，針對帶入Adobe Experience Platform的資料提供通用結構和定義（結構描述）。 藉由遵守XDM標準，所有客戶體驗資料都可以整合到通用表示中，以更快、更整合的方式提供深入分析。 您可以從客戶動作獲得有價值的深入分析、透過區段定義客戶對象，以及使用客戶屬性進行個人化。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 透過UI棄用欄位 | 您現在可以 [在擷取資料後，棄用結構描述中的欄位](../../xdm/tutorials/field-deprecation-ui.md). XDM欄位棄用可讓您從UI檢視中移除欄位，同時保留這些欄位以供使用。 您可以視需要再次顯示已棄用的欄位，任何參考欄位的區段、查詢或下游解決方案都將照常執行。 |

{style="table-layout:auto"}

**新XDM元件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 类 | [[!UICONTROL XDM個別潛在客戶設定檔]](https://github.com/adobe/xdm/pull/1669/files) | XDM Individual Prospect Profile類別可匯入合作夥伴提供的ID。 |

{style="table-layout:auto"}

**已更新XDM元件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 字段组 | [!UICONTROL 頻率上限限制] | 此 [!UICONTROL 頻率上限限制] 欄位群組已 [更新以支援重複和自訂事件](https://github.com/adobe/xdm/pull/1641/files). |
| 資料型別 | [!UICONTROL 網頁反向連結] | 網頁反向連結屬性已 [更新以包含 `xdm:linkName` 和 `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). 這些分別是上一頁所選HTML元素的名稱和區域。 |
| 欄位群組 | [!UICONTROL AdobeCJM ExperienceEvent — 訊息互動細節] | [此 [!UICONTROL 追蹤器URL] 欄位已新增](https://github.com/adobe/xdm/pull/1665/files) 至 [!UICONTROL AdobeCJM ExperienceEvent]. 此追蹤器會提供使用者選取的URL。 |
| 欄位群組 | [!UICONTROL AdobeCJM ExperienceEvent — 訊息互動細節] | [空白 `meta:enum` 屬性已移除](https://github.com/adobe/xdm/pull/1668/files) 從URL [!UICONTROL 追蹤型別] 欄位。 |
| 資料型別 | [!UICONTROL 媒體資訊] | [來自的規則運算式模式 `videoSegment` 中的屬性 [!UICONTROL 媒體資訊] 資料型別已移除](https://github.com/adobe/xdm/pull/1667/files). |

{style="table-layout:auto"}

如需Platform中XDM的詳細資訊，請閱讀 [XDM系統總覽](../../xdm/home.md). &#x200B;

## 查询服务 {#query-service}

查詢服務可讓您使用標準SQL在Adobe Experience Platform中查詢資料 [!DNL Data Lake]. 您可以聯結Data Lake的任何資料集，並將查詢結果擷取為新資料集，以用於報表、Data Science Workspace或內嵌到即時客戶個人檔案中。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 為具有SQL的設定檔啟用資料集 | [在CTAS查詢中使用LABEL，讓資料集「已啟用設定檔」](../../query-service/sql/syntax.md#create-table-as-select)，或使用ALTER來更新要針對設定檔啟用的現有資料集。 您可以使用此延伸的SQL建構，針對您的Real-Time Customer Profile業務使用案例的衍生屬性提供順暢支援。 請參閱 [衍生屬性檔案的無縫SQL流程](../../query-service/data-distiller/derived-attributes/seamless-sql-flow.md) 以取得更多詳細資料。 |
| 監視排定的查詢 | 使用 [排定的查詢索引標籤](../../query-service/ui/monitor-queries.md) 以尋找關於查詢執行的重要資訊，並訂閱警示。 監視排程詳細資料、狀態，以及失敗時的錯誤訊息/代碼的查詢。 |
| 切換自動完成功能 | 透過以下方式消除某些中繼資料命令並縮短處理時間 [切換查詢編輯器自動完成功能](../../query-service/ui/user-guide.md#auto-complete). 此功能會在您編寫查詢時，自動建議查詢的潛在SQL關鍵字和表格詳細資訊。 |
| 資料集範例 | 在查詢中指定取樣率，並 [使用資料集範例建立統一的隨機範例](../../query-service/essential-concepts/dataset-samples.md)，或根據特定條件建立條件式範例。 |

{style="table-layout:auto"}

如需查詢服務的詳細資訊，請參閱 [查詢服務總覽](../../query-service/home.md).


## Real-Time Customer Data Platform B2B 版 {#b2b}

Real-Time CDP B2B Edition以Real-time Customer Data Platform (Real-Time CDP)為基礎，專為以B2B服務模式運作的行銷人員所打造。 它會整合來自多個來源的資料，並將其合併為單一檢視的人員與帳戶設定檔。 此統一的資料可讓行銷人員精準鎖定特定對象，並透過所有可用管道吸引這些對象。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 啟用相關的帳戶服務 | 新的切換功能可讓您在您的帳戶上啟用相關的帳戶服務。 如需詳細資訊，請閱讀以下指南： [啟用相關的帳戶服務](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style="table-layout:auto"}

若要進一步瞭解Real-Time CDP B2B版本，請閱讀 [Real-Time CDP B2B版本概觀](../../rtcdp/overview.md).

## 源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，並允許您使用Platform服務來建構、加標籤及增強這些資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

**更新的功能**

| 功能 | 描述 |
| --- | --- |
| 透過指定訂閱層級存取權 [!DNL Google PubSub] | 您現在可以使用定義特定主題訂閱的存取權 [!DNL Google PubSub] 來源是在驗證時提供訂閱ID。 如需詳細資訊，請閱讀 [!DNL Google PubSub] 驗證教學課程 [使用流量服務API](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) 或 [平台UI](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| 從擷取自訂活動資料 [!DNL Marketo] | 您現在可以從的自訂活動資料帶 [!DNL Marketo] 執行個體以Experience Platform。 若要內嵌自訂活動資料，您必須在B2B活動結構描述中設定自訂活動欄位群組，並使用活動資料集建立資料流。 資料流完成後，擷取的資料集將包含中的標準和自訂活動 [!DNL Marketo] 執行個體。 然後，您可以使用 [查詢服務](../../query-service/home.md) 以存取您在Platform上的自訂活動記錄。 如需詳細資訊，請閱讀以下指南： [為自訂活動資料建立資料流](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| 排除無人認領的帳戶 [!DNL Marketo] | 您現在可以設定在為公司資料建立資料流時，是否要從擷取中排除或包含無人認領的帳戶。 如需詳細資訊，請閱讀以下指南： [為建立來源連線和資料流 [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style="table-layout:auto"}

若要進一步瞭解來源，請閱讀 [來源概觀](../../sources/home.md).

---
title: Adobe Experience Platform發行說明2023年1月
description: Adobe Experience Platform的2023年1月發行說明。
exl-id: 461898ce-5683-4ab1-9167-ac25843a1ff8
source-git-commit: a0400ab255b3b6a7edb4dcfd5c33a0f9e18b5157
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 6%

---

# Adobe Experience Platform 发行说明

**发行日期：2023 年 1 月 25 日**

Adobe Experience Platform 现有功能的更新包括：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [Assurance](#assurance)
- [資料彙集](#data-collection)
- [[!DNL Destinations]](#destinations)
- [體驗資料模型(XDM)](#xdm)
- [实时客户资料](#profile)
- [分段服务](#segmentation)
- [源](#sources)

## 人工智慧/機器學習服務 {#ai-ml}

人工智慧和機器學習服務可讓行銷分析師和從業人員在客戶體驗使用案例中運用AI/ML的強大功能。 這可讓行銷分析人員使用業務層級設定，針對公司需求設定預測，而不需要資料科學專業知識。

### 归因人工智能

Attribution AI用於將點數歸因於導致轉換事件的接觸點。 营销人员可利用此功能，促进量化客户旅程中每个营销接触点的营销影响。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| HIPAA 准备就绪 | Healthcare Shield客戶現在可以在Attribution AI和某些其他Experience Platform型應用程式中接收、使用、維護或傳輸受保護的健康資訊。 Healthcare Shield適用於身為HIPAA涵蓋實體或業務夥伴的醫療保健客戶。 如需詳細資訊，請閱讀以下檔案： [HIPAA與Adobe產品與服務](https://www.adobe.com/cn/trust/compliance/hipaa-ready.html) |
| 編輯其他分數資料集欄 | 您現在可以在編輯現有模型時，新增或移除其他分數資料集欄（報告欄）。 這可擴充歸因分數的彈性，在建立模型後，為您提供其他維度的深入分析。 請參閱 [歸因UI指南](../../intelligent-services/attribution-ai/user-guide.md) 以深入瞭解。 |

{style="table-layout:auto"}

請參閱 [AI/ML服務](../../intelligent-services/attribution-ai/overview.md) 概覽以取得詳細資訊。

### Customer AI

適用於Real-time Customer Data Platform的Customer AI可產生自訂傾向評分，例如大規模個別設定檔的流失和轉換情形。 这无需通过将业务需求转变为机器学习问题、选择算法、培训或部署即可完成。

**更新的功能**

| 功能 | 描述 |
| ------- | ----------- |
| HIPAA 准备就绪 | Healthcare Shield客戶現在可以在Customer AI中接收、使用、維護或傳輸受保護的健康資訊，用於Real-time Customer Data Platform和某些其他Experience Platform型應用程式。 Healthcare Shield適用於身為HIPAA涵蓋實體或業務夥伴的醫療保健客戶。 如需詳細資訊，請參閱以下檔案： [HIPAA與Adobe產品與服務](https://www.adobe.com/cn/trust/compliance/hipaa-ready.html) |

{style="table-layout:auto"}

請參閱 [AI/ML服務](../../intelligent-services/customer-ai/overview.md) 概覽以取得詳細資訊。

## Assurance {#assurance}

Adobe保證可讓您檢查、校樣、模擬及驗證在您的行動應用程式中收集資料或提供體驗的方式。

**新功能或更新功能**

| 功能 | 描述 |
| ------- | ----------- |
| 驗證編輯器 | 已新增驗證編輯器的新增強功能。 這些增強功能包括驗證欄、新的程式碼建置工具和改善的檢視。 |

{style="table-layout:auto"}

如需Assurance的詳細資訊，請閱讀 [保證檔案](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## 資料彙集 {#data-collection}

Adobe Experience Platform提供了一套技術，可讓您收集使用者端客戶體驗資料，並將其傳送至Adobe Experience Platform Edge Network，在那裡可以擴充和轉換資料，並將其分發到Adobe或非Adobe目的地。

**新功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| 新主畫面 | 資料收集UI的首頁已更新，加入實用的入門資訊和連結，以簡化生產力。 这包括：<ol><li>開始使用的檔案和建議工作流程</li><li>最近使用的屬性、規則和資料元素</li><li>熱門擴充功能</li><li>包含快速安裝功能的新擴充功能更新</li></ol> |
| 傳送資料至 [!DNL Google Ads] 使用事件轉送 | 您現在可以使用 [[!DNL Google Ads Enhanced Conversions] API擴充功能](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 用於事件轉送，結合 [Google Oauth 2秘密](../../tags/ui/event-forwarding/secrets.md#google-oauth2)，以安全地傳送伺服器端資料至 [!DNL Google Ads] 即時。 |

{style="table-layout:auto"}

## 目的地（更新日期： 2月2日） {#destinations}

[!DNL Destinations] 是預先建立的與目標平台的整合，可無縫啟用Adobe Experience Platform的資料。 您可以使用目的地，針對跨頻道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例，啟用已知和未知的資料。

**新目的地**

| 目标 | 描述 |
| ----------- | ----------- |
| [(Beta) Adobe Experience Cloud受眾連線](../../destinations/catalog/adobe/experience-cloud-audiences.md) | 使用 [!UICONTROL (Beta) Adobe Experience Cloud對象] 此連線可將Experience Platform的區段分享至各種Experience Platform解決方案，例如Audience Manager、Analytics、Advertising Cloud、Adobe Campaign、Target或Marketo。 |
| [Pega設定檔連線](../../destinations/catalog/personalization/pega-profile.md) | 使用 [!DNL Pega Profile Connector] 在Adobe Experience Platform中建立與您的的即時輸出連線 [!DNL Amazon] S3儲存空間，可定期從Adobe Experience Platform將設定檔資料匯出為CSV檔案，並放入您自己的S3儲存貯體。 在 [!DNL Pega Customer Decision Hub]，您可以排程資料工作，以從S3儲存空間匯入此設定檔資料來更新 [!DNL Pega Customer Decision Hub] 設定檔。 |
| [(Beta)交易台CRM EU連線](../../destinations/catalog/advertising/tradedesk-emails.md) | 隨著EUID (European Unified ID)的推出，您現在可以看到兩個 [!DNL The Trade Desk - CRM] 中的目的地 [目的地目錄](/help/destinations/catalog/overview.md). <ul><li> 若您的資料來源是歐盟，請使用 **[!DNL The Trade Desk - CRM (EU)]** 目的地。</li><li> 如果您在APAC或NAMER地區取得資料，請使用 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 目的地。 </li></ul> |

**新功能或更新功能** {#destinations-new-updated-functionality}

| 功能 | 描述 |
| ----------- | ----------- |
| 與串流目的地整合的付費媒體同意原則增強功能 | 一個 [增強同意原則執行](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) 於 [串流目的地](/help/destinations/destination-types.md#streaming-destinations) 適用於付費媒體啟用使用案例。 當設定檔不再符合約意原則時，Experience Platform現在會主動將其原則退出傳達給串流目的地。 <br> <b>注意</b>：此功能僅適用於 **[!UICONTROL 隱私權與安全遮蔽]**，以及 **[!UICONTROL Healthcare Shield]**. |
| 適用於Beta版雲端儲存空間目的地聯結器的新分隔符號選項 | 三個新的分隔符號選項（冒號） `:`，垂直號，分號 `;`)現在可用於新的測試版雲端儲存目標 —  [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md)， [(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md)， [(Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md)， [(Beta)資料登陸區域](/help/destinations/catalog/cloud-storage/data-landing-zone.md)， [(Beta) Google雲端儲存空間](/help/destinations/catalog/cloud-storage/google-cloud-storage.md)， [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br> 閱讀支援的 [檔案格式選項](/help/destinations/ui/batch-destinations-file-formatting-options.md) 適用於檔案型目的地。 |
| 新的選用引數可用於 [客戶資料欄位](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md) 中的設定 [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`：當您需要建立客戶資料欄位時，使用此引數，該欄位的值在使用者組織設定的所有目的地資料流中必須是唯一的。 <br> 例如， **[!UICONTROL 整合別名]** 中的欄位 [[!UICONTROL 自訂個人化]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) 目的地必須是唯一的，這表示流向此目的地的兩個獨立資料流不能在此欄位中有相同的值。 |

**修正和增強功能** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>修正或增強功能</b></td>
        <td><b>描述</b></td>
    </tr>
    <tr>
        <td>更新檔案型目的地的匯出行為(PLAT-123316)</td>
        <td>我們已修正以下專案的行為問題： <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mandatory-attributes">強制屬性</a> 將資料檔案匯出至批次目的地時。 <br> 先前，輸出檔案中的每個記錄都確認包含兩者： <ol><li>「 」的非空值 <code>mandatoryField</code> 欄和</li><li>至少一個其他非必要欄位上的非空值。</li></ol> 第二個條件已移除。 因此，您可能會在匯出的資料檔案中看到更多輸出列，如以下範例所示：<br> <b> 2023年1月版本之前的範例行為 </b> <br> 必要欄位： <code>emailAddress</code> <br> <b>輸入資料以啟動</b> <br><table><thead><tr><th>名字</th><th>電子郵件地址</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>啟用輸出</b> <br><table><thead><tr><th>名字</th><th>電子郵件地址</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> 2023年1月發行後的範例行為 </b> <br> <b>啟用輸出</b> <br> <table><thead><tr><th>名字</th><th>電子郵件地址</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>必要對應和重複對應的UI和API驗證(PLAT-123316)</td>
        <td>現在，當發生下列情況時，UI和API會依照以下方式強制執行驗證 <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mapping">對應欄位</a> 在啟用目的地工作流程中：<ul><li><b>必要的對應</b>：如果目的地已由目的地開發人員透過所需的對應(例如 <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html?lang=en">Google Ad Manager 360</a> 目的地)，則使用者在啟動資料至目的地時，需要新增這些必要的對應。 </li><li><b>複製對應</b>：在啟動工作流程的對映步驟中，您可以在來源欄位中新增重複值，但不能在目標欄位中新增。 請參閱下表，以取得允許和禁止的對應組合範例。 <br><table><thead><tr><th>允許/禁止</th><th>源字段</th><th>目標欄位</th></tr></thead><tbody><tr><td>允许</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>電子郵件別名2</li></ul></td></tr><tr><td>已禁止</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

如需有關目的地的詳細一般資訊，請參閱 [目的地概觀](../../destinations/home.md).

## 體驗資料模型(XDM) {#xdm}

XDM是開放原始碼規格，針對帶入Adobe Experience Platform的資料提供通用結構和定義（結構描述）。 藉由遵守XDM標準，所有客戶體驗資料都可以整合到通用表示中，以更快、更整合的方式提供深入分析。 您可以從客戶動作獲得有價值的深入分析、透過區段定義客戶對象，以及使用客戶屬性進行個人化。

**新功能或更新功能**

| 功能 | 描述 |
| --- | --- |
| 結構描述樹狀結構顯示名稱改良 | 以前，欄位名稱會顯示在UI中，但現在，結構畫布上的結構描述欄位顯示名稱更易於閱讀。 |

**新XDM元件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 类 | [[!UICONTROL 转化]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | 追蹤貨幣轉換等轉換資料的類別。 |
| 字段组 | [[!UICONTROL 幣別兌換率詳細資料]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | 的欄位群組 [!UICONTROL 轉換] 類別，擷取與貨幣轉換相關的其他詳細資訊。 |
| 字段组 | [[!UICONTROL 同意原則評估結果與中繼資料對應]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | 擷取多個同意政策的評估結果的詳細資訊，包括同意政策進入和存在的相關中繼資料資訊。 |

**已更新XDM元件**

| 组件类型 | 名称 | 描述 |
| --- | --- | --- |
| 資料型別 | [[!UICONTROL 廣告詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | 此 `ID` 欄位已重新命名為 `name`，以及上一個 `name` 欄位現在為 `friendlyName`. |
| 資料型別 | [[!UICONTROL 決定主張詳細資訊]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | 已新增 `selectionStrategy` 擷取選擇策略詳細資料的欄位。 |
| 字段组 | [[!UICONTROL 體驗事件 — 主張互動]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | 欄位群組現在與 [!UICONTROL 歷程步驟事件] 類別。 |
| 資料型別 | [[!UICONTROL 錯誤詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | 此 `ID` 欄位已重新命名為 `name`. |
| 資料型別 | [[!UICONTROL 媒體資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | 將模式變更還原為視訊區段屬性。 |
| 資料型別 | [[!UICONTROL Qoe資料詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 已移除 `droppedFrameCount` 欄位。 |
| 資料型別 | [[!UICONTROL 工作階段詳細資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 已重新命名 `isAuthorized` 欄位至 `authorized`，並更新其 `type` 變更為字串（先前為布林值）。 |
| 資料型別 | [[!UICONTROL 送貨]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 新增幾個新欄位： `shipDate`， `trackingNumber`、和 `trackingURL`. |
| 字段组 | [[!UICONTROL ajo實體欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | 新增幾個新欄位： `journeyNodeID`， `journeyNodeName`、和 `journeyModeType`. |
| 字段组 | [[!UICONTROL 消費者體驗事件]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | 欄位群組現在也與相容 [!UICONTROL 摘要量度] 類別。 |
| 字段组 | [[!UICONTROL 產品觸發程式]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | 此 `productTriggers` 欄位現在巢狀於 `weather` 物件。 |
| 字段组 | [[!UICONTROL 相對觸發程式]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | 此 `relativeTriggers` 欄位現在巢狀於 `weather` 物件。 |
| 字段组 | [[!UICONTROL 嚴重觸發程式]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 此 `severeTriggers` 欄位現在巢狀於 `weather` 物件。 |
| 字段组 | [[!UICONTROL 天氣觸發程式]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 此 `weatherTriggers` 欄位現在巢狀於 `weather` 物件。 |
| 字段组 | [[!UICONTROL XDM相關的商業帳戶]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | 欄位群組現在為穩定。 |

{style="table-layout:auto"}

如需有關Platform中XDM的詳細資訊，請參閱 [XDM系統總覽](../../xdm/home.md).

## 实时客户资料 {#profile}

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，無論客戶在哪裡或何時與您的品牌互動。 透過即時客戶個人檔案，您可以檢視結合來自多個管道（包括線上、離線、CRM和第三方資料）之資料的每個個別客戶的整體檢視。 設定檔可讓您將客戶資料整合到統一的檢視中，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

**即將淘汰** {#deprecation}

為了移除區段成員資格生命週期中的備援， `Existing` 狀態將從以下內容棄用： [區段會籍對應](../../xdm/field-groups/profile/segmentation.md) 於2023年3月底。 後續公告將包含確切的淘汰日期。

棄用後，區段中符合資格的設定檔將呈現為 `Realized` 而不符合資格的設定檔將繼續顯示為 `Exited`. 這將帶來與檔案型目的地的等同性，具有 `Active` 和 `Expired` 區段狀態。

如果您使用的是 [企業目的地](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis、Azure事件中樞、HTTP API)，並已根據 `Existing` 狀態。 若情況如此，請檢閱您的下游整合。 如果您想要在超過特定時間後識別新合格的設定檔，請考慮使用以下組合 `Realized` 狀態和 `lastQualificationTime` 區段會籍對映中的。 如需詳細資訊，請洽詢您的Adobe代表。

若要進一步瞭解即時客戶個人檔案，包括使用個人檔案資料的教學課程和最佳實務，請先閱讀 [即時客戶個人檔案總覽](../../profile/home.md).

## 分段服务 {#segmentation}

[!DNL Segmentation Service] 透過描述可區分客戶群內可銷售人員群組的條件，來定義設定檔的特定子集。 區段能以記錄資料（例如人口資訊）或代表客戶與品牌互動的時間序列事件為基礎。

**新功能或更新功能**

| 功能 | 描述 |
| ------- | ----------- |
| 在區段產生器中匯入大量值 | 「區段產生器」現在支援匯入多個值，其方式為上傳CSV或TSV檔案，或手動插入逗號分隔的值。 如需詳細資訊，請參閱 [區段產生器指南](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |
| 外部對象成員資格到期 | 依預設，外部對象會籍會保留30天。 若要保留時間更長，請使用 `validUntil` 擷取對象資料期間的欄位。 |
| 平台產生的區段會籍有效期 | 任何位於中的區段會籍 `Exited` 狀態持續30天以上，根據 `lastQualificationTime` 欄位可能會刪除。 |

{style="table-layout:auto"}

如需詳細資訊，請參閱 [!DNL Segmentation Service]，請參閱 [區段概觀](../../segmentation/home.md).

## 源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，並允許您使用Platform服務來建構、加標籤及增強這些資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆設定各種資料提供者的來源連線。 這些來源連線可讓您驗證並連線至外部儲存系統和CRM服務、設定擷取執行的時間，以及管理資料擷取輸送量。

| 功能 | 描述 |
| --- | --- |
| 允許使用者存取雲端儲存空間來源的子資料夾 | 建立新帳戶時，您現在可以定義雲端儲存空間來源特定子資料夾的存取權。 建立後，使用者將只能從允許的子資料夾存取資料。 此功能適用於下列雲端儲存空間來源： [Azure Blob儲存體](../../sources/connectors/cloud-storage/blob.md)， [Google雲端儲存空間](../../sources/connectors/cloud-storage/google-cloud-storage.md)， [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)、和 [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| 的Beta版可用性 [!DNL SugarCRM] | [!DNL SugarCRM] 來源現在提供測試版。 使用 [!DNL SugarCRM Accounts & Contacts] 和 [!DNL SugarCRM Events] 來源，從您的網站帶入資料 [!DNL SugarCRM] 要Experience Platform的帳戶。 如需詳細資訊，請閱讀 [[!DNL SugarCRM] 概觀](../../sources/connectors/crm/sugarcrm.md). |

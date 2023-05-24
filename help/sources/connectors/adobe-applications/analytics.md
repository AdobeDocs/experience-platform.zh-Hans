---
title: 報告套裝資料的Adobe Analytics來源聯結器
description: 本檔案提供Analytics概觀及說明Analytics資料的使用案例。
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 83ce7d46e4e64fbe961c964ed5a17ec12a7ec15f
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 7%

---

# 报告包数据的 Adobe Analytics Source Connector

Adobe Experience Platform可讓您透過Analytics來源聯結器內嵌Adobe Analytics資料。 此 [!DNL Analytics] 來源聯結器串流資料收集者 [!DNL Analytics] 即時轉換至Platform，轉換SCDS格式 [!DNL Analytics] 資料匯入 [!DNL Experience Data Model] (XDM)欄位供平台使用。

本檔案提供下列專案的概觀： [!DNL Analytics] 和說明的使用案例 [!DNL Analytics] 資料。

## Adobe Analytics和Analytics資料

[!DNL Analytics] 是一款強大的引擎，可協助您進一步瞭解客戶、客戶如何與您的Web屬性互動、瞭解您的數位行銷支出在何處有效，並找出需改善的領域。 [!DNL Analytics] 每年處理數萬億次的Web交易，以及 [!DNL Analytics] 來源聯結器可讓您輕鬆利用這項豐富的行為資料，並將 [!DNL Real-Time Customer Profile] 幾分鐘內。

![說明不同Adobe應用程式(包括Adobe Analytics)之資料歷程的圖形。](./images/analytics-data-experience-platform.png)

高階， [!DNL Analytics] 從全球各地的各種數位頻道和多個資料中心收集資料。 收集到資料後，會套用訪客識別、細分和轉換架構(VISTA)規則和處理規則來塑造傳入的資料。 原始資料經過此輕量級處理後，即可由以下人員使用 [!DNL Real-Time Customer Profile]. 在上述平行處理程式中，相同的已處理資料會經過微批次處理，並擷取至Platform資料集，供下列人員使用： [!DNL Data Science Workspace]， [!DNL Query Service]和其他資料探索應用程式。

請參閱 [處理規則概觀](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=zh-Hans) 以取得處理規則的詳細資訊。

## 體驗資料模型(XDM)

XDM是公開記錄的規格，提供通用結構和定義，以供應用程式用於與Experience Platform的服務通訊。

遵守XDM標準可讓資料以統一方式合併，讓您更輕鬆地傳送資料和收集資訊。

若要進一步瞭解XDM，請參閱 [XDM系統總覽](../../../xdm/home.md).

## 如何將欄位從Adobe Analytics對應至XDM？

>[!IMPORTANT]
>
>「資料準備」轉換可能會增加整個資料流程的延遲。 新增的額外延遲因轉換邏輯的複雜度而異。

建立來源連線以帶來 [!DNL Analytics] 資料使用Platform使用者介面進入Experience Platform，資料欄位會自動對應並擷取到 [!DNL Real-Time Customer Profile] 幾分鐘內。 有關建立來源連線的指示 [!DNL Analytics] 使用Platform UI，請參閱 [Analytics來源聯結器教學課程](../../tutorials/ui/create/adobe-applications/analytics.md).

有關之間發生的欄位對應的詳細資訊 [!DNL Analytics] 和Experience Platform，請參閱 [Adobe Analytics欄位對應](./mapping/analytics.md) 指南。

## Platform上Analytics資料的預期延遲為何？

下表列出Platform上Analytics資料的預期延遲。 延遲會依客戶組態、資料量和消費者應用程式而有所不同。 例如，如果Analytics實作設定為 `A4T` 管道的延遲將增加到5-10分鐘。

| Analytics 数据 | 預期延遲 |
| -------------- | ---------------- |
| 將新資料新增至 [!DNL Real-Time Customer Profile] (A4T **not** enabled) | &lt; 2 分钟 |
| 將新資料新增至 [!DNL Real-Time Customer Profile] (A4T **是** enabled) | 最多30分鐘 |
| 將新資料新增至Data Lake | &lt; 90 分钟 |
| 少於100億個事件的回填 | &lt; 4 周 |

生產沙箱的Analytics回填預設為13個月。 對於非生產沙箱中的Analytics資料，回填會設定為三個月。 上表提到的100億個事件上限與預期延遲有關。

在生產沙箱中建立Analytics來源資料流時，會建立兩個資料流：

* 此資料流會將13個月的歷史報告套裝資料回填至Data Lake。 此資料流會在回填完成時結束。
* 將即時資料傳送至資料湖和的資料流流程 [!DNL Real-Time Customer Profile]. 此資料流會持續執行。

>[!NOTE]
>
>Analytics回填資料未內嵌至 [!DNL Profile] 因此不會計入授權設定檔中。

## 中的主要識別碼 [!DNL Analytics] 資料

來自的每次點選 [!DNL Analytics] 來源聯結器包含取決於ECID或AAID存在與否的主要識別碼。 如果存在ECID，則會將ECID指定為主要識別碼。 如果有AAID，則會將AAID指定為主要的。

下表提供「 」中身分識別欄位的詳細資訊 [!DNL Analytics] 資料。

| 身分欄位 | 描述 |
| --- | --- |
| AAID | AAID是Adobe Analytics中的主要裝置識別碼，並且保證存在於每個透過 [!DNL Analytics] 來源。 AAID有時稱為 *舊版Analytics ID* 或作為 `s_vi` Cookie ID。 儘管如此，仍會建立AAID，即使 `s_vi` Cookie不存在。 AAID由 `post_visid_high` 和 `post_visid_low` 中的欄 [[!DNL Analytics] 資料摘要](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). 在任何指定事件中，AAID欄位都包含單一身分識別，該身分識別可能是 [的作業順序 [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **注意**：在整個報表套裝中，AAID可能包含跨事件的多種型別。 |
| ECID | ECID (Experience CloudAdobe Analytics ID)是獨立的裝置識別碼欄位，此欄位會在 [!DNL Analytics] 是使用Experience CloudIdentity服務實作。 ECID有時也稱為MCID (Marketing CloudID)。 如果事件中存在ECID，則AAID可能會以ECID為基礎，具體取決於Analytics是否會 [寬限期](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) 已設定。 ECID由 `mcvisid` Analytics資料摘要中的。 如需ECID的詳細資訊，請參閱 [ECID概觀](../../../identity-service/ecid.md). 如需ECID如何搭配使用的詳細資訊 [!DNL Analytics]，請參閱本檔案： [Analytics與Experience CloudID請求](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html?lang=zh-Hans). |
| AACUSTOMID | Adobe Analytics AACUSTOMID是一個單獨的識別碼欄位，根據 `s.VisitorID` 中的變數 [!DNL Analytics] 實作。 AACUSTOMID由 `cust_visid` 中的欄 [[!DNL Analytics] 資料摘要](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). 如果AACUSTOMID存在，則AAID將以AACUSTOMID為基礎，因為AACUSTOMID勝過 [的作業順序 [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### 如何 [!DNL Analytics] 來源處理身分

此 [!DNL Analytics] 來源將這些身分識別以XDM形式傳遞給Experience Platform，如下所示：

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

这些字段未标记为标识。而是將相同的身分識別複製到XDM的 `identityMap` 做為機碼值組：

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

在身分對應中，如果ECID存在，則會標示為事件的主要身分。 在此情況下，AAID可能以ECID為基礎，原因如下 [Identity Service寬限期](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). 否则，会将 AAID 标记为事件的主标识。绝不会将 AACUSTOMID 标记为事件的主 ID。不過，如果AACUSTOMID存在，則AAID會以AACUSTOMID為基礎，因為操作順序是Experience Cloud的。

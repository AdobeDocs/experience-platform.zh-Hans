---
keywords: Experience Platform；快速入門；customer ai；熱門主題；customer ai輸入；customer ai輸出；資料要求
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Customer AI的資料需求
topic-legacy: Getting started
description: 進一步瞭解Customer AI使用的必要事件、輸入和輸出。
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 5f7b602b68f5cbf4b1f4b08603757b0956e36408
workflow-type: tm+mt
source-wordcount: '2484'
ht-degree: 2%

---


# Customer AI中的輸入和輸出

以下檔案概述Customer AI中使用的不同必要事件、輸入和輸出。

## 快速入门 {#getting-started}

以下是在Customer AI中建立傾向模型並識別個人化行銷目標對象的步驟：

1. 概述使用案例：傾向模型如何協助識別個人化行銷的目標對象？ 我的業務目標和達成目標的對應策略為何？ 傾向性模型在此過程中適用於何處？

2. 排定使用案例的優先順序：哪一個是業務的最高優先順序？

3. 在Customer AI中建立模型：觀看此 [快速教學課程](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html) 並參閱我們的 [UI指南](../customer-ai/user-guide/configure.md) 建立模型的逐步程式。

4. [建立區段](../customer-ai/user-guide/create-segment.md) 使用模型結果。

5. 根據這些區段採取目標業務動作。 監視結果並重複要改善的動作。

以下是您第一個模型的設定範例。  本檔案中建立的範例模型使用Customer AI模型來預測誰可能在未來30天內轉換零售業務。 輸入資料集是Adobe Analytics資料集。

| 步骤 | 定义 | 示例 |
| ---- | ------ | ------- |
| 設定 | 指定關於模型的基本資訊。 | **名稱**：鉛筆購買傾向模型 <br> **模型型別**：轉換 |
| 選取資料 | 指定用來建立模型的資料集。 | **資料集**：Adobe Analytics資料集 <br> **身分**：確認每個資料集的身分欄都設為通用身分。 |
| 定義目標 | 定義目標、合格母體、自訂事件和設定檔屬性。 | **預測目標**：選取 `commerce.purchases.value` 等於鉛筆 <br> **結果視窗**：30天。 |
| 設定選項 | 設定模型重新整理的排程並啟用設定檔的分數 | **排程**：每週 <br> **為設定檔啟用**：必須啟用此項，模型輸出才能用於分段。 |

## 資料概述 {#data-overview}

以下章節概述Customer AI中使用的不同必要事件、輸入和輸出。

Customer AI的運作方式是分析以下資料集來預測流失率（客戶何時可能停止使用產品）或轉換率（客戶何時可能購買）傾向分數：

- Adobe Analytics資料使用 [Analytics來源聯結器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Audience Manager資料使用 [Audience Manager來源聯結器](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [體驗事件資料集](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html)
- [取用者體驗事件資料集](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html#cee-schema)

如果每個資料集共用相同的身分型別（名稱空間） （例如ECID），您可以新增來自不同來源的多個資料集。 如需新增多個資料集的詳細資訊，請造訪 [Customer AI使用手冊](../customer-ai/user-guide/configure.md).

>[!IMPORTANT]
>
>來源聯結器最多需要4週的時間來回填資料。 如果您最近設定了聯結器，您應該確認資料集具有Customer AI所需的最小資料長度。 請檢閱 [歷史資料](#data-requirements) 區段，以確認您有足夠的資料可達到預測目標。

下表概述本檔案使用的一些常見術語：

| 搜索词 | 定义 |
| --- | --- |
| [體驗資料模型(XDM)](../../xdm/home.md) | XDM是基礎架構，可讓Adobe Experience Platform支援的Adobe Experience Cloud在正確的時間透過正確的管道將正確的訊息傳遞給正確的人。 Platform使用XDM系統以特定方式組織資料，以更方便用於Platform服務。 |
| [XDM 架构](../../xdm/schema/composition.md) | Experience Platform 会使用架构，以便以可重用的一致方式描述数据结构。通过在整个系统中以一致的方式定义数据，更容易保留含义并因此从数据中获取价值。在將資料內嵌至Platform之前，必須組成結構描述來說明資料結構，並對可包含在每個欄位中的資料型別提供限制。 結構描述包含一個基本XDM類別和零個或多個結構描述欄位群組。 |
| [XDM類別](../../xdm/schema/field-constraints.md) | 所有XDM結構描述都說明可分類為 `Experience Event`. 結構描述的資料行為由結構描述的類別定義，該類別在首次建立時指派給結構描述。 XDM類別說明結構描述必須包含的最小屬性數量，才能代表特定的資料行為。 |
| [字段组](../../xdm/schema/composition.md) | 定義結構描述中一或多個欄位的元件。 欄位群組會強制實施其欄位在結構描述階層中的顯示方式，因此會在其包含的每個結構描述中顯示相同的結構。 欄位群組僅與特定類別相容，由識別專案群組 `meta:intendedToExtend` 屬性。 |
| [資料型別](../../xdm/schema/composition.md) | 也可以為結構描述提供一個或多個欄位的元件。 不過，與欄位群組不同，資料型別不受限於特定類別。 這讓資料型別成為描述通用資料結構的更具彈性的選項，這些資料結構可重複用於具有不同類別的多個結構描述。 CEE和Adobe Analytics架構均支援本檔案中概述的資料型別。 |
| [实时客户资料](../../profile/home.md) | Real-time Customer Profile提供集中式消費者設定檔，用於針對性和個人化的體驗管理。 每個設定檔都包含彙總所有系統的資料，以及在您用於Experience Platform的任何系統中發生的涉及個人之事件的可操作時間戳記帳戶。 |

## Customer AI輸入資料 {#customer-ai-input-data}

對於輸入資料集(例如Adobe Analytics和Adobe Audience Manager)，依預設，各自的來源聯結器會在連線過程中直接對應這些標準欄位群組（商務、Web、應用程式和搜尋）中的事件。 下表顯示Customer AI預設標準欄位群組中的事件欄位。

如需對應Adobe Analytics資料或Audience Manager資料的詳細資訊，請造訪Analytics欄位對應或Audience Manager [欄位對應指南](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

對於未透過上述聯結器之一填入的輸入資料集，您可以使用體驗事件或消費者體驗事件XDM結構描述。 可在架構建立過程中新增其他XDM欄位群組。 欄位群組可以透過Adobe提供，例如標準欄位群組或自訂欄位群組，其符合Platform中的資料表示。

>[!IMPORTANT]
>
>您必須確保資料已填入這些輸入資料集。 如果在輸入資料集中找不到標準欄位群組中的事件，您必須在設定工作流程期間新增自訂事件。 請參閱自訂事件的詳細資料。

### Customer AI使用的標準欄位群組 {#standard-events}

體驗事件是用來判斷各種客戶行為。 視您的資料結構而定，下列事件型別可能不會涵蓋客戶的所有行為。 您可以自行決定哪些欄位具備必要資料，可清楚且明確地識別Web或其他通道專屬的使用者活動。 視您的預測目標而定，所需的必填欄位可能會變更。

>[!NOTE]
>
>如果您使用Adobe Analytics或Adobe Audience Manager資料，系統會自動建立結構描述，並包含擷取資料所需的標準事件。 如果您要建立自己的自訂EE結構描述來擷取資料，則需要考慮擷取資料所需的欄位群組。

Customer AI預設會使用這四個標準欄位群組中的事件：商務、網頁、應用程式和搜尋。 下列標準欄位群組中不需要每個事件的資料，但在某些情況下需要特定事件。 如果您的標準欄位群組中有任何可用事件，建議將其納入結構描述中。 例如，如果您想建立用於預測購買事件的Customer AI模型，擁有來自Commerce和網頁詳細資料欄位群組的資料會很有用。

若要在Platform UI中檢視欄位群組，請選取 **[!UICONTROL 結構描述]** 標籤並選取「 」 **[!UICONTROL 欄位群組]** 標籤。

| 字段组 | 事件型別 | xdm欄位路徑 |
| --- | --- | --- |
| [!UICONTROL 商務詳細資料] | 订单 | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | productListView | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | 結帳 | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
|  | 購買 | <li> `commerce.purchases.value` </li> <li> `productListItems.SKU` </li> |
|  | productListRemovals | <li> `commerce.productListRemovals.value` </li> <li> `productListItems.SKU` </li> |
|  | productListOpens | <li> `commerce.productListOpens.value` </li> <li> `productListItems.SKU` </li> |
|  | 產品檢視 | <li> `commerce.productViews.value` </li> <li> `productListItems.SKU` </li> |
| [!UICONTROL 網頁詳細資訊] | webVisit | `web.webPageDetails.name` |
|  | webInteraction | `web.webInteraction.linkClicks.value` |
| [!UICONTROL 應用程式詳細資料] | applicationClose | <li> `application.applicationCloses.value` </li> <li> `application.name` </li> |
|  | applicationCrashes | <li> `application.crashes.value` </li> <li> `application.name` </li> |
|  | applicationFeatureUsages | <li> `application.featureUsages.value` </li> <li> `application.name` </li> |
|  | applicationFirstLaunches | <li> `application.firstLaunches.value` </li> <li> `application.name` </li> |
|  | applicationInstall | <li> application.installs.value </li> <li> `application.name` </li> |
|  | applicationLaunch | <li> application.launches.value </li> <li> `application.name` </li> |
|  | applicationUpgrade | <li> application.upgrades.value </li> <li> `application.name` </li> |
| [!UICONTROL 搜尋詳細資料] | 搜索 | `search.keywords` |

此外，Customer AI可以使用訂閱資料來建立更好的流失模型。 每個設定檔需要使用訂閱資料 [[!UICONTROL 訂閱]](../../xdm/data-types/subscription.md) 資料型別格式。 大部分欄位都是選用欄位，不過，若要取得最佳流失模型，強烈建議您為儘可能多的欄位提供資料，例如 `startDate`， `endDate`以及任何其他相關詳細資訊。 如需此功能的額外支援，請洽詢您的帳戶團隊。

### 新增自訂事件和設定檔屬性 {#add-custom-events}

如果您有想要在預設值之外包含的資訊 [標準事件欄位](#standard-events) 由Customer AI使用，您可以使用 [自訂事件設定](./user-guide/configure.md#custom-events) 以擴充模型使用的資料。

#### 自訂事件的使用時機

當在資料集選取步驟中選擇的資料集包含 *無* Customer AI使用的預設事件欄位中。 Customer AI需要結果以外的至少一個使用者行為事件的相關資訊。

自訂事件對以下方面很有幫助：

- 將領域知識或先前的專業知識整合到模型中。

- 改善預測模型品質。

- 獲得更多深入分析和詮釋。

自訂事件的最佳候選者是包含領域知識（可預測結果）的資料。 自訂事件的一些一般範例包括：

- 註冊帳戶

- 訂閱Newsletter

- 致電客戶服務

以下是業界特有的一些自訂事件範例：

| 行业 | 自定义事件 |
| --- | --- |
| 零售 | 店內交易<br>註冊俱樂部卡<br>剪裁行動優惠券。 |
| 娛樂 | 購買季節會籍 <br> 串流視訊。 |
| 招待 | 預約餐廳 <br> 購買熟客點數。 |
| 旅遊 | 新增已知的旅行者資訊購買里程。 |
| 通信 | 升級/降級/取消計畫。 |

自訂事件必須代表使用者啟動的動作才能加以選取。 例如，「電子郵件傳送」是由行銷人員而非使用者起始的動作，因此不應作為自訂事件使用。

### 历史数据

Customer AI需要歷史資料才能進行模型訓練。 資料在系統中存在的所需持續時間由兩個關鍵元素決定：結果視窗和適用母體。

根據預設，如果在應用程式設定期間未提供合格的母體定義，Customer AI會尋找過去45天內有活動的使用者。 此外，根據預測的目標定義，Customer AI需要至少500個符合條件和500個非符合條件的事件（總共1000個）。

下列範例示範如何使用簡單的公式，協助您判斷所需的最小資料量。 如果您的資料超過最低需求，您的模型可能會提供更精確的結果。 如果您的數量少於所需的最小數量，則模型會失敗，因為沒有足夠的資料進行模型訓練。

**公式**:

若要決定系統中現有資料的最短所需持續時間：

- 建立功能所需的最少資料為30天。 比較資格回顧期間與30天：

   - 如果資格回顧期間大於30天，資料需求=資格回顧期間+結果期間。

   - 否則，資料需求= 30天+結果視窗。

**如果定義適用母體的條件不只一個，則適用性回顧期間為最長。

>[!NOTE]
>
>30是合格母體所需的最小天數。 若未提供，預設值為45天。

**示例**:

- 您想要預測客戶在未來30天內是否可能為過去60天內有某些網路活動的客戶購買手錶。

   - 資格回顧期間= 60天

   - 結果期間= 30天

   - 所需資料= 60天+ 30天= 90天

- 您想要預測使用者在未來7天內是否可能購買手錶 **不含** 提供明確的合格母體。 在此情況下，符合資格的母體會預設為「過去45天內有活動的人」，而結果期間為7天。

   - 資格回顧期間= 45天

   - 結果期間= 7天

   - 所需資料= 45天+ 7天= 52天

- 您想要預測客戶在未來7天內是否可能為過去7天內進行一些網路活動的客戶購買手錶。

   - 資格回顧期間= 7天

   - 建立功能所需的最少資料= 30天

   - 結果期間= 7天

   - 所需資料= 30天+ 7天= 37天

雖然Customer AI要求資料在系統中存在的最短時間，但它也最適用於最近的資料。 透過使用較新的行為資料，Customer AI可能會對使用者的未來行為產生更準確的預測。

## Customer AI輸出資料 {#customer-ai-output-data}

Customer AI會針對視為符合資格的個別設定檔產生數個屬性。 根據您已布建的內容，有兩種方式可使用分數（輸出）。 如果您有已啟用即時客戶設定檔的資料集，您可以取用來自即時客戶設定檔的深入分析： [區段產生器](../../segmentation/ui/segment-builder.md). 如果您沒有啟用設定檔的資料集，您可以 [下載Customer AI輸出](./user-guide/download-scores.md) 資料湖上可用的資料集。

您可以在Platform中找到輸出資料集 **資料集** 工作區。 所有Customer AI輸出資料集都以名稱開頭 **Customer AI分數 — NAME_OF_APP**. 同樣地，所有Customer AI輸出結構描述都以名稱開頭 **Customer AI結構描述 — Name_of_app**.

![Customer AI中輸出資料集的名稱](./images/user-guide/cai-schema-name-of-app.png)

下表說明可在Customer AI輸出中找到的各種屬性：

| 属性 | 描述 |
| ----- | ----------- |
| [!UICONTROL 得分] | 客戶在定義的時間範圍內達成預測目標的相對可能性。 此值不應被視為機率百分比，而是個人相較於整體母體的可能性。 此分數介於0到100之間。 |
| 機率 | 此屬性是設定檔在定義的時間範圍內達到預測目標的真實機率。 比較不同目標的輸出時，建議考量超過百分位數或分數的機率。 在決定適用母體的平均機率時，應一律使用機率，因為機率對於不經常發生的事件往往位於較低端。 機率範圍在0到1之間的值。 |
| 百分位數 | 此值提供有關設定檔相對於其他類似評分的設定檔效能的資訊。 例如，百分位數排名為99的設定檔流失率顯示，相較於所有其他已評分設定檔的99%，該設定檔有較高的流失風險。 百分位數的範圍從1到100。 |
| 傾向性型別 | 選取的傾向性型別。 |
| 評分日期 | 評分發生的日期。 |
| 影響因素 | 這些是個人資料可能會轉換或流失的預測原因。 這些因素由下列屬性組成：<ul><li>程式碼：對設定檔的預測分數產生正面影響的設定檔或行為屬性。 </li><li>值：設定檔或行為屬性的值。</li><li>重要性：表示設定檔或行為屬性對預測分數（低、中、高）的權重</li></ul> |

## 后续步骤 {#next-steps}

準備資料並確保所有認證和結構描述都就緒後，請參閱 [設定Customer AI執行個體](./user-guide/configure.md) 指南，可引導您完成建立Customer AI執行個體的逐步教學課程。
---
keywords: Experience Platform；快速入門；Attribution ai；熱門主題；Attribution ai輸入；Attribution ai輸出；
feature: Attribution AI
title: Attribution AI的輸入和輸出
description: 以下檔案概述Attribution AI中使用的各種輸入和輸出。
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '2504'
ht-degree: 3%

---

# 輸入和輸出 [!DNL Attribution AI]

以下檔案概述中使用的不同輸入和輸出 [!DNL Attribution AI].

## [!DNL Attribution AI] 輸入資料

Attribution AI的運作方式是分析下列資料集以計算演演算法分數：

- Adobe Analytics資料集使用 [Analytics來源聯結器](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Experience Platform結構描述中的體驗事件(EE)資料集
- 消費者體驗事件(CEE)資料集

您現在可以根據以下專案從不同來源新增多個資料集 **身分對應** （欄位）表示每個資料集共用相同的身分型別（名稱空間），例如ECID。 選取身分和名稱空間後，會顯示「ID欄」完整度量度，指出要彙整的資料量。 若要進一步瞭解新增多個資料集，請造訪 [Attribution AI使用手冊](./user-guide.md#identity).

預設不會一律對應管道資訊。 在某些情況下，如果mediaChannel （欄位）空白，您將欄位對應到mediaChannel之後才能繼續，因為它是必要欄。 如果在資料集中偵測到頻道，則預設會將它對應到mediaChannel。 其他欄，例如 **媒體型別** 和 **媒體動作** 仍是選用專案。

對應管道欄位後，請繼續執行「定義事件」步驟，您可以在此選取轉換事件、接觸點事件，然後從個別資料集選擇特定欄位。

>[!IMPORTANT]
>
>Adobe Analytics來源聯結器最多可能需要四週的時間來回填資料。 如果您最近才設定聯結器，您應驗證資料集是否具備Attribution AI所需的最小資料長度。 請檢閱 [歷史資料](#data-requirements) 區段，驗證您是否有足夠的資料來計算精確的演演算法分數。

如需有關設定的詳細資訊 [!DNL Consumer Experience Event] (CEE)結構描述，請參閱 [Intelligent Services資料準備](../data-preparation.md) 指南。 如需對應Adobe Analytics資料的詳細資訊，請造訪 [Analytics欄位對映](../../sources/connectors/adobe-applications/analytics.md) 說明檔案。

並非所有的欄位都在 [!DNL Consumer Experience Event] (CEE)結構描述是Attribution AI的必要專案。

您可以使用在結構描述或選取的資料集中建議使用的任何欄位來設定接觸點。

| 建議的欄 | 需要 |
| --- | --- |
| 主要身分欄位 | 接觸點/轉換 |
| 时间戳 | 接觸點/轉換 |
| 渠道._类型 | 接觸點 |
| Channel.mediaAction | 接觸點 |
| Channel.mediaType | 接觸點 |
| Marketing.trackingCode | 接觸點 |
| Marketing.campaignname | 接觸點 |
| Marketing.campaigngroup | 接觸點 |
| Commerce | 转化 |

通常，歸因會針對轉換欄執行，例如「商務」底下的「訂單」、「購買」和「結帳」。 「管道」和「行銷」欄可用來定義Attribution AI的接觸點(例如， `channel._type = 'https://ns.adobe.com/xdm/channel-types/email'`)。 為獲得最佳結果和深入分析，強烈建議您儘可能加入轉換和接觸點欄。 此外，您並非僅限於上述欄。 您可以將任何其他建議或自訂欄加入為轉換或接觸點定義。

體驗事件(EE)資料集不需要明確擁有管道和行銷Mixin，只要與設定接觸點相關的管道或行銷活動資訊存在於Mixin或傳遞欄位之一中即可。

>[!TIP]
>
>如果您在CEE結構描述中使用Adobe Analytics資料，Analytics的接觸點資訊通常會儲存在 `channel.typeAtSource` (例如， `channel.typeAtSource = 'email'`)。

## 历史数据 {#data-requirements}

>[!IMPORTANT]
>
> Attribution AI運作所需的最小資料量如下：
> - 您需要提供至少3個月（90天）的資料，才能執行良好的模型。
> - 您至少需要1000次轉換。


Attribution AI需要歷史資料作為模型訓練的輸入。 所需的資料持續時間主要取決於兩個關鍵因素：訓練時段和回顧時段。 較短的訓練時段輸入對最近的趨勢更敏感，而較長的訓練時段有助於產生更穩定和準確的模型。 請務必使用最能代表您業務目標的歷史資料來模型化目標。

此 [訓練時段設定](./user-guide.md#training-window) 根據發生時間篩選轉換事件，並將其設定為用於模型訓練。 目前，最低訓練時段為1季（90天）。 此 [回顧期間](./user-guide.md#lookback-window) 提供一個時間範圍，指出應納入與此轉換事件相關的轉換事件接觸點之前天數。 這兩個概念共同決定應用程式所需的輸入資料量（以天為單位測量）。

根據預設，Attribution AI會將訓練時段定義為最近2季（6個月），並將回顧時段定義為56天。 換言之，此模型會考慮過去2個季度發生的所有已定義轉換事件，並尋找在相關轉換事件前56天內發生的所有接觸點。

**公式**:

所需的最小資料長度=訓練時段+回顧時段

>[!TIP]
>
> 具有預設設定的應用程式所需的最小資料長度為：2季（180天） + 56天= 236天。

示例：

- 您想要將過去90天（3個月）內發生的轉換事件歸因，並追蹤轉換事件之前4週內發生的所有接觸點。 輸入資料持續時間應跨越過去90天+ 28天（4週）。 訓練期間為90天，回顧期間為28天，總共118天。

## Attribution AI輸出資料

Attribution AI會輸出下列內容：

- [原始精細分數](#raw-granular-scores)
- [彙總分數](#aggregated-attribution-scores)

**範例輸出結構描述：**

![](./images/input-output/schema_output.gif)

### 原始精細分數 {#raw-granular-scores}

Attribution AI會儘可能以最精細的層級輸出歸因分數，因此您可以依任何分數欄來分割分數。 若要在UI中檢視這些分數，請閱讀以下章節： [檢視原始分數路徑](#raw-score-path). 若要使用API下載分數，請造訪 [在Attribution AI中下載分數](./download-scores.md) 檔案。

>[!NOTE]
>
> 只有符合下列任一條件時，您才能從分數輸出資料集的輸入資料集中看到任何所需的報表欄：
> - 報告欄包含在設定頁面中，作為接觸點或轉換定義設定的一部分。
> - 報告欄包含在其他分數資料集欄中。


下表概述原始分數範例輸出中的結構描述欄位：

| 欄名稱（資料型別） | 可為空 | 描述 |
| --- | --- | --- |
| timestamp (DateTime) | False | 轉換事件或觀察發生的時間。 <br> **範例：** 2020-06-09T00:01:51.000盎司 |
| identityMap （對應） | True | 與CEE XDM格式類似的使用者的identityMap。 |
| eventType （字串） | True | 此時間序列記錄的主要事件型別。 <br> **範例：** &quot;Order&quot;、&quot;Purchase&quot;、&quot;Visit&quot; |
| eventMergeId （字串） | True | 要關聯或合併多個ID [!DNL Experience Events] 基本上是相同事件或應該合併的資料放在一起。 這是為了在擷取之前由資料製作者填入。 <br> **範例：** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id （字串） | False | 時間序列事件的唯一識別碼。 <br> **範例：** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId （物件） | False | 與您的租使用者ID對應的頂層物件容器。 <br> **範例：** _atsdsnrmsv2 |
| your_schema_name （物件） | False | 使用轉換事件對列進行評分，所有與其關聯的接觸點事件及其中繼資料。 <br> **範例：** Attribution AI分數 — 模型名稱__2020 |
| 分段（字串） | True | 轉換區段，例如建立模型時所依據的地理細分。 如果缺少區段，區段會與conversionName相同。 <br> **範例：** ORDER_US |
| conversionName （字串） | True | 設定期間設定的轉換名稱。 <br> **範例：** 訂購、銷售機會、瀏覽 |
| 轉換（物件） | False | 轉換中繼資料欄。 |
| dataSource （字串） | True | 資料來源的全域唯一識別碼。 <br> **範例：** Adobe Analytics |
| eventSource （字串） | True | 實際事件發生時的來源。 <br> **範例：** Adobe.com |
| eventType （字串） | True | 此時間序列記錄的主要事件型別。 <br> **範例：** 訂購 |
| 地理（字串） | True | 轉換傳遞的地理位置 `placeContext.geo.countryCode`. <br> **範例：** US |
| priceTotal （兩次） | True | 透過轉換獲得的收入 <br> **範例：** 99.9 |
| product （字串） | True | 產品本身的XDM識別碼。 <br> **範例：** RX 1080 ti |
| productType （字串） | True | 針對此產品檢視向使用者展示的產品顯示名稱。 <br> **範例：** Gpu |
| 數量（整數） | True | 轉換期間購買的數量。 <br> **範例：** 1 1080英吋 |
| receivedTimestamp (DateTime) | True | 已收到轉換的時間戳記。 <br> **範例：** 2020-06-09T00:01:51.000盎司 |
| skuId （字串） | True | 庫存單位(SKU)，供應商所定義之產品的唯一識別碼。 <br> **範例：** MJ-03-XS-Black |
| timestamp (DateTime) | True | 轉換的時間戳記。 <br> **範例：** 2020-06-09T00:01:51.000盎司 |
| passThrough （物件） | True | 使用者在設定模型時指定的其他分數資料集欄。 |
| commerce_order_purchaseCity （字串） | True | 其他分數資料集欄。 <br> **範例：** 城市：聖荷西 |
| customerProfile （物件） | False | 用來建立模型的使用者身分詳細資訊。 |
| identity （物件） | False | 包含用於建立模型的使用者的詳細資訊，例如 `id` 和 `namespace`. |
| id （字串） | True | 使用者的身分ID，例如Cookie ID、Adobe Analytics ID (AAID)或Experience CloudID （ECID，也稱為MCID或訪客ID）等。 <br> **範例：** 17348762725408656344688320891369597404 |
| 名稱空間（字串） | True | 用來建置路徑進而建置模型的身分名稱空間。 <br> **範例：** aaid |
| touchpointsDetail （物件陣列） | True | 導致轉換的接觸點詳細資訊清單，排序依據： | 接觸點發生次數或時間戳記。 |
| 接觸點名稱（字串） | True | 設定期間設定的接觸點名稱。 <br> **範例：** PAID_SEARCH_CLICK |
| 分數（物件） | True | 以此分數表示的接觸點對此轉換的貢獻。 如需此物件所產生之分數的詳細資訊，請參閱 [彙總歸因分數](#aggregated-attribution-scores) 區段。 |
| 接觸點（物件） | True | 接觸點中繼資料。 如需此物件所產生之分數的詳細資訊，請參閱 [彙總分數](#aggregated-scores) 區段。 |

### 檢視原始分數路徑(UI) {#raw-score-path}

您可以在UI中檢視原始分數的路徑。 從選取開始 **[!UICONTROL 結構描述]** 在Platform UI中，然後在中搜尋並選取您的Attribution AI分數結構 **[!UICONTROL 瀏覽]** 標籤。

![選擇您的結構描述](./images/input-output/schemas_browse.png)

接下來，選取 **[!UICONTROL 結構]** UI的視窗， **[!UICONTROL 欄位屬性]** 標籤開啟。 範圍 **[!UICONTROL 欄位屬性]** 是對映至原始分數的路徑欄位。

![挑選結構描述](./images/input-output/field_properties.png)

### 彙總歸因分數 {#aggregated-attribution-scores}

如果日期範圍少於30天，可以從Platform UI以CSV格式下載彙總分數。

Attribution AI支援兩種類別的歸因分數：演演算法分數和規則型分數。

Attribution AI會產生兩種不同型別的演演算法分數：累加分數和受影響的分數。 受影響的分數是每個行銷接觸點負責的轉換比例。 累加分數是行銷接觸點直接造成的邊緣影響量。 累加分數和受影響的分數之間的主要差異在於，累加分數會將基線影響納入考量。 它不會假設轉換完全是由先前的行銷接觸點所造成。

以下快速檢視Adobe Experience Platform UI中的Attribution AI結構描述輸出範例：

![](./images/input-output/schema_screenshot.png)

請參閱下表，瞭解這些歸因分數的詳細資訊：

| 歸因分數 | 描述 |
| ----- | ----------- |
| 受影響的（演演算法） | 受影響的分數是每個行銷接觸點負責的轉換比例。 |
| 增量（演演算法） | 累加分數是行銷接觸點直接造成的邊緣影響量。 |
| 首次接触 | 規則型歸因分數，可將所有點數指派給轉換路徑上的初始接觸點。 |
| 最后接触 | 規則型歸因分數，可將所有點數指派給最接近轉換的接觸點。 |
| 线性 | 規則型歸因分數，可將相等點數指派給轉換路徑上的每個接觸點。 |
| U 型 | 規則型歸因分數會將40%的點數指派給第一個接觸點，再將40%的點數指派給最後一個接觸點，其他接觸點則平分剩餘的20%。 |
| 时间衰减 | 規則型歸因分數，其中離轉換較近的接觸點所獲得的點數多於時間上離轉換較遠的接觸點。 |

**原始分數參考（歸因分數）**

下表將歸因分數對應至原始分數。 如果您想下載原始分數，請造訪 [在Attribution AI中下載分數](./download-scores.md) 說明檔案。

| 歸因分數 | 原始分數參考欄 |
| --- | --- |
| 受影響的（演演算法） | _tenantID.your_schema_name.element.touchpoint.algorithmicInffected |
| 增量（演演算法） | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmicInffected |
| 首次接触 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| 最后接触 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| 线性 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| U 型 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.uShape |
| 时间衰减 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### 彙總分數 {#aggregated-scores}

如果日期範圍少於30天，可以從Platform UI以CSV格式下載彙總分數。 如需這些彙總資料欄的詳細資訊，請參閱下表。

| 欄名稱 | 限制 | 可為空 | 描述 |
| --- | --- | --- | --- |
| customerevents_date (DateTime) | 使用者定義與固定格式 | False | YYYY-MM-DD格式的客戶事件日期。 <br> **範例**：2016-05-02 |
| mediatouchpoints_date (DateTime) | 使用者定義與固定格式 | True | YYYY-MM-DD格式的媒體接觸點日期 <br> **範例**：2017-04-21 |
| 區段（字串） | 已計算 | False | 轉換區段，例如建立模型時所依據的地理細分。 如果沒有區段，則區段與conversion_scope相同。 <br> **範例**： ORDER_AMER |
| conversion_scope （字串） | 使用者定義 | False | 使用者設定的轉換名稱。 <br> **範例**：訂購 |
| touchpoint_scope （字串） | 使用者定義 | True | 使用者設定的接觸點名稱 <br> **範例**： PAID_SEARCH_CLICK |
| product （字串） | 使用者定義 | True | 產品的XDM識別碼。 <br> **範例**：CC |
| product_type （字串） | 使用者定義 | True | 針對此產品檢視向使用者展示的產品顯示名稱。 <br> **範例**：gpu，筆記型電腦 |
| 地理（字串） | 使用者定義 | True | 轉換發生的地理位置(placeContext.geo.countryCode) <br> **範例**：US |
| event_type （字串） | 使用者定義 | True | 此時間序列記錄的主要事件型別 <br> **範例**：付費轉換 |
| media_type （字串） | 列舉 | False | 說明媒體型別是付費、擁有還是贏得。 <br> **範例**：付費，擁有 |
| channel （字串） | 列舉 | False | 此 `channel._type` 屬性，用來提供具有類似屬性的管道的粗略分類。 [!DNL Consumer Experience Event] XDM. <br> **範例**：搜尋 |
| 動作（字串） | 列舉 | False | 此 `mediaAction` 屬性是用來提供體驗事件媒體動作的型別。 <br> **範例**：按一下 |
| campaign_group （字串） | 使用者定義 | True | 促銷活動群組名稱，多個促銷活動會聚集在一起，例如「50%_DISCOUNT」。 <br> **範例**：商業 |
| campaign_name （字串） | 使用者定義 | True | 用於識別「50%_DISCOUNT_USA」或「50%_DISCOUNT_ASIA」等行銷活動的行銷活動名稱。 <br> **範例**：感恩節優惠 |

**原始分數參考（彙總）**

下表將彙總分數對應至原始分數。 如果您想下載原始分數，請造訪 [在Attribution AI中下載分數](./download-scores.md) 說明檔案。 若要從UI內檢視原始分數路徑，請造訪以下區段： [檢視原始分數路徑](#raw-score-path) 在此檔案中。

| 欄名稱 | 原始分數參考欄 |
| --- | --- |
| customerevents_date | timestamp |
| mediatouchpoints_date | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| segment（区段） | _tenantID.your_schema_name.segmentation |
| conversion_scope | _tenantID.your_schema_name.conversion.conversionName |
| touchpoint_scope | _tenantID.your_schema_name.touchpointsDetail.element.touchpointName |
| product | _tenantID.your_schema_name.conversion.product |
| product_type | _tenantID.your_schema_name.conversion.product_type |
| 地理 | _tenantID.your_schema_name.conversion.geo |
| event_type | 事件型別 |
| media_type | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| channel | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| 動作 | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| campaign_name | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |

>[!IMPORTANT]
>
> - Attribution AI僅會使用更新的資料進行進一步的訓練和評分。 同樣地，當您請求刪除資料時，Customer AI會限制使用已刪除的資料。
> - Attribution AI會利用Platform資料集。 為支援品牌可能收到的消費者權利請求，品牌應使用平台Privacy Service提交消費者存取和刪除請求，以透過Data Lake、Identity Service和即時客戶設定檔移除其資料。
> - 我們用於模型輸入/輸出的所有資料集都將遵循Platform准則。 平台資料加密適用於待用和傳輸中的資料。 請參閱檔案以深入瞭解 [資料加密](../../../help/landing/governance-privacy-security/encryption.md)


## 后续步骤 {#next-steps}

當您準備好資料及所有認證和結構描述後，請依照以下步驟開始 [Attribution AI使用手冊](./user-guide.md). 本指南會逐步引導您建立Attribution AI的執行個體。

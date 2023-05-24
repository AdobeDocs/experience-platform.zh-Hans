---
keywords: Experience Platform；啟動；疑難排解；護欄；指引；限制
title: 啟用資料的預設護欄
solution: Experience Platform
product: experience platform
type: Documentation
description: 進一步瞭解資料啟用預設使用量和速率限制。
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 7c1d956e3b6a1314baa13fef823d73d42404516a
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 1%

---

# 啟用資料的護欄

此頁面提供與啟用行為相關的預設使用量和速率限制。 檢閱下列護欄時，系統假設您已正確設定 [已連線至目的地](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* 大多數客戶不會超過這些預設限制。 如果您想瞭解自訂限制，請聯絡客戶服務代表。
>* 本檔案中概述的限制正在不斷改進。 請定期回來檢視更新。
>* 根據個別下游限制，某些目的地的護欄可能會比本頁面上記錄的護欄更嚴格。 也請務必檢查 [目錄](/help/destinations/catalog/overview.md) 您連線並啟用資料的目的地頁面。


## 限制型別 {#limit-types}

本檔案有兩種預設限制：

* **軟限制：** 可以超出軟限制，但軟限制提供系統效能的建議指引。
* **硬限制：** 硬限制提供絕對最大值。 Experience PlatformUI或API不允許您超出此限制，或如果您超出此限制會傳回錯誤。


## 啟用限制 {#activation-limits}

啟用目的地的即時客戶設定檔資料時，下列護欄會提供建議的限制。

### 一般啟動護欄 {#general-activation-guardrails}

以下護欄通常適用於透過啟動 [所有目的地型別](/help/destinations/destination-types.md#destination-types).

| 護欄 | 限制 | 限制型別 | 描述 |
| --- | --- | --- | --- |
| 單一目的地的最大區段數 | 250 | 柔和 | 建議將最多250個區段對應至資料流中的單一目的地。 <br><br> 如果您需要啟用一個目的地超過250個區段，您可以： <ul><li> 取消對應您不想再啟用的區段，或</li><li>建立新資料流到所需的目的地，並將區段對應到這個新資料流。</li></ul> <br> 請注意，在某些情況下，您對應至目的地的區段可能限制在250個以下。 這些目標會在頁面下方各自的區段中進一步說明。 |
| 目的地數量上限 | 100 | 柔和 | 建議最多建立100個目的地，供您連線並啟用資料至 *每個沙箱*. [Edge個人化目的地（自訂個人化）](#edge-destinations-activation) 在100個建議目的地中，最多可組成10個。 |
| 對應至目的地的屬性數目上限 | 50 | 柔和 | 如果有多種目的地和目的地型別，您可以選取要對應的設定檔屬性和身分來匯出。 為獲得最佳效能，資料流中最多應將50個屬性對應至目的地。 |
| 啟用至目的地的資料型別 | 設定檔資料，包括身分和身分對應 | 硬 | 目前只能匯出 *設定檔記錄屬性* 至目的地。 描述事件資料的XDM屬性目前不支援匯出。 |
| 啟用至目的地的資料型別 — 陣列和對應屬性支援 | 不可用 | 硬 | 目前為 **not** 可匯出 *陣列或對應屬性* 至目的地。 此規則的例外情況是 [身分對應](/help/xdm/field-groups/profile/identitymap.md)，會在串流和檔案型啟用中匯出。 |

{style="table-layout:auto"}

### 串流啟用 {#streaming-activation}

以下護欄適用於透過啟動 [串流目的地](/help/destinations/ui/activate-segment-streaming-destinations.md).

| 護欄 | 限制 | 限制型別 | 描述 |
| --- | --- | --- | --- |
| 每秒的啟用數目（具有設定檔匯出內容的HTTP訊息） | 不适用 | - | 目前每秒從Experience Platform傳送至合作夥伴目的地API端點的訊息數量沒有限制。 <br> 任何限制或延遲都由Experience Platform傳送資料的端點指定。 也請務必檢查 [目錄](/help/destinations/catalog/overview.md) 您連線並啟用資料的目的地頁面。 |

{style="table-layout:auto"}

### 批次（檔案式）啟用 {#batch-file-based-activation}

以下護欄適用於透過啟動 [批次（以檔案為基礎）目的地](/help/destinations/ui/activate-batch-profile-destinations.md).

| 護欄 | 限制 | 限制型別 | 描述 |
| --- | --- | --- | --- |
| 啟用頻率 | 每3、6、8或12小時進行一次每日完整匯出或更頻繁的增量匯出。 | 硬 | 閱讀 [匯出完整檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) 和 [匯出增量檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) 檔案區段，以取得批次匯出頻率遞增的詳細資訊。 |
| 在指定小時內可匯出的區段數上限 | 100 | 柔和 | 建議最多新增100個區段至批次目的地資料流。 |
| 要啟用的每個檔案的最大列數（記錄） | 500萬 | 硬 | Adobe Experience Platform會自動將匯出的檔案分割為每個檔案500萬筆記錄（列）。 每一列代表一個設定檔。 分割檔案名稱會附加一個數字，指示檔案是較大匯出的一部分，例如： `filename.csv`， `filename_2.csv`， `filename_3.csv`. 如需詳細資訊，請閱讀 [排程區段](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 「啟用批次目的地」教學課程的內容。 |

{style="table-layout:auto"}

### 隨選啟用 {#ad-hoc-activation}

以下護欄適用於 [臨機啟動](/help/destinations/api/ad-hoc-activation-api.md) 方法。

| 護欄 | 限制 | 限制型別 | 描述 |
| --- | --- | --- | --- |
| 根據隨選啟用工作啟用的區段 | 80 | 硬 | 目前，每個隨選啟動工作最多可啟動80個區段。 嘗試為每個工作啟動超過80個區段會導致工作失敗。 未來版本可能會對此行為有所變更。 |
| 每個區段的同時臨機啟動工作 | 1 | 硬 | 每個區段請勿執行多個同時臨機啟動工作。 |

{style="table-layout:auto"}

### Edge個人化目的地啟用 {#edge-destinations-activation}

以下護欄適用於透過啟動 [邊緣個人化目的地](/help/destinations/destination-types.md#streaming-profile-export).

| 護欄 | 限制 | 限制型別 | 描述 |
| --- | --- | --- | --- |
| 最大數量 [自訂個人化](/help/destinations/catalog/personalization/custom-personalization.md) 目的地 | 10 | 柔和 | 您可以將資料流設定為每個沙箱10個自訂個人化目的地。 |
| 每個沙箱對應至個人化目的地的屬性數量上限 | 30 | 硬 | 每個沙箱在資料流中最多可以將30個屬性對應到個人化目的地。 |
| 對應至單一的最大區段數 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 目的地 | 50 | 柔和 | 您最多可以在至單一Adobe Target目的地的啟用流程中啟用50個區段。 |

{style="table-layout:auto"}

### Destination SDK護欄 {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) 是一套設定API，可讓您根據您選擇的資料和驗證格式，設定Experience Platform的目的地整合模式，以傳送對象和設定檔資料至您的端點。 以下護欄適用於您使用Destination SDK設定的目的地。

| 護欄 | 限制 | 限制型別 | 描述 |
| --- | --- | --- | --- |
| 最大數量 [私人自訂目的地](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | 柔和 | 您可以使用Destination SDK建立最多5個私人自訂串流或批次目的地。 如果您需要建立5個以上的這類目的地，請聯絡自訂服務代表。 |
| Destination SDK的設定檔匯出原則 | <ul><li>`maxBatchAgeInSecs` （最低1.800，最高3.600）</li><li>`maxNumEventsInBatch` （最小1.000，最大10.000）</li></ul> | 硬 | 使用時 [可設定的彙總](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 您目的地的選項，請留意決定HTTP訊息傳送至API型目的地頻率的最小和最大值，以及訊息應包含多少設定檔。 |

{style="table-layout:auto"}

### 目的地節流和重試原則 {#destination-throttling-and-retry-policy}

指定目的地的節流臨界值或限制的詳細資訊。 本節也提供有關目的地的重試原則的資訊。

| 目的地型別 | 描述 |
| --- | --- |
| 企業目的地(HTTP API、Amazon Kinesis、Azure EventHubs) | 在95%的時間中，Experience Platform會嘗試為成功傳送的訊息提供少於10分鐘的輸送量延遲，每個資料流到企業目的地的每秒要求速率少於10,000個要求。 <br> 如果對您的企業目的地的請求失敗，Experience Platform會儲存失敗的請求，並重試兩次，以將請求傳送至您的端點。 |

{style="table-layout:auto"}

## 其他Experience Platform服務的護欄 {#guardrails-other-services}

檢視其他Experience Platform服務的護欄資訊：

* 護欄 [資料擷取](/help/ingestion/guardrails.md)
* 護欄 [[!DNL Identity Service] 資料](/help/identity-service/guardrails.md)
* 護欄 [[!DNL Real-Time Customer Profile] 資料](/help/profile/guardrails.md)
* 護欄 [[!DNL Query Service] 資料](/help/query-service/guardrails.md)

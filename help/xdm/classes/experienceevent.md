---
keywords: Experience Platform；首頁；熱門主題；結構描述；結構描述；XDM；欄位；結構描述；結構描述；identityMap；身分對應；身分對應；結構描述設計；對應；事件模型；事件模型；最佳實務；事件；事件；
solution: Experience Platform
title: XDM ExperienceEvent類別
description: 本檔案提供XDM ExperienceEvent類別的概觀，以及事件資料模型化的最佳實務。
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: a3140d5216857ef41c885bbad8c69d91493b619d
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 1%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] 是一個標準Experience Data Model (XDM)類別，可讓您在發生特定事件或達到特定條件集時，建立系統的時間戳記快照。

體驗事件是所發生事件的事實記錄，包括時間點和所涉及個人的身分。 事件可以是明確的（直接可觀察的人類動作）或隱含的（在沒有直接人類動作的情況下引發），並且記錄時不會彙總或解釋。 如需有關在平台生態系統中使用此類別的詳細資訊，請參閱 [XDM概觀](../home.md#data-behaviors).

此 [!DNL XDM ExperienceEvent] 類別本身為結構描述提供幾個時間序列相關的欄位。 以下兩個欄位(`_id` 和 `timestamp`)為 **必填** 適用於以類別為基礎的所有結構描述，其餘則是選擇性的。 某些欄位的值會在擷取資料時自動填入。

![Platform UI中顯示的XDM ExperienceEvent結構](../images/classes/experienceevent/structure.png)

| 属性 | 描述 |
| --- | --- |
| `_id`<br>**(必需)** | 事件的唯一字串識別碼。 此欄位用於追蹤個別事件的唯一性、防止資料重複，以及在下游服務中查詢該事件。 某些情況下， `_id` 可以是 [通用唯一識別碼(UUID)](https://tools.ietf.org/html/rfc4122) 或 [全域唯一識別碼(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>如果您要從來源連線串流資料，或直接從Parquet檔案擷取資料，應串連特定欄位組合（例如主要ID、時間戳記、事件型別等）以產生此值。 串連值必須是 `uri-reference` 格式化字串，表示必須移除任何冒號字元。 之後，應該使用SHA-256或您選擇的其他演演算法來雜湊串連值。<br><br>請務必區分 **此欄位不代表與個人相關的身分**&#x200B;而是資料本身的記錄。 與個人相關的身分資料應委派至 [身分欄位](../schema/composition.md#identity) 由相容的欄位群組所提供。 |
| `eventMergeId` | 若使用 [Adobe Experience Platform Web SDK](../../edge/home.md) 若要內嵌資料，這代表導致建立記錄之內嵌批次的ID。 此欄位會在資料擷取時自動由系統填入。 不支援在Web SDK實作的內容之外使用此欄位。 |
| `eventType` | 指出事件型別或類別的字串。 如果您想要區分相同結構描述和資料集中的不同事件型別（例如區分零售公司的產品檢視事件和加入購物車的事件），則可以使用此欄位。<br><br>此屬性的標準值提供在 [附錄部分](#eventType)，包括預期使用案例的說明。 此欄位是可擴充的列舉，這表示您也可以使用自己的事件型別字串來分類您正在追蹤的事件。<br><br>`eventType` 限制您僅能針對應用程式的每個點選使用單一事件，因此您必須使用計算欄位，讓系統知道哪個事件最重要。 如需詳細資訊，請參閱以下章節： [計算欄位的最佳實務](#calculated). |
| `producedBy` | 描述事件製作者或來源的字串值。 如果需要，可使用此欄位來篩選掉某些事件產生者，以用於細分目的。<br><br>此屬性的部分建議值提供在 [附錄部分](#producedBy). 此欄位是可擴充的列舉，這表示您也可以使用自己的字串來代表不同的事件產生器。 |
| `identityMap` | 對應欄位，其中包含套用事件之個人的名稱空間身分識別集。 系統會在擷取身分資料時自動更新此欄位。 為了正確使用此欄位 [即時客戶個人檔案](../../profile/home.md)，請勿嘗試手動更新資料作業中的欄位內容。<br /><br />請參閱「 」中有關身分對應的章節 [結構描述組合基本概念](../schema/composition.md#identityMap) 以取得其使用案例的詳細資訊。 |
| `timestamp`<br>**(必需)** | 事件發生時間的ISO 8601時間戳記，格式如下 [RFC 3339第5.6節](https://tools.ietf.org/html/rfc3339#section-5.6). 此時間戳記必須發生在過去。 請參閱以下章節： [時間戳記](#timestamps) 以取得使用此欄位的最佳實務。 |

{style="table-layout:auto"}

## 事件模型化的最佳實務

以下小節涵蓋在Adobe Experience Platform中設計事件型Experience Data Model (XDM)結構描述的最佳實務。

### 時間戳記 {#timestamps}

根 `timestamp` 事件結構描述的欄位可以 **僅限** 代表觀察到的事件本身，且必須發生在過去。 如果您的細分使用案例需要使用未來可能發生的時間戳記，這些值必須限制在體驗事件結構描述中的其他位置。

例如，如果旅遊業及旅館業的企業正在模型化航班訂位事件，則類別層級 `timestamp` 欄位代表觀察到預訂事件的時間。 與事件相關的其他時間戳記（例如旅行預訂的開始日期）應擷取在標準或自訂欄位群組提供的單獨欄位中。

![反白顯示航班預訂和開始日期的體驗事件結構描述範例。](../images/classes/experienceevent/timestamps.png)

將類別層級的時間戳記與事件結構描述中的其他相關日期時間值分開，您就可以實作靈活的分段使用案例，同時保留體驗應用程式中客戶歷程的時間戳記帳戶。

### 使用計算欄位 {#calculated}

體驗應用程式中的某些互動可能會導致多個相關事件，在技術上會共用相同的事件時間戳記，因此可以呈現為單一事件記錄。 例如，如果客戶檢視您網站上的產品，這可能會導致事件記錄具有兩種可能性 `eventType` 值： 「產品檢視」事件(`commerce.productViews`)或一般「頁面檢視」事件(`web.webpagedetails.pageViews`)。 在這些情況下，您可以在單一點選中擷取多個事件時，使用計算欄位來擷取最重要的屬性。

[Adobe Experience Platform資料準備](../../data-prep/home.md) 可讓您對應、轉換及驗證XDM之間的資料。 使用可用的 [對應函式](../../data-prep/functions.md) 由服務提供，您可以叫用邏輯運運算元，以便在資料擷取至Experience Platform時，優先處理、轉換及/或合併多事件記錄中的資料。 在上述範例中，您可以指定 `eventType` 作為計算欄位，每當「產品檢視」和「頁面檢視」發生時，都會優先考慮「產品檢視」。

如果您是透過UI手動將資料擷取到Platform，請參閱以下指南： [計算欄位](../../data-prep/ui/mapping.md#calculated-fields) 有關如何建立計算欄位的特定步驟。

如果您使用來源連線將資料串流至Platform，您可以將來源設定為改用計算欄位。 請參閱 [您特定來源的檔案](../../sources/home.md) 瞭解如何在設定連線時實作計算欄位。

## 相容的結構描述欄位群組 {#field-groups}

>[!NOTE]
>
>數個欄位群組的名稱已變更。 檢視檔案： [欄位群組名稱更新](../field-groups/name-updates.md) 以取得詳細資訊。

Adobe提供數個標準欄位群組，可搭配使用 [!DNL XDM ExperienceEvent] 類別。 以下是類別的一些常用欄位群組清單：

* [[!UICONTROL Adobe Analytics ExperienceEvent完整擴充功能]](../field-groups/event/analytics-full-extension.md)
* [[!UICONTROL 餘額轉帳]](../field-groups/event/balance-transfers.md)
* [[!UICONTROL 行銷活動行銷細節]](../field-groups/event/campaign-marketing-details.md)
* [[!UICONTROL 卡片動作]](../field-groups/event/card-actions.md)
* [[!UICONTROL 管道詳細資料]](../field-groups/event/channel-details.md)
* [[!UICONTROL 商務詳細資料]](../field-groups/event/commerce-details.md)
* [[!UICONTROL 存款細節]](../field-groups/event/deposit-details.md)
* [[!UICONTROL 裝置折舊換新細節]](../field-groups/event/device-trade-in-details.md)
* [[!UICONTROL 餐飲預訂]](../field-groups/event/dining-reservation.md)
* [[!UICONTROL 一般使用者ID詳細資訊]](../field-groups/event/enduserids.md)
* [[!UICONTROL 环境详细信息]](../field-groups/event/environment-details.md)
* [[!UICONTROL 航班預訂]](../field-groups/event/flight-reservation.md)
* [[!UICONTROL IAB TCF 2.0同意]](../field-groups/event/iab.md)
* [[!UICONTROL 住宿預訂]](../field-groups/event/lodging-reservation.md)
* [[!UICONTROL 報價請求細節]](../field-groups/event/quote-request-details.md)
* [[!UICONTROL 預訂詳細資料]](../field-groups/event/reservation-details.md)
* [[!UICONTROL 網頁詳細資訊]](../field-groups/event/web-details.md)

## 附录

以下小節包含更多關於 [!UICONTROL XDM ExperienceEvent] 類別。

### 接受的值 `eventType` {#eventType}

下表概述下列專案的可接受值 `eventType`，以及其定義：

| 值 | 定义 |
| --- | --- |
| `advertising.clicks` | 廣告上的點按動作。 |
| `advertising.completes` | 定時媒體資產已觀看至完成。 這並不一定表示檢視者看完整段影片，因為檢視者可能略過前面。 |
| `advertising.conversions` | 客戶所執行的預先定義動作，會觸發效能評估事件。 |
| `advertising.federated` | 顯示是否透過資料同盟（客戶之間資料共用）建立體驗事件。 |
| `advertising.firstQuartiles` | 數位影片廣告已使用正常速度播放其長度的25%。 |
| `advertising.impressions` | 可能被檢視的客戶對廣告的閱聽。 |
| `advertising.midpoints` | 數位影片廣告已使用正常速度播放其長度的50%。 |
| `advertising.starts` | 數位影片廣告已開始播放。 |
| `advertising.thirdQuartiles` | 數位影片廣告已使用正常速度播放其長度的75%。 |
| `advertising.timePlayed` | 說明使用者在特定的定時媒體資產上所花費的時間。 |
| `application.close` | 應用程式已關閉或傳送到背景。 |
| `application.launch` | 應用程式已啟動或進入前景。 |
| `commerce.checkouts` | 產品清單發生結帳事件。 如果結帳程式中有多個步驟，就可能有一個以上的結帳事件。 如果有多個步驟，則會使用每個事件的時間戳記和參考頁面/體驗來識別每個個別事件（步驟），並依序表示。 |
| `commerce.productListAdds` | 產品已新增至產品清單或購物車。 |
| `commerce.productListOpens` | 新產品清單（購物車）已初始化或建立。 |
| `commerce.productListRemovals` | 一或多個產品專案已從產品清單或購物車中移除。 |
| `commerce.productListReopens` | 客戶已重新啟用無法再存取（已捨棄）的產品清單（購物車），例如透過重新行銷活動。 |
| `commerce.productListViews` | 產品清單或購物車已收到一個或多個檢視。 |
| `commerce.productViews` | 產品已收到一或多個檢視。 |
| `commerce.purchases` | 已接受訂單。 這是商務轉換中唯一需要的動作。 購買事件必須有參考的產品清單。 |
| `commerce.saveForLaters` | 已儲存產品清單以供日後使用，例如產品願望清單。 |
| `decisioning.propositionDisplay` | 決策主張已顯示給個人。 |
| `decisioning.propositionInteract` | 與決策主張互動的人。 |
| `delivery.feedback` | 傳送的意見回饋事件，例如電子郵件傳送。 |
| `directMarketing.emailBounced` | 傳送給個人的電子郵件已跳出。 |
| `directMarketing.emailBouncedSoft` | 傳送給個人的電子郵件已軟退回。 |
| `directMarketing.emailClicked` | 有人點按了行銷電子郵件中的連結。 |
| `directMarketing.emailDelivered` | 電子郵件已成功傳遞至個人的電子郵件服務 |
| `directMarketing.emailOpened` | 有人已開啟行銷電子郵件。 |
| `directMarketing.emailUnsubscribed` | 個人已取消訂閱行銷電子郵件。 |
| `inappmessageTracking.dismiss` | 已解除應用程式內訊息。 |
| `inappmessageTracking.display` | 已顯示應用程式內訊息。 |
| `inappmessageTracking.interact` | 已互動應用程式內訊息。 |
| `leadOperation.callWebhook` | 已呼叫webhook以回應銷售機會。 |
| `leadOperation.convertLead` | 潛在客戶已轉換。 |
| `leadOperation.interestingMoment` | 為個人錄製了一個有趣的時刻。 |
| `leadOperation.newLead` | 已建立潛在客戶。 |
| `leadOperation.scoreChanged` | 潛在客戶評分屬性的值已變更。 |
| `leadOperation.statusInCampaignProgressionChanged` | 促銷活動中的潛在客戶狀態已變更。 |
| `listOperation.addToList` | 已將個人新增至行銷清單。 |
| `listOperation.removeFromList` | 已將個人從行銷清單中移除。 |
| `message.feedback` | 針對傳送給客戶的訊息，提供意見回饋事件，例如已傳送/退回/錯誤。 |
| `message.tracking` | 追蹤事件，例如傳送給客戶的訊息上的開啟/點選/自訂動作。 |
| `opportunityEvent.addToOpportunity` | 已將個人新增至商機。 |
| `opportunityEvent.opportunityUpdated` | 機會已更新。 |
| `opportunityEvent.removeFromOpportunity` | 已將個人從機會中移除。 |
| `pushTracking.applicationOpened` | 有人從推播通知開啟應用程式。 |
| `pushTracking.customAction` | 有人點按了推播通知中的自訂動作。 |
| `web.formFilledOut` | 有人在wep頁面上填寫表單。 |
| `web.webinteraction.linkClicks` | 已選取連結一或多次。 |
| `web.webpagedetails.pageViews` | 網頁已收到一或多個檢視。 |

{style="table-layout:auto"}

### 建議值 `producedBy` {#producedBy}

下表概述一些接受的值 `producedBy`：

| 值 | 定义 |
| --- | --- |
| `self` | 自我 |
| `system` | 系统 |
| `salesRef` | 銷售代表 |
| `customerRep` | 客戶代表 |

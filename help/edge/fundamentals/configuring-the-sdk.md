---
title: 設定Adobe Experience Platform Web SDK
description: 瞭解如何設定Adobe Experience Platform Web SDK。
seo-description: Learn how to configure the Experience Platform Web SDK
keywords: 設定；設定；SDK；Edge；Web SDK；設定；edgeConfigId；上下文；Web；裝置；環境；placeContext；debugEnabled；edgeDomain；orgId；clickCollectionEnabled；onBeforeEventSend；defaultConsent；Web sdk設定；prehidingStyle；不透明度；cookieDestinationsEnabled；urlDestinationsEnabled；idMigrationEnabled；therPartyCookiesEnabled；
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
source-git-commit: a192a746fa227b658fcdb8caa07ea6fb4ac1a944
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 9%

---

# 設定Platform Web SDK

SDK的設定已完成 `configure` 命令。

>[!IMPORTANT]
>
>`configure` 是 *一律* 第一個命令稱為。

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

設定期間可設定許多選項。 所有選項都可在下方找到，並按類別分組。

## 一般選項

### `edgeConfigId`

>[!NOTE]
>
>**Edge Configurations已重新命名為Datastreams。 資料串流ID與設定ID相同。**

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 字符串 | 是 | None |

{style="table-layout:auto"}

您指派的設定ID，可將SDK連結至適當的帳戶和設定。 在單一頁面中設定多個執行個體時，您必須設定不同的 `edgeConfigId` 每個執行個體使用。

### `context` {#context}

| **类型** | 必需 | **默认值** |
| ---------------- | ------------ | -------------------------------------------------- |
| 字串陣列 | 否 | `["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]` |

{style="table-layout:auto"}

指示要自動收集哪些內容類別，如中所述 [自動資訊](../data-collection/automatic-information.md). 如果未指定此設定，預設會使用所有類別。

>[!IMPORTANT]
>
>所有內容屬性，但不包括 `highEntropyUserAgentHints`，預設為啟用。 如果您在Web SDK設定中手動指定內容屬性，則必須啟用所有內容屬性，才能繼續收集所需的資訊。

若要啟用 [高平均資訊量使用者端提示](user-agent-client-hints.md#enabling-high-entropy-client-hints) 在您的Web SDK部署中，您必須包含其他 `highEntropyUserAgentHints` 上下文選項，以及您現有的設定。

例如，若要從Web屬性擷取高平均資訊量使用者端提示，您的設定將如下所示：

`context: ["highEntropyUserAgentHints", "web"]`


### `debugEnabled`

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `false` |

{style="table-layout:auto"}

指出是否已啟用偵錯。 將此設定設為 `true` 啟用下列功能：

| **功能** | **函数** |
| ---------------------- | ------------------ |
| 主控台記錄 | 啟用在瀏覽器的JavaScript主控台中顯示的偵錯訊息 |

{style="table-layout:auto"}

### `edgeDomain` {#edge-domain}

將您的第一方網域填入此欄位。 如需詳細資訊，請參閱 [檔案](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=zh-Hans).

網域類似於 `data.{customerdomain.com}` ，網址為www。{customerdomain.com}。

### `edgeBasePath` {#edge-base-path}

用來與Adobe服務通訊和互動的edgeDomain之後的路徑。  通常這只有在未使用預設生產環境時才會變更。

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 字符串 | 否 | ee |

{style="table-layout:auto"}

### `orgId`

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 字符串 | 是 | None |

{style="table-layout:auto"}

您指派的 [!DNL Experience Cloud] 組織ID。 在一個頁面中設定多個執行個體時，您必須設定不同的 `orgId` 每個執行個體使用。

## 資料彙集

### `clickCollectionEnabled` {#clickCollectionEnabled}

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style="table-layout:auto"}

指出是否自動收集與連結點選相關聯的資料。 另請參閱 [自動連結追蹤](../data-collection/track-links.md#automaticLinkTracking) 以取得詳細資訊。 如果連結包含下載屬性或結尾為副檔名的連結，也會標示為下載連結。 可使用規則運算式來設定下載連結限定詞。 默认值为 `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 函数 | 否 | () =>未定義 |

{style="table-layout:auto"}

設定在傳送前為每個事件呼叫的回呼。 具有欄位的物件 `xdm` 會傳送至回呼。 若要變更傳送的內容，請修改 `xdm` 物件。 在回呼內， `xdm` 物件已在事件命令中傳遞資料，且已自動收集資訊。 如需此回撥時間與範例的詳細資訊，請參閱 [全域修改事件](tracking-events.md#modifying-events-globally).

### `onBeforeLinkClickSend` {#onBeforeLinkClickSend}

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 函数 | 否 | () =>未定義 |

{style="table-layout:auto"}

設定在傳送前為每個連結點選追蹤事件呼叫的回呼。 callback傳送的物件具有 `xdm`， `clickedElement`、和 `data` 欄位。

使用DOM元素結構來篩選連結追蹤時，您可以使用 `clickElement` 命令。 `clickedElement` 是已點按且已封裝上層節點樹狀結構的DOM元素節點。

若要變更要傳送的資料，請修改 `xdm` 和/或 `data` 物件。 在回呼內， `xdm` 物件已在事件命令中傳遞資料，且已自動收集資訊。

* 任何以外的值 `false` 將允許處理事件並傳送回呼。
* 如果回呼傳回 `false` 值、事件處理已停止（沒有錯誤），且事件未傳送。 此機制可讓您透過檢查事件資料並傳回 `false` 是否不應傳送事件。
* 如果callback擲回例外狀況，則事件的處理會停止，且不會傳送事件。


## 隱私權選項

### `defaultConsent` {#default-consent}

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 对象 | 否 | `"in"` |

{style="table-layout:auto"}

設定使用者的預設同意。 若尚未儲存使用者的同意偏好設定，請使用此設定。 其他有效值為 `"pending"` 和 `"out"`. 此預設值不會持續存在於使用者的設定檔中。 使用者的設定檔只有在以下情況下才會更新 `setConsent` 稱為。
* `"in"`：若此設定已設定或未提供值，則工作無需使用者同意偏好設定即可進行。
* `"pending"`：設定此設定時，工作會排入佇列，直到使用者提供同意偏好設定為止。
* `"out"`：設定此設定時，會捨棄工作，直到使用者提供同意偏好設定為止。
提供使用者的偏好設定後，工作會根據使用者的偏好設定進行或中止。 另請參閱 [支援同意](../consent/supporting-consent.md) 以取得詳細資訊。

## 個人化選項 {#personalization}

### `prehidingStyle` {#prehidingStyle}

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 字符串 | 否 | None |

{style="table-layout:auto"}

用來建立CSS樣式定義，在從伺服器載入個人化內容時隱藏網頁的內容區域。 如果未提供此選項，SDK在載入個人化內容時不會嘗試隱藏任何內容區域，這可能會導致「閃爍」。

例如，如果網頁上的某個元素的ID為 `container`，在從伺服器載入個人化內容時，您要隱藏其預設內容，請使用下列預先隱藏樣式：

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

### `targetMigrationEnabled` {#targetMigrationEnabled}

從移轉個別頁面時，應使用此選項 [!DNL at.js] 至Web SDK。

使用此選項可讓Web SDK讀取和寫入舊版 `mbox` 和 `mboxEdgeCluster` 使用的Cookie [!DNL at.js]. 這可協助您在從使用Web SDK的頁面移至使用 [!DNL at.js] 資料庫或反之。

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `false` |

## 對象選項

### `cookieDestinationsEnabled`

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style="table-layout:auto"}

啟用 [!DNL Audience Manager] Cookie目的地，可讓您根據區段資格來設定Cookie。

### `urlDestinationsEnabled`

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style="table-layout:auto"}

啟用 [!DNL Audience Manager] URL目的地，可讓您根據區段資格引發URL。

## 身分選項

### `idMigrationEnabled` {#id-migration-enabled}

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style="table-layout:auto"}

如果為true，SDK會讀取及設定舊的AMCV Cookie。 當網站某些部分仍可能使用Visitor.js時，此選項可協助您轉換至使用Adobe Experience Platform Web SDK。

如果頁面上定義了訪客API，SDK會查詢訪客API以取得ECID。 此選項可讓您使用Adobe Experience Platform Web SDK來雙標籤頁面，並且仍然擁有相同的ECID。

### `thirdPartyCookiesEnabled`

| 类型 | 必需 | 默认值 |
| -------- | ------------ | ----------------- |
| 布尔值 | 否 | `true` |

{style="table-layout:auto"}

啟用設定Adobe第三方Cookie。 SDK可在協力廠商內容中儲存訪客ID，以便跨網站使用相同的訪客ID。 如果您有多個網站或想與合作夥伴共用資料，請使用此選項；不過，有時基於隱私權原因並不需要此選項。

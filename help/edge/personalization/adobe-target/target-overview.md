---
title: 搭配Platform Web SDK使用Adobe Target
description: 瞭解如何使用Adobe Target以Experience Platform Web SDK呈現個人化內容
keywords: target；adobe target；activity.id；experience.id；renderDecisions；decisionScopes；預先隱藏程式碼片段；vec；表單式體驗撰寫器；xdm；對象；決定；範圍；結構；系統圖表；圖表
exl-id: 021171ab-0490-4b27-b350-c37d2a569245
source-git-commit: 5a048505be139b58dbb3bf85120df5e3cc46881e
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 6%

---

# 使用 [!DNL Adobe Target] 使用 [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] 可以傳遞和轉譯受管理的個人化體驗 [!DNL Adobe Target] 至網路頻道。 您可以使用WYSIWYG編輯器，稱為 [視覺化體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC)或非視覺化介面， [表單式體驗撰寫器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)，以建立、啟用及傳遞您的活動和個人化體驗。

>[!IMPORTANT]
>
>瞭解如何透過將您的Target實作移轉至Platform Web SDK [將Target從at.js 2.x移轉至Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html) 教學課程。
>
>瞭解如何使用第一次實作Target [使用Web SDK實作Adobe Experience Cloud](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hans) 教學課程。 如需Target的特定資訊，請參閱教學課程中標題為 [使用Platform Web SDK設定Target](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).


下列功能已經過測試，目前支援 [!DNL Target]：

* [A/B測試](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [A4T曝光和轉換報告](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)
* [Automated Personalization活動](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [體驗鎖定目標活動](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [多變數測試(MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)
* [Recommendations 活动](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html)
* [原生目標曝光和轉換報告](https://experienceleague.adobe.com/docs/target/using/reports/reports.html)
* [VEC支援](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)

## [!DNL Platform Web SDK] 系統圖表

下圖可協助您瞭解 [!DNL Target] 和 [!DNL Platform Web SDK] 邊緣決策。

![使用Platform Web SDK的Adobe Target邊緣決策圖表](./assets/target-platform-web-sdk.png)

| 调用 | 详细信息 |
| --- | --- |
| 1 | 裝置載入 [!DNL Platform Web SDK]. 此 [!DNL Platform Web SDK] 會傳送要求至Edge網路，要求中包含XDM資料、資料串流環境ID、傳入引數和客戶ID （選用）。 頁面（或容器）已預先隱藏。 |
| 2 | Edge Network會傳送要求給Edge Services，以使用訪客ID、同意和其他訪客內容資訊（例如地理位置和方便使用的裝置名稱）來擴充要求。 |
| 3 | 邊緣網路會將擴充的個人化請求傳送至 [!DNL Target] 邊緣包含訪客ID和傳入的引數。 |
| 4 | 個人資料指令碼執行，然後注入到 [!DNL Target] 設定檔儲存。 設定檔儲存體會從擷取區段 [!UICONTROL 對象庫] (例如，從以下專案共用的區段： [!DNL Adobe Analytics]， [!DNL Adobe Audience Manager]，則 [!DNL Adobe Experience Platform])。 |
| 5 | 根據URL要求引數和設定檔資料， [!DNL Target] 決定要針對目前頁面檢視和未來預先擷取的檢視，為訪客顯示哪些活動和體驗。 [!DNL Target] 然後將此資料傳回邊緣網路。 |
| 6 | a. Edge Network會將個人化回應傳送回頁面，選擇性地包括其他個人化的設定檔值。 目前頁面上的個人化內容會儘快顯示，不會有忽隱忽現的預設內容。<br>b.作為使用者在單頁應用程式(SPA)中的動作結果而針對檢視顯示的個人化內容會經過快取，以便在觸發檢視時立刻套用，不需額外的伺服器呼叫。 <br>c. Edge網路會傳送訪客ID和Cookie中的其他值，例如同意、工作階段ID、身分、Cookie檢查、個人化等。 |
| 7 | 邊緣網路轉送 [!UICONTROL 目標分析] 「 」的(A4T)詳細資料（活動、體驗和轉換中繼資料） [!DNL Analytics] edge。 |

## 正在啟用 [!DNL Adobe Target]

若要啟用 [!DNL Target]，請執行下列動作：

1. 啟用 [!DNL Target] 在您的 [資料串流](../../datastreams/overview.md) 並附上適當的使用者端代碼。
1. 新增 `renderDecisions` 選項新增至您的事件。

然後，您也可選擇新增下列選項：

* **`decisionScopes`**：將此選項新增至事件，擷取特定活動（適用於使用表單式撰寫器建立的活動）。
* **[預先隱藏程式碼片段](../manage-flicker.md)**：僅隱藏頁面的某些部分。

## 使用Adobe Target VEC

若要搭配使用VEC [!DNL Platform Web SDK] 實作，安裝並啟動 [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) 或 [鉻黃](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper擴充功能。

如需詳細資訊，請參閱 [視覺化體驗撰寫器Helper擴充功能](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) 在 *Adobe Target指南*.

## 呈現個人化內容

另請參閱 [呈現個人化內容](../rendering-personalization-content.md) 以取得詳細資訊。

## XDM中的對象

為您的定義對象時 [!DNL Target] 透過傳遞的活動 [!DNL Platform Web SDK]， [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hans) 必須定義及使用。 定義XDM結構描述、類別和結構描述欄位群組後，您可以建立 [!DNL Target] 由XDM資料定義的對象規則，用於鎖定目標。 範圍 [!DNL Target]，XDM資料會顯示在 [!UICONTROL Audience Builder] 作為自訂引數。 XDM是使用點標籤法序列化(例如， `web.webPageDetails.name`)。

如果您有 [!DNL Target] 具有預先定義對象、使用自訂引數或使用者設定檔的活動，無法透過SDK正確傳送。 您必須改用XDM，而不是使用自訂引數或使用者設定檔。 不過，有現成的受眾目標定位欄位可透過 [!DNL Platform Web SDK] 不需要XDM的版本。 這些欄位位於 [!DNL Target] 不需要XDM的UI：

* 定位库
* 地域
* 网络
* 操作系统
* 站点页面
* 浏览器
* 流量源
* 时间范围

如需詳細資訊，請參閱 [對象的類別](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=en) 在 *Adobe Target指南*.

### 响应令牌

回應Token主要用於傳送中繼資料給第三方，例如Google、Facebook等。 回應Token會傳回 `meta` 欄位範圍 `propositions` -> `items`. 範例如下：

```json
{
  "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI2NzM2IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
  "scope": "__view__",
  "scopeDetails": ...,
  "renderAttempted": true,
  "items": [
    {
      "id": "0",
      "schema": "https://ns.adobe.com/personalization/dom-action",
      "meta": {
        "experience.id": "0",
        "activity.id": "126736",
        "offer.name": "Default Content",
        "offer.id": "0"
      }
    }
  ]
}
```

若要收集回應Token，您必須訂閱 `alloy.sendEvent` Promise，逐一檢視 `propositions`
並從中擷取詳細資訊 `items` -> `meta`. 每 `proposition` 具有 `renderAttempted` 布林值欄位，指出 `proposition` 是否呈現。 請參閱下列範例：

```js
alloy("sendEvent",
  {
    renderDecisions: true,
    decisionScopes: [
      "hero-container"
    ]
  }).then(result => {
    const { propositions } = result;

    // filter rendered propositions
    const renderedPropositions = propositions.filter(proposition => proposition.renderAttempted === true);

    // collect the item metadata that represents the response tokens
    const collectMetaData = (items) => {
      return items.filter(item => item.meta !== undefined).map(item => item.meta);
    }

    const pageLoadResponseTokens = renderedPropositions
      .map(proposition => collectMetaData(proposition.items))
      .filter(e => e.length > 0)
      .flatMap(e => e);
  });
  
```

啟用自動轉譯時，主張陣列包含：

#### 在頁面載入時：

* 表單式撰寫器型 `propositions` 替換為 `renderAttempted` 標幟設定為 `false`
* 視覺化體驗撰寫器式主張，具有 `renderAttempted` 標幟設定為 `true`
* 單一頁面應用程式檢視的視覺化體驗撰寫器型主張，具有 `renderAttempted` 標幟設定為 `true`

#### 檢視時 — 變更（針對快取檢視）：

* 單一頁面應用程式檢視的視覺化體驗撰寫器型主張，具有 `renderAttempted` 標幟設定為 `true`

停用自動轉譯時，主張陣列包含：

#### 在頁面載入時：

* 表單式撰寫器型 `propositions` 替換為 `renderAttempted` 標幟設定為 `false`
* 視覺化體驗撰寫器式主張，具有 `renderAttempted` 標幟設定為 `false`
* 單一頁面應用程式檢視的視覺化體驗撰寫器型主張，具有 `renderAttempted` 標幟設定為 `false`

#### 檢視時 — 變更（針對快取檢視）：

* 單一頁面應用程式檢視的視覺化體驗撰寫器型主張，具有 `renderAttempted` 標幟設定為 `false`

### 單一設定檔更新

此 [!DNL Platform Web SDK] 可讓您更新設定檔至 [!DNL Target] 設定檔和 [!DNL Platform Web SDK] 做為體驗事件。

若要更新 [!DNL Target] 設定檔時，請確保已使用以下專案傳遞設定檔資料：

* 在 `"data {"`
* 在 `"__adobe.target"`
* 前置詞 `"profile."` 例如，如下所示

| 键 | 类型 | 描述 |
| --- | --- | --- |
| `renderDecisions` | 布尔值 | 指示個人化元件是否應解譯DOM動作 |
| `decisionScopes` | 陣列 `<String>` | 要擷取決定的範圍清單 |
| `xdm` | 对象 | 在Platform Web SDK中以體驗事件形式登陸的XDM格式資料 |
| `data` | 对象 | 任意索引鍵/值組傳送至 [!DNL Target] 目標類別下的解決方案。 |

典型 [!DNL Platform Web SDK] 使用此命令的程式碼如下所示：

**`sendEvent`包含設定檔資料**

```js
alloy("sendEvent", {
   renderDecisions: true|false,
   xdm: { // Experience Event XDM data },
   data: { // Freeform data }
});
```

**如何傳送設定檔屬性至Adobe Target：**

```js
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## 要求建議

下表列出 [!DNL Recommendations] 屬性以及是否透過 [!DNL Platform Web SDK]：

| 类别 | 属性 | 支援狀態 |
| --- | --- | --- |
| Recommendations — 預設實體屬性 | entity.id | 受支持 |
|  | entity.name | 受支持 |
|  | entity.categoryId | 受支持 |
|  | entity.pageUrl | 受支持 |
|  | entity.thumbnailUrl | 受支持 |
|  | entity.message | 受支持 |
|  | entity.value | 受支持 |
|  | entity.inventory | 受支持 |
|  | entity.brand | 受支持 |
|  | entity.margin | 受支持 |
|  | entity.event.detailsOnly | 受支持 |
| Recommendations — 自訂實體屬性 | entity.yourCustomAttributeName | 受支持 |
| Recommendations — 保留的mbox/頁面引數 | excludedIds | 受支持 |
|  | cartIds | 受支持 |
|  | productPurchasedId | 受支持 |
| 類別相關性的頁面或料號類別 | user.categoryId | 受支持 |

**如何將Recommendations屬性傳送至Adobe Target：**

```js
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## 调试

已棄用mboxTrace和mboxDebug。 使用 [[!DNL Platform Web SDK] 偵錯](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html).

## 术语

__主張：__ 在 [!DNL Target]，此主張與從活動選取的體驗相關聯。

__結構描述：__ 決定的結構描述是中的優惠型別 [!DNL Target].

__範圍：__ 決定的範圍。 在 [!DNL Target]，範圍是mBox。 全域mBox是 `__view__` 範圍。

__XDM：__ XDM會序列化為點標籤法，然後放入 [!DNL Target] 作為mBox引數。

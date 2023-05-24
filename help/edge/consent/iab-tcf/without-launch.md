---
title: 使用Adobe Experience Platform Web SDK整合IAB TCF 2.0支援
description: 瞭解如何設定網站的IAB TCF 2.0支援，而不使用標籤。
seo-description: Learn how to set up IAB TCF 2.0 consent with Adobe Experience Platform Web SDK
exl-id: 14f1802a-0f8d-487f-ae17-5daaaab05162
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# 將IAB TCF 2.0支援與Platform Web SDK整合

本指南說明如何在不使用標籤的情況下，將Interactive Advertising Bureau Transparency &amp; Consent Framework 2.0版(IAB TCF 2.0)與Adobe Experience Platform Web SDK整合。 如需與IAB TCF 2.0整合的概觀，請參閱 [概觀](./overview.md). 如需如何與標籤整合的指南，請閱讀 [IAB TCF 2.0標籤指南](./with-launch.md).

## 快速入门

本指南使用 `__tcfapi` 存取同意資訊的介面。 您可以更輕鬆地直接與雲端管理提供者(CMP)整合。 不過，本指南中的資訊可能仍然有用，因為CMP通常提供與TCF API類似的功能。

>[!NOTE]
>
>這些範例假設在執行程式碼時， `window.__tcfapi` 定義於頁面上。 CMP可提供掛接，讓您可以在下列情況下執行這些函式： `__tcfapi` 物件已就緒。

若要搭配標籤和Adobe Experience Platform Web SDK擴充功能使用IAB TCF 2.0，您需要有XDM結構描述可用。 如果您尚未設定上述任何一項，請先檢視此頁面再繼續。

此外，本指南也要求您實際瞭解Adobe Experience Platform Web SDK。 如需快速複習內容，請閱讀 [Adobe Experience Platform Web SDK總覽](../../home.md) 和 [常見問題](../../web-sdk-faq.md) 說明檔案。

## 啟用預設同意

如果您希望以相同方式處理所有未知使用者，您可以將預設同意設定為 `pending` 或 `out`. 在收到同意偏好設定之前，這會佇列或捨棄體驗事件。

如需預設同意的詳細資訊，請參閱 [預設同意區段](../../fundamentals/configuring-the-sdk.md#default-consent) （位於Platform Web SDK設定檔案中）。

### 設定預設同意依據 `gdprApplies`

有些CMP提供判斷一般資料保護規範(GDPR)是否適用於客戶的能力。 如果您希望客戶同意GDPR不適用的情況，您可以使用 `gdprApplies` TCF API呼叫中的旗標。

以下範例顯示執行此操作的一種方式：

```javascript
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

在此範例中， `configure` 命令是在以下專案之後呼叫： `tcData` 是從TCF API取得。 若 `gdprApplies` 為true，預設同意設定為 `pending`. 若 `gdprApplies` 為false，預設同意設為 `in`. 請務必填寫 `alloyConfiguration` 變數來識別。

>[!NOTE]
>
>當預設同意設定為 `in`，則 `setConsent` 命令仍可用來記錄客戶的同意偏好設定。

## 使用setConsent事件

IAB TCF 2.0 API會提供客戶更新同意時適用的事件。 當客戶最初設定其偏好設定以及客戶更新其偏好設定時，就會發生這種情況。

以下範例顯示執行此操作的一種方式：

```javascript
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

此程式碼區塊會接聽 `useractioncomplete` 事件，然後設定同意、傳遞同意字串和 `gdprApplies` 標幟。 如果您有客戶的自訂身分，請務必填寫 `identityMap` 變數。 請參閱以下指南： [支援同意](../../consent/supporting-consent.md) 有關呼叫的詳細資訊 `setConsent`.

## 在sendEvent中包含同意資訊

在XDM結構描述中，您可以儲存來自體驗事件的同意偏好設定資訊。 有兩種方式可將此資訊新增至每個事件。

首先，您可以在上提供相關的XDM結構描述，每 `sendEvent` 呼叫。 以下範例顯示執行此操作的一種方式：

```javascript
var sendEventOptions = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    sendEventOptions.xdm.consentStrings = [{
      consentStandard: "IAB TCF"
      consentStandardVersion: "2.0"
      consentStringValue: tcData.tcString,
      gdprApplies: tcData.gdprApplies
    }];
    window.alloy("sendEvent", sendEventOptions);
  }
});
```

此範例會取得TCF API的同意資訊，然後傳送包含已新增至XDM結構描述之同意資訊的事件。 請參閱 [追蹤事件](../../fundamentals/tracking-events.md) 指南以瞭解應包含在 `sendEvent` 命令選項。

將同意資訊新增至每個請求的另一種方式是 `onBeforeEventSend` callback。 閱讀以下章節： [全域修改事件](../../fundamentals/tracking-events.md#modifying-events-globally) 從追蹤事件檔案中，取得如何執行此動作的詳細資訊。

## 后续步骤

現在您已瞭解如何將IAB TCF 2.0與Platform Web SDK擴充功能搭配使用，您也可以選擇與其他Adobe解決方案(例如Adobe Analytics或Adobe Real-time Customer Data Platform)整合。 請參閱 [IAB透明與同意架構2.0概覽](./overview.md) 以取得詳細資訊。

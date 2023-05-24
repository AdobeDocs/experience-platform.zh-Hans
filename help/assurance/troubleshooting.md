---
title: Adobe Experience Platform保證疑難排解指南
description: 本檔案概述使用Adobe Experience Platform保證時常見問題的解決方案。
exl-id: 8078e6f6-ca18-4939-a417-40ebf5a52e24
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 3%

---

# 疑難排解Adobe Experience Platform保證

如果您無法讓保證開始運作，請參閱下列問題主題下的建議，以解決常見的問題。

若要啟用更順暢的實作並探索任何潛在問題，請確保您已根據以下設定開啟SDK記錄： [啟用偵錯記錄](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) （位於快速入門區段）。

您可以使用變更SDK記錄層級 [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel) API。

## 裝置上、應用程式問題

### QR碼未開啟應用程式

* 直接存取連結。 複製連結來源 **工作階段詳細資訊**. 將其貼到裝置的瀏覽器位址列以開啟。 如果檔案未開啟，請參閱區段 [應用程式未開啟連結](#app-does-not-open-link).
* 使用不同的QR閱讀器。 若是iOS 11或更新版本，請使用像片應用程式來讀取二維碼。

### 應用程式未開啟連結

* 確認應用程式中的深層連結實作已正確設定。
   * **Android：** 深層連結（應用程式連結）
      * [建立應用程式內容的深層連結](https://developer.android.com/training/app-links/deep-linking)
   * **iOS：** 自訂URL配置或通用連結
      * [為您的應用程式定義自訂URL配置](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [在您的應用程式中支援通用連結](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>若為Android，則為 `startSession` API不需要明確呼叫。 若為iOS，請依照中的說明使用API [Adobe Experience Platform保證](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core).

### 出現驗證覆蓋，但應用程式無法連線

* 確保裝置透過裝置網頁瀏覽器連線至網際網路。
* 如果應用程式從未成功連線至Assurance服務，請確保已正確設定Assurance。 請參閱安裝說明 [Adobe Experience Platform保證](./tutorials/implement-assurance.md) SDK程式庫。
* 驗證工作階段符合連結，且已針對預期的工作階段正確輸入。 另請參閱 [記錄訊息「無法使用OrgID資訊」](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) （只有當您擁有多個ORG例項的存取權時，才不常見且相關）。

### Adobe Analytics除錯

**後處理狀態 — 無偵錯旗標**

在「Analytics事件」檢視中，如果事件失敗並顯示後續處理狀態「No Debug Flag」，表示您目前的Adobe Analytics或Assurance SDK版本可能不支援「Analytics偵錯」功能。
請將Adobe Analytics和Assurance SDK擴充功能升級至最新版本，以解決此問題。

| 最低版本需求 | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Assurance | > 1.0.0 | > 1.0.0 |

### React Native MobileCore和AEPAssurance相容性

| AEP保證版本 | 行動核心版本 | 安裝指示 |
| --------------------- | ------------------- | ------------------- |
| react-native-aepassurance v2.x.x | [react-native-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| react-native-aepassurance v3.x.x | [react-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

如果您使用 `react-native-acpcore` 使用Assurance時，React原生應用程式可能會因下列錯誤訊息之一而無法建置：

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

或

```
AppDelegate: AEPAssurance.h file not found
```

**解决方案**

如果發生上述情況，請將您的 `react-native-aepassurance` 使用下列npm命令：

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

發生此錯誤是因為 `react-native-acpcore` 擴充功能為 **僅限** 相容於 `react-native-aepassurance` 版本2.x.x及更低版本。

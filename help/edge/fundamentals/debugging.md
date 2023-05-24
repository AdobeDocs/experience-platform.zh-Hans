---
title: 在Adobe Experience Platform Web SDK中偵錯
description: 瞭解如何在Experience PlatformWeb SDK中切換偵錯功能。
keywords: 偵錯web sdk；偵錯；設定；設定命令；偵錯命令；edgeConfigId；setDebug；debugEnabled；偵錯；
exl-id: 4e893af8-a48e-48dc-9737-4c61b3355f03
source-git-commit: f5270d1d1b9697173bc60d16c94c54d001ae175a
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 2%

---

# 调试

啟用偵錯功能後，SDK會將訊息輸出至瀏覽器主控台，有助於對實作進行偵錯，並瞭解SDK的表現。

除錯功能預設為停用，但可透過四種不同方式開啟：

* `configure` 命令
* `setDebug` 命令
* 查詢字串引數
* 在Adobe Experience Platform Debugger中切換啟用偵錯。 Adobe Experience Platform是一款功能強大的工具，可檢查您的網頁，並協助您針對Experience Cloud產品的實作問題進行偵錯。 Adobe Experience Platform Debugger可同時作為 [鉻黃](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) 和 [Firefox](https://addons.mozilla.org/zh-CN/firefox/addon/adobe-experience-platform-dbg/) 副檔名。 您可以從AEP Web SDK區段的設定標籤啟用偵錯。

![](../assets/enable-debugging.png)

## 使用Configure命令切換偵錯

使用設定SDK時 `configure` 命令，透過設定 `debugEnabled` 選項至 `true`.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "debugEnabled": true
});
```

>[!TIP]
>
>這可讓網頁的所有使用者進行偵錯，而不只是您的個人瀏覽器。

## 使用Debug命令切換偵錯

使用個別專案切換除錯 `debug` 命令，如下所示：

```javascript
alloy("setDebug", {
  "enabled": true
});
```

如果您不想變更網頁上的程式碼，或不想為網站的所有使用者產生記錄訊息，這會特別有用，因為您可以執行 `debug` 命令來執行。

## 使用查詢字串引數切換除錯

透過設定來切換偵錯 `alloy_debug` 查詢字串引數至 `true` 或 `false` 如下所示：

```HTTP
http://example.com/?alloy_debug=true
```

類似於 `debug` 命令，如果您不想變更網頁上的程式碼，或不想為網站的所有使用者產生記錄訊息，這會特別有用，因為您可以在瀏覽器中載入網頁時設定查詢字串引數。

## 優先順序和期間

當透過設定偵錯時 `debug` 命令或查詢字串引數，會覆寫任何 `debug` 選項設定於 `configure` 命令。 在這兩種情況下，在工作階段期間，除錯功能也會保持開啟狀態。 換言之，如果您使用debug命令或查詢字串引數啟用偵錯，則會保持啟用狀態，直到下列其中一項：

* 工作階段結束
* 您執行 `debug` 命令
* 您再次設定查詢字串引數

## 正在擷取程式庫資訊

存取您已載入網站之程式庫背後的某些詳細資訊，通常會有幫助。 若要這麼做，請執行 `getLibraryInfo` 命令，如下所示：

```js
alloy("getLibraryInfo").then(function(result) {
  console.log(result.libraryInfo.version);
  console.log(result.libraryInfo.commands);
  console.log(result.libraryInfo.configs);
});
```

目前，提供 `libraryInfo` 物件包含下列屬性：

* `version`：這是載入的程式庫版本。 例如，如果要載入的程式庫版本是1.0.0，則值會是 `1.0.0`. 當程式庫在標籤擴充功能（名為「AEP Web SDK」）中執行時，版本為程式庫版本，而標籤擴充功能版本以「+」符號連結。 例如，如果程式庫的版本是1.0.0，而標籤擴充功能的版本是1.2.0，則值會是 `1.0.0+1.2.0`.
* `commands`：這些是載入的程式庫支援的所有可用命令。
* `configs`：這些是載入的程式庫中所有的目前設定。

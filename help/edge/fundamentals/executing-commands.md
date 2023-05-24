---
title: 執行Adobe Experience Platform Web SDK命令
description: 瞭解如何執行Experience PlatformWeb SDK命令
keywords: 執行命令；commandName；Promise；getLibraryInfo；回應物件；同意；
exl-id: dda98b3e-3e37-48ac-afd7-d8852b785b83
source-git-commit: f3344c9c9b151996d94e40ea85f2b0cf9c9a6235
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 2%

---

# 執行命令


在您的網頁上實作基底程式碼後，您就可以開始使用SDK執行命令。 您不需要等待外部檔案(`alloy.js`)，以便在執行命令之前從伺服器載入。 如果SDK尚未完成載入，SDK會儘快將命令排入佇列及處理。

命令使用下列語法執行。

```javascript
alloy("commandName", options);
```

此 `commandName` 告訴SDK該做什麼，同時 `options` 是您想要傳遞至命令的引數和資料。 由於可用選項取決於命令，請參考檔案以瞭解有關每個命令的更多詳細資訊。

## 承諾注意事項

[Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 是SDK與網頁上程式碼通訊的基礎。 Promise是一種常見的程式設計結構，並非此SDK或JavaScript特有的。 Promise會作為建立Promise時未知之值的代理。 知道值後，就會使用值「解析」Promise。 處理常式函式可與Promise相關聯，以便在Promise已解決或在解析Promise的程式中發生錯誤時通知您。 若要進一步瞭解承諾，請閱讀 [本教學課程](https://javascript.info/promise-basics) 或網頁上的任何其他資源。

## 處理成功或失敗 {#handling-success-or-failure}

每次執行命令時，都會傳回Promise。 promise代表命令的最終完成。 在以下範例中，您可以使用 `then` 和 `catch` 用來判斷命令是否成功的方法。

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" is whatever the command returned
  })
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

如果知道指令何時成功對您來說並不重要，您可以移除 `then` 呼叫。

```javascript
alloy("commandName", options)
  .catch(function(error) {
    // The command failed.
    // "error" is an error object with additional information
  });
```

同樣地，如果知道命令何時失敗對您來說並不重要，您可以移除 `catch` 呼叫。

```javascript
alloy("commandName", options)
  .then(function(result) {
    // The command succeeded.
    // "value" will be whatever the command returned
  });
```

### 回應物件

從命令傳回的所有promise都使用 `result` 物件。 根據命令和使用者的同意，結果物件將包含資料。 例如，程式庫資訊會作為結果物件的屬性在下列命令中傳遞。

```js
alloy("getLibraryInfo")
  .then(function(result) {
    console.log(result.libraryInfo.version);
    console.log(result.libraryInfo.commands);
    console.log(result.libraryInfo.configs);
  });
```

### 同意

如果使用者未針對特定目的提供其同意，仍會解析Promise；不過，回應物件將僅包含可在使用者同意的內容中提供的資訊。

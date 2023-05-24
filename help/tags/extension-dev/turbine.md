---
title: Turbine自由變數
description: 瞭解Turbine物件，這是一個自由變數，提供Adobe Experience Platform標籤執行階段專用的資訊和公用程式。
exl-id: 1664ab2e-8704-4a56-8b6b-acb71534084e
source-git-commit: 27dd38cc509040ea9dc40fc7030dcdec9a182d55
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 49%

---

# Turbine 自由变量

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../term-updates.md)。

`turbine` 对象是扩展库模块范围内的“自由变量”。它提供Adobe Experience Platform標籤執行階段的特定資訊和公用程式，且程式庫模組隨時都可加以使用（無需使用） `require()`.

## `buildInfo`

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` 是一個物件，其中包含目前標籤執行階段程式庫的相關建置資訊。

```js
{
    turbineVersion: "14.0.0",
    turbineBuildDate: "2016-07-01T18:10:34Z",
    buildDate: "2016-03-30T16:27:10Z"
}
```

| 属性 | 描述 |
| --- | --- |
| `turbineVersion` | 当前库中使用的 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) 版本。 |
| `turbineBuildDate` | 生成容器内使用的 [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) 版本的 ISO 8601 日期。 |
| `buildDate` | 生成当前库的 ISO 8601 日期。 |

{style="table-layout:auto"}

## `environment`

```js
console.log(turbine.environment.stage);
```

`turbine.environment` 是一個物件，其中包含程式庫部署所在環境的相關資訊。

```js
{
    id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
    stage: "development"
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 環境的ID。 |
| `stage` | 生成此库的环境。可能的值包括 `development`， `staging`、和 `production`. |

{style="table-layout:auto"}

## `debugEnabled`

表示標籤偵錯目前是否啟用的布林值。

如果您只是尝试记录消息，则可能不需要使用此功能。請一律使用下列方式記錄訊息： `turbine.logger` 以確保在啟用標籤偵錯功能時，您的訊息只會列印至主控台。

## `getDataElementValue`

```js
console.log(turbine.getDataElementValue(dataElementName));
```

返回数据元素的值。

## `getExtensionSettings` {#get-extension-settings}

```js
var extensionSettings = turbine.getExtensionSettings();
```

返回上次从[扩展配置](./configuration.md)视图中保存的设置对象。

请注意，返回的设置对象中的值可能来自数据元素。因此，如果数据元素的值发生变化，那么在不同时间调用 `getExtensionSettings()` 可能会产生不同的结果。若要取得最新的值，請儘可能久地等候後再呼叫 `getExtensionSettings()`.

## `getHostedLibFileUrl` {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

此 [Hostedlibfiles](./manifest.md) 屬性可定義於擴充功能資訊清單中，以將各種檔案與標籤執行階段程式庫裝載在一起。 此模块会返回托管给定库文件的 URL。

## `getSharedModule` {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

擷取已從其他擴充功能共用的模組。 如果找不到匹配的模块，则返回 `undefined`。有关共享模块的更多信息，请参阅[实施共享模块](./web/shared.md)。

## `logger`

```js
turbine.logger.error('Error!');
```

記錄公用程式用於將訊息記錄到主控台。 仅当用户开启调试功能时，消息才会显示在控制台中。開啟偵錯功能的建議方式，是使用 [Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?src=propaganda). 或者，使用者可以執行以下命令 `_satellite.setDebug(true)` 瀏覽器開發人員控制檯內。 该日志记录器包括以下方法：

* `logger.log(message: string)`：将消息记录到控制台。
* `logger.info(message: string)`：将信息性消息记录到控制台。
* `logger.warn(message: string)`：将警告消息记录到控制台。
* `logger.error(message: string)`：将错误消息记录到控制台。
* `logger.debug(message: string)`：将调试消息记录到控制台。（仅当在浏览器控制台中启用 `verbose` 日志记录时才可见。）
* `logger.deprecation(message: string)`：無論使用者是否啟用標籤偵錯，都會將警告訊息記錄到主控台。

## `onDebugChanged`

將回呼函式傳入 `turbine.onDebugChanged`，標籤會在切換偵錯時呼叫您的回呼。 標籤會將布林值傳至回呼函式，如果啟用偵錯，則值為true；如果禁用偵錯，則值為false。

如果您只是尝试记录消息，则可能不需要使用此功能。請一律使用下列方式記錄訊息： `turbine.logger` 和標籤可確保在啟用標籤偵錯功能時，訊息只會列印至主控台。

## `propertySettings` {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

一個物件，其中包含使用者為目前標籤執行階段程式庫的屬性所定義的下列設定：

* `propertySettings.domains: Array<String>`

   一个由属性涵盖的域数组。

* `propertySettings.undefinedVarsReturnEmpty: boolean`

   扩展开发者不应关注此设置。

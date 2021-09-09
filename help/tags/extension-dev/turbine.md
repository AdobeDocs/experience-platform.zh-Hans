---
title: Turbine自由变量
description: 了解turbine对象，该对象是一个自由变量，可提供特定于Adobe Experience Platform标记运行时的信息和实用程序。
exl-id: 1664ab2e-8704-4a56-8b6b-acb71534084e
source-git-commit: 814f853d16219021d9151458d93fc5bdc6c860fb
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 50%

---

# Turbine 自由变量

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../term-updates.md)。

`turbine` 对象是扩展库模块范围内的“自由变量”。它提供了特定于Adobe Experience Platform标记运行时的信息和实用程序，并且始终可供库模块使用，而无需使用`require()`。

## `buildInfo`

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo` 是一个对象，其中包含有关当前标记运行时库的生成信息。

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


## `environment`

```js
console.log(turbine.environment.stage);
```

`turbine.environment` 是一个对象，其中包含有关库所部署的环境的信息。

```js
{
    id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
    stage: "development"
}
```

| 属性 | 描述 |
| --- | --- |
| `id` | 环境的ID。 |
| `stage` | 生成此库的环境。可能的值为`development`、`staging`和`production`。 |


## `debugEnabled`

一个布尔值，用于指示当前是否启用标记调试。

如果您只是尝试记录消息，则可能不需要使用此功能。相反，应始终使用`turbine.logger`记录消息，以确保在启用标记调试后，消息只打印到控制台。

### `getDataElementValue`

```js
console.log(turbine.getDataElementValue(dataElementName));
```

返回数据元素的值。

### `getExtensionSettings` {#get-extension-settings}

```js
var extensionSettings = turbine.getExtensionSettings();
```

返回上次从[扩展配置](./configuration.md)视图中保存的设置对象。

请注意，返回的设置对象中的值可能来自数据元素。因此，如果数据元素的值发生变化，那么在不同时间调用 `getExtensionSettings()` 可能会产生不同的结果。要获取最新的值，请尽可能等待，然后再调用`getExtensionSettings()`。

### `getHostedLibFileUrl` {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

[hostedLibFiles](./manifest.md)属性可在扩展清单中定义，以便将各种文件与标记运行时库一起托管。 此模块会返回托管给定库文件的 URL。

### `getSharedModule` {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

检索已从其他扩展共享的模块。 如果找不到匹配的模块，则返回 `undefined`。有关共享模块的更多信息，请参阅[实施共享模块](./web/shared.md)。

### `logger`

```js
turbine.logger.error('Error!');
```

日志记录实用程序用于将消息记录到控制台。 仅当用户开启调试功能时，消息才会显示在控制台中。开启调试功能的推荐方法是使用[Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj?src=propaganda)。 作为替代方法，用户可以在浏览器开发人员控制台中运行以下命令`_satellite.setDebug(true)`。 该日志记录器包括以下方法：

* `logger.log(message: string)`：将消息记录到控制台。
* `logger.info(message: string)`：将信息性消息记录到控制台。
* `logger.warn(message: string)`：将警告消息记录到控制台。
* `logger.error(message: string)`：将错误消息记录到控制台。
* `logger.debug(message: string)`：将调试消息记录到控制台。（仅当在浏览器控制台中启用 `verbose` 日志记录时才可见。）

### `onDebugChanged`

每当切换调试功能时，标记通过将回调函数传递到`turbine.onDebugChanged`来调用您的回调。 标记将向回调函数传递一个布尔值，如果启用了调试，则该布尔值为true；如果禁用了调试，则该布尔值为false。

如果您只是尝试记录消息，则可能不需要使用此功能。相反，始终使用`turbine.logger`和标记来记录消息，以确保在启用标记调试后，消息只会打印到控制台。

### `propertySettings` {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

包含以下设置的对象，这些设置由用户为当前标记运行时库的属性定义：

* `propertySettings.domains: Array<String>`

   一个由属性涵盖的域数组。

* `propertySettings.undefinedVarsReturnEmpty: boolean`

   扩展开发者不应关注此设置。

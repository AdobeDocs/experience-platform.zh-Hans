---
title: Turbine自由变量
description: 了解turbine对象，这是一个自由变量，提供特定于Adobe Experience Platform标记运行时的信息和实用程序。
exl-id: 1664ab2e-8704-4a56-8b6b-acb71534084e
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 47%

---

# Turbine 自由变量

`turbine` 对象是扩展库模块范围内的“自由变量”。它提供特定于Adobe Experience Platform标记运行时的信息和实用程序，并且始终可供库模块使用，而无需使用`require()`。

## `buildInfo`

```js
console.log(turbine.buildInfo.turbineBuildDate);
```

`turbine.buildInfo`是一个对象，其中包含有关当前标记运行时库的生成信息。

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

`turbine.environment`是一个对象，其中包含有关库已部署到的环境的信息。

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

{style="table-layout:auto"}

## `debugEnabled`

一个布尔值，指示当前是否启用标记调试。

如果您只是尝试记录消息，则可能不需要使用此功能。相反，请始终使用`turbine.logger`来记录消息，以确保仅在启用标记调试时将消息打印到控制台。

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

请注意，返回的设置对象中的值可能来自数据元素。因此，如果数据元素的值发生变化，那么在不同时间调用 `getExtensionSettings()` 可能会产生不同的结果。若要获取最新的值，请在调用`getExtensionSettings()`之前尽可能长时间地等待。

## `getHostedLibFileUrl` {#get-hosted-lib-file}

```js
var loadScript = require('@adobe/reactor-load-script');
loadScript(turbine.getHostedLibFileUrl('AppMeasurement.js')).then(function() {
  // Do something ...
})
```

可以在扩展清单中定义[hostedLibFiles](./manifest.md)属性，以便随标记运行时库一起托管各种文件。 此模块会返回托管给定库文件的 URL。

## `getSharedModule` {#shared}

```js
var mcidInstance = turbine.getSharedModule('adobe-mcid', 'mcid-instance');
```

检索从其他扩展共享的模块。 如果找不到匹配的模块，则返回 `undefined`。有关共享模块的更多信息，请参阅[实施共享模块](./web/shared.md)。

## `logger`

```js
turbine.logger.error('Error!');
```

日志记录实用程序用于将消息记录到控制台。 仅当用户开启调试功能时，消息才会显示在控制台中。开启调试功能的推荐方法是使用[Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)。 作为替代方法，用户可以在浏览器开发人员控制台中运行以下命令`_satellite.setDebug(true)`。 该日志记录器包括以下方法：

* `logger.log(message: string)`：将消息记录到控制台。
* `logger.info(message: string)`：将信息性消息记录到控制台。
* `logger.warn(message: string)`：将警告消息记录到控制台。
* `logger.error(message: string)`：将错误消息记录到控制台。
* `logger.debug(message: string)`：将调试消息记录到控制台。（仅当在浏览器控制台中启用 `verbose` 日志记录时才可见。）
* `logger.deprecation(message: string)`：将警告消息记录到控制台，无论用户是否启用了标记调试。

## `onDebugChanged`

通过将回调函数传递到`turbine.onDebugChanged`，标记将在切换调试时调用您的回调。 标记将向回调函数传递一个布尔值，如果启用了调试，该值为true；如果禁用了调试，该值则为false。

如果您只是尝试记录消息，则可能不需要使用此功能。相反，始终使用`turbine.logger`来记录消息，并且标记将确保仅在启用标记调试时将消息打印到控制台。

## `propertySettings` {#property-settings}

```js
console.log(turbine.propertySettings.domains);
```

一个包含以下设置的对象，这些设置是用户为当前标记运行时库的属性定义的：

* `propertySettings.domains: Array<String>`

  一个由属性涵盖的域数组。

* `propertySettings.undefinedVarsReturnEmpty: boolean`

  扩展开发者不应关注此设置。

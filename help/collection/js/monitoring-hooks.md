---
title: 监控Adobe Experience Platform Web SDK的挂接
description: 了解如何使用Adobe Experience Platform Web SDK提供的监视挂接来调试您的实施并捕获Web SDK日志。
exl-id: 56633311-2f89-4024-8524-57d45c7d38f7
source-git-commit: 9b2ecedfafbafed042eba73a034cb9b9e95af579
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 6%

---

# 监控Web SDK的挂接

Adobe Experience Platform Web SDK包括监视挂接，您可以使用这些挂接监视各种系统事件。 这些工具可用于开发您自己的调试工具和捕获Web SDK日志。

无论是否启用了[调试](commands/configure/debugenabled.md)，Web SDK都会触发监视功能。

## `onInstanceCreated` {#onInstanceCreated}

当您成功创建了新的Web SDK实例时，将触发此回调函数。 有关函数参数的详细信息，请参阅下面的示例。

```js
onInstanceCreated(data) {
    // data.instanceName
    // data.instance
}
```

| 参数 | 类型 | 描述 |
|---------|----------|----------|
| `data.instanceName` | 字符串 | 存储Web SDK实例的全局变量的名称。 |
| `data.instance` | 函数 | 用于调用Web SDK命令的实例函数。 |

## `onInstanceConfigured` {#onInstanceConfigured}

成功解析[`configure`](commands/configure/overview.md)命令后，Web SDK会触发此回调函数。 有关函数参数的详细信息，请参阅下面的示例。

```js
 onInstanceConfigured(data) {
     // data.instanceName
     // data.config
 }
```

| 参数 | 类型 | 描述 |
|---------|----------|----------|
| `data.instanceName` | 字符串 | 存储Web SDK实例的全局变量的名称。 |
| `data.config` | 对象 | 包含用于Web SDK实例的配置的对象。 这些是传递到[`configure`](commands/configure/overview.md)命令的选项，并添加了所有默认值。 |

## `onBeforeCommand` {#onBeforeCommand}

此回调函数在执行任何其他命令之前由Web SDK触发。 可以使用此函数检索特定命令的配置选项。 有关函数参数的详细信息，请参阅下面的示例。

```js
onBeforeCommand(data) {
    // data.instanceName
    // data.commandName
    // data.options
}
```

| 参数 | 类型 | 描述 |
|---------|----------|----------|
| `data.instanceName` | 字符串 | 存储Web SDK实例的全局变量的名称。 |
| `data.commandName` | 字符串 | 执行此函数之前的Web SDK命令的名称。 |
| `data.options` | 对象 | 包含传递给Web SDK命令的选项的对象。 |

## `onCommandResolved` {#onCommandResolved}

解析命令承诺时会触发此回调函数。 您可以使用此函数查看命令选项和结果。 有关函数参数的详细信息，请参阅下面的示例。

```js
onCommandResolved(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.result
},
```

| 参数 | 类型 | 描述 |
|---------|----------|----------|
| `data.instanceName` | 字符串 | 存储Web SDK实例的全局变量的名称。 |
| `data.commandName` | 字符串 | 已执行的Web SDK命令的名称。 |
| `data.options` | 对象 | 包含传递给Web SDK命令的选项的对象。 |
| `data.result` | 对象 | 包含Web SDK命令结果的对象。 |

## `onCommandRejected` {#onCommandRejected}

此回调函数在命令promise被拒绝之前触发，它包含有关命令被拒绝原因的信息。 有关函数参数的详细信息，请参阅下面的示例。

```js
onCommandRejected(data) {
    // data.instanceName
    // data.commandName
    // data.options
    // data.error
}
```

| 参数 | 类型 | 描述 |
|---------|----------|----------|
| `data.instanceName` | 字符串 | 存储Web SDK实例的全局变量的名称。 |
| `data.commandName` | 字符串 | 已执行的Web SDK命令的名称。 |
| `data.options` | 对象 | 包含传递给Web SDK命令的选项的对象。 |
| `data.error` | 对象 | 一个对象，其中包含从浏览器的网络调用（`fetch`，大多数情况下）返回的错误消息，以及命令被拒绝的原因。 |

## `onBeforeNetworkRequest` {#onBeforeNetworkRequest}

此回调函数在执行网络请求之前触发。 有关函数参数的详细信息，请参阅下面的示例。

```js
onBeforeNetworkRequest(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
}
```

| 参数 | 类型 | 描述 |
|---------|----------|----------|
| `data.instanceName` | 字符串 | 存储Web SDK实例的全局变量的名称。 |
| `data.requestId` | 字符串 | Web SDK为启用调试而生成的`requestId`。 |
| `data.url` | 字符串 | 请求的URL。 |
| `data.payload` | 对象 | 将转换为JSON格式并在请求正文中通过`POST`方法发送的网络请求有效负载对象。 |

## `onNetworkResponse` {#onNetworkResponse}

此回调函数在浏览器收到响应时触发。 有关函数参数的详细信息，请参阅下面的示例。

```js
onNetworkResponse(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.body
    // data.parsedBody
    // data.status
    // data.retriesAttempted
}
```

| 参数 | 类型 | 描述 |
|---------|----------|----------|
| `data.instanceName` | 字符串 | 存储Web SDK实例的全局变量的名称。 |
| `data.requestId` | 字符串 | Web SDK为启用调试而生成的`requestId`。 |
| `data.url` | 字符串 | 请求的URL。 |
| `data.payload` | 对象 | 将转换为JSON格式并通过`POST`方法在请求正文中发送的有效负荷对象。 |
| `data.body` | 字符串 | 字符串格式的响应正文。 |
| `data.parsedBody` | 对象 | 包含已解析的响应主体的对象。 如果解析响应正文时出错，则此参数为未定义。 |
| `data.status` | 字符串 | 整数格式的响应代码。 |
| `data.retriesAttempted` | 整数 | 发送请求时尝试重试的次数。 零表示请求在第一次尝试时成功。 |

## `onNetworkError` {#onNetworkError}

当网络请求失败时，将触发此回调函数。 有关函数参数的详细信息，请参阅下面的示例。

```js
onNetworkError(data) {
    // data.instanceName
    // data.requestId
    // data.url
    // data.payload
    // data.error
},
```

| 参数 | 类型 | 描述 |
|---------|----------|----------|
| `data.instanceName` | 字符串 | 存储Web SDK实例的全局变量的名称。 |
| `data.requestId` | 字符串 | Web SDK为启用调试而生成的`requestId`。 |
| `data.url` | 字符串 | 请求的URL。 |
| `data.payload` | 对象 | 将转换为JSON格式并通过`POST`方法在请求正文中发送的有效负荷对象。 |
| `data.error` | 对象 | 一个对象，其中包含从浏览器的网络调用（`fetch`，大多数情况下）返回的错误消息，以及命令被拒绝的原因。 |

## `onBeforeLog` {#onBeforeLog}

此回调函数在Web SDK将任何内容记录到控制台之前触发。 有关函数参数的详细信息，请参阅下面的示例。

```js
onBeforeLog(data) {
    // data.instanceName
    // data.componentName
    // data.level
    // data.arguments
}
```

| 参数 | 类型 | 描述 |
|---------|----------|----------|
| `data.instanceName` | 字符串 | 存储Web SDK实例的全局变量的名称。 |
| `data.componentName` | 字符串 | 生成日志消息的组件的名称。 |
| `data.level` | 字符串 | 日志记录级别。 支持的级别： `log`、`info`、`warn`、`error`。 |
| `data.arguments` | 字符串数组 | 日志消息的参数。 |


## `onContentRendering` {#onContentRendering}

此回调函数由`personalization`组件在渲染的各个阶段触发。 有效负载可能因`status`参数而异。 有关函数参数的详细信息，请参阅下面的示例。

```js
 onContentRendering(data) {
     // data.instanceName
     // data.componentName
     // data.payload
     // data.status
}
```

| 参数 | 类型 | 描述 |
|---------|----------|----------|
| `data.instanceName` | 字符串 | 存储Web SDK实例的全局变量的名称。 |
| `data.componentName` | 字符串 | 生成日志消息的组件的名称。 |
| `data.payload` | 对象 | 将转换为JSON格式并通过`POST`方法在请求正文中发送的有效负荷对象。 |
| `data.status` | 字符串 | `personalization`组件将渲染状态通知给Web SDK。  支持的值： <ul><li>`rendering-started`：指示Web SDK即将呈现建议。 在Web SDK开始呈现决策范围或视图之前，您可以在`data`对象中看到将由`personalization`组件和范围名称呈现的建议。</li><li>`no-offers`：表示未收到所请求参数的有效负载。</li> <li>`rendering-failed`：表示Web SDK无法呈现建议。</li><li>`rendering-succeeded`：表示已针对决策范围完成渲染。</li> <li>`rendering-redirect`：指示Web SDK将渲染重定向建议。</li></ul> |

## `onContentHiding` {#onContentHiding}

当应用或删除预隐藏样式时，将触发此回调函数。

```js
onContentHiding(data) {
    // data.instanceName
    // data.componentName
    // data.status
}
```

| 参数 | 类型 | 描述 |
|---------|----------|----------|
| `data.instanceName` | 字符串 | 存储Web SDK实例的全局变量的名称。 |
| `data.componentName` | 字符串 | 生成日志消息的组件的名称。 |
| `data.status` | 字符串 | `personalization`组件将渲染状态通知给Web SDK。 支持的值： <ul><li>`hide-containers`</li><li>`show-containers`</ul> |

## 如何在使用NPM包时指定监视挂接 {#specify-monitoring-npm}

如果您通过[NPM包](install/npm.md)使用Web SDK，则可以在`createInstance`函数中指定监视挂接，如下所示。

```js
var monitor = {
  onBeforeCommand(data) {
    console.log(data);
  },
  ...
};
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy", monitors: [monitor] });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

## 示例 {#example}

Web SDK在名为`__alloyMonitors`的全局变量中查找对象数组。

要捕获所有Web SDK事件，必须先定义监视挂接，然后才能将Web SDK代码加载到页面上。 每个监视方法都会捕获Web SDK事件。

您可以在页面上加载&#x200B;*Web SDK代码之后定义监视挂接*，但在页面加载之前触发的任何挂接都将&#x200B;*无法捕获*。

定义监视挂接对象时，只需要定义要为其定义特殊逻辑的方法。
例如，如果您只关心`onContentRendering`，则可以只定义该方法。 您无需一次使用所有监控挂接。

您可以定义多个监视挂接对象。 当触发相应的事件时，将调用给定方法的所有对象。

>[!TIP]
>
>请参阅下面的示例页面，其中实施了所有监视挂接。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window.__alloyMonitors = window.__alloyMonitors || [];
    window.__alloyMonitors.push({
      onInstanceCreated(data) {
        // data.instanceName
        // data.instance
      },
      onInstanceConfigured(data) {
        // data.instanceName
        // data.config
      },
      onBeforeCommand(data) {
        // data.instanceName
        // data.commandName
        // data.options
      },
      // Added in version 2.4.0
      onCommandResolved(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.result
      },
      // Added in version 2.4.0
      onCommandRejected(data) {
        // data.instanceName
        // data.commandName
        // data.options
        // data.error
      },
      onBeforeNetworkRequest(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
      },
      onNetworkResponse(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.body
        // data.parsedBody
        // data.status
        // data.retriesAttempted
      },
      onNetworkError(data) {
        // data.instanceName
        // data.requestId
        // data.url
        // data.payload
        // data.error
      },
      onBeforeLog(data) {
        // data.instanceName
        // data.componentName
        // data.level
        // data.arguments
      }
      onContentRendering(data) {
        // data.instanceName
        // data.componentName
        // data.payload
        // data.status
      },
      onContentHiding(data) {
        // data.instanceName
        // data.componentName
        // data.status
      }
    });
  </script>
  <script>
      !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
      []).push(o),n[o]=function(){var u=arguments;return new Promise(
      function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
      (window,["alloy"]);
    </script>
    <script src="alloy.js" async></script>
</head>
<body>
  <h1>Monitor Test</h1>
</body>
</html>
```

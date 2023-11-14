---
title: 安装Adobe Experience Platform Web SDK
description: 了解如何安装Experience PlatformWeb SDK。
keywords: web sdk安装；安装web sdk；internet explorer；promise；npm包
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 2%

---

# 安装SDK {#installing-the-sdk}

有三种受支持的方法可使用Adobe Experience Platform Web SDK：

1. 使用Adobe Experience Platform Web SDK的首选方式是通过数据收集UI或Experience PlatformUI。
1. Adobe Experience Platform Web SDK也可在内容交付网络(CDN)上提供，以供您使用。
1. 使用导出EcmaScript 5和EcmaScript 2015 (ES6)模块的NPM库。

## 选项1：安装标记扩展

有关标记扩展的文档，请参阅 [标记文档](../../tags/extensions/client/web-sdk/overview.md)

## 选项2：安装预生成的独立版本

预建版本在CDN上可用。 您可以在页面上直接在CDN上引用库，也可以将其下载并托管在您自己的基础架构上。 它以缩小和未缩小的格式提供。 未缩小的版本有助于进行调试。

URL结构： https://cdn1.adoberesources.net/alloy/[版本]/alloy.min.js或alloy.js（非缩小版本）。

例如：


* 缩小： [https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js)
* 未缩小： [https://cdn1.adoberesources.net/alloy/2.14.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.14.0/alloy.js)


### 添加代码 {#adding-the-code}

预建独立版本要求直接在页面中添加“基础代码”。 将以下“基础代码”复制并粘贴到尽可能高的位置 `<head>` HTML的标记：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

“基础代码”创建一个名为的全局函数 `alloy`. 使用此函数与SDK交互。 如果要将全局函数命名为其他名称，请更改 `alloy` 名称，如下所示：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

在此示例中，将重命名全局函数 `mycustomname`，而不是 `alloy`.

>[!IMPORTANT]
>
>要避免出现潜在问题，请使用至少包含一个非数字字符且不会与上已找到的属性名称冲突的名称 `window`.

此基础代码除了创建全局函数外，还会加载外部文件中包含的附加代码\(`alloy.js`\)托管在服务器上。 默认情况下，将异步加载此代码，以使您的网页尽可能提高性能。 这是推荐的实施。

### 支持Explorer {#support-internet-explore}

此SDK使用promise ，这是一种用于通信异步任务完成情况的方法。 此 [Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 除以下内容外，所有目标浏览器均本机支持SDK使用的实施 [!DNL Internet Explorer]. 要在上使用SDK，请执行以下操作 [!DNL Internet Explorer]，您必须拥有 `window.Promise` [多填充](https://remysharp.com/2010/10/08/what-is-a-polyfill).

以确定您是否已经拥有 `window.Promise` 多填充：

1. 在中打开您的网站 [!DNL Internet Explorer].
1. 打开浏览器的调试控制台。
1. 类型 `window.Promise` 进入控制台，然后按Enter。

如果不是 `undefined` 显示，您可能已经填充了 `window.Promise`. 确定是否 `window.Promise` ，方法是在完成上述安装说明后加载您的网站。 如果SDK抛出错误，提及了某个承诺的内容，则您可能没有进行复填 `window.Promise`.

如果您已确定，则必须进行多边形填充 `window.Promise`，请在之前提供的基础代码上方包含以下脚本标记：

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

此标记会加载一个脚本，用于确保 `window.Promise` 是有效的Promise实施。

>[!NOTE]
>
>如果选择加载其他Promise实施，请确保该实施支持 `Promise.prototype.finally`.

### 同步加载JavaScript文件 {#loading-javascript-synchronously}

如一节所述 [添加代码](#adding-the-code)，您复制并粘贴到网站HTML中的基础代码将加载外部文件。 外部文件包含SDK的核心功能。 在此文件加载时尝试执行的任何命令都会排入队列，然后在文件加载后进行处理。 异步加载文件是性能最佳的安装方法。

但在特定情况下，您可能希望同步加载文件\（稍后将记录有关这些情况的更多详细信息\）。 此操作会阻止浏览器解析和渲染HTML文档的其余部分，直到加载和执行外部文件为止。 通常建议不要在向用户显示主要内容之前再延迟一次，但根据具体情况而定，这样做可能会有意义。

要以同步方式而不是异步方式加载文件，请删除 `async` 属性来自第二个 `script` 标记如下所示：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js"></script>
```

## 选项3：使用NPM包

Adobe Experience Platform Web SDK还作为NPM包提供。 [npm](https://www.npmjs.com) 是JavaScript的包管理器。 通过安装NPM包，您可以控制Adobe Experience Platform Web SDK JavaScript的构建过程。 NPM包会公开要在浏览器中运行的EcmaScript版本5模块或EcmaScript版本2015 (ES6)模块。

```bash
npm install @adobe/alloy
```

Adobe Experience Platform Web SDK的NPM包会公开 `createInstance` 函数。 此函数用于创建实例。 传递到函数的name选项可控制日志记录中使用的前缀。 以下是使用该包的示例。

### 将软件包用作ECMAScript 2015 (ES6)模块

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>NPM包依赖于CommonJS模块；因此，在使用捆绑包时，请确保该捆绑包支持CommonJS模块。 一些捆绑包，例如 [汇总](https://rollupjs.org)，需要 [插件](https://www.npmjs.com/package/@rollup/plugin-commonjs) 提供CommonJS支持。

### 将软件包用作ECMAScript 5模块

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### 支持Explorer

Adobe Experience Platform SDK使用promise ，这是一种用于通信异步任务完成情况的方法。 此 [Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) 除以下内容外，所有目标浏览器均本机支持SDK使用的实施 [!DNL Internet Explorer]. 要在上使用SDK，请执行以下操作 [!DNL Internet Explorer]，您必须拥有 `window.Promise` [多填充](https://remysharp.com/2010/10/08/what-is-a-polyfill).

有一个可用于聚合填充promise的库是promise-polyfill。 请参阅 [promise-polyfill文档](https://www.npmjs.com/package/promise-polyfill) 有关如何使用NPM安装的更多信息。

>[!NOTE]
>
>如果选择加载其他Promise实施，请确保该实施支持 `Promise.prototype.finally`.

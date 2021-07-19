---
title: 安装Adobe Experience Platform Web SDK
description: 了解如何安装Experience PlatformWeb SDK。
keywords: Web SDK安装；安装Web SDK;Internet Explorer;promise;npm包
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 2%

---

# 安装SDK {#installing-the-sdk}

使用Adobe Experience Platform Web SDK的方法有三种：

1. 使用Adobe Experience Platform Web SDK的首选方式是通过[Adobe Experience Platform Launch](https://launch.adobe.com/)。
1. Adobe Experience Platform Web SDK还可在内容交付网络(CDN)上提供，供您使用。
1. 使用用于导出EcmaScript 5和EcmaScript 2015(ES6)模块的NPM库。

## 选项1:安装Adobe Experience Platform Launch扩展

有关Adobe Experience Platform Launch扩展的文档，请参阅[launch文档](../../tags/extensions/web/sdk/overview.md)

## 选项2:安装预建的独立版本

预建版本可在CDN上使用。 您可以直接在页面上引用CDN上的库，或在自己的基础架构下载并托管该库。 它以缩小和未缩小的格式提供。 未缩小版本有助于进行调试。

URL结构：https://cdn1.adoberesources.net/alloy/[版本]/alloy.min.js或用于非缩小版本的alloy.js。

例如：


* 缩小：[https://cdn1.adoberesources.net/alloy/2.5.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.5.0/alloy.min.js)
* 未缩小：[https://cdn1.adoberesources.net/alloy/2.5.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.5.0/alloy.js)


### 添加代码 {#adding-the-code}

预建的独立版本要求直接将“基础代码”添加到页面。 在HTML的`<head>`标记中尽可能高地复制并粘贴以下“基本代码”：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.5.0/alloy.min.js" async></script>
```

“基本代码”将创建一个名为`alloy`的全局函数。 使用此函数与SDK进行交互。 如果要为全局函数命名其他名称，请按如下方式更改`alloy`名称：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.5.0/alloy.min.js" async></script>
```

在此示例中，全局函数被重命名为`mycustomname`，而不是`alloy`。

>[!IMPORTANT]
>
>为避免出现潜在问题，请使用至少包含一个非数字且与`window`上已找到的属性名称不冲突的字符的名称。

除了创建全局函数之外，此基础代码还加载其他代码，这些代码包含在服务器上托管的外部文件\(`alloy.js`\)中。 默认情况下，此代码会异步加载，以尽可能提高网页的性能。 这是建议的实施。

### 支持Internet Explorer {#support-internet-explore}

此SDK使用promise，promise是用于传递异步任务完成情况的方法。 SDK使用的[Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)实施本地受除[!DNL Internet Explorer]之外的所有目标浏览器支持。 要在[!DNL Internet Explorer]上使用SDK，您必须具有`window.Promise` [polycilled](https://remysharp.com/2010/10/08/what-is-a-polyfill)。

要确定是否已填充`window.Promise`聚合，请执行以下操作：

1. 在[!DNL Internet Explorer]中打开您的网站。
1. 打开浏览器的调试控制台。
1. 在控制台中键入`window.Promise`，然后按Enter。

如果出现“`undefined`”以外的内容，则可能已经填充了“`window.Promise`”。 确定`window.Promise`是否已填充的另一种方法是，在完成上述安装说明后加载您的网站。 如果SDK引发提及承诺内容的错误，则您可能尚未填充`window.Promise`。

如果您确定必须对`window.Promise`进行多填充，请在先前提供的基本代码上方包含以下脚本标记：

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

此标记加载一个脚本，以确保`window.Promise`是有效的Promise实施。

>[!NOTE]
>
>如果选择加载其他Promise实施，请确保它支持`Promise.prototype.finally`。

### 同步加载JavaScript文件 {#loading-javascript-synchronously}

如[添加代码](#adding-the-code)部分中所述，您复制并粘贴到网站HTML中的基本代码会加载外部文件。 外部文件包含SDK的核心功能。 加载此文件时尝试执行的任何命令都将排入队列，然后在加载文件后进行处理。 异步加载文件是安装效率最高的方法。

但是，在某些情况下，您可能希望同步加载文件\（以后将记录有关这些情况的更多详细信息\）。 这样做会阻止浏览器解析和渲染HTML文档的其余部分，直到加载和执行外部文件为止。 在向用户显示主内容之前，通常不会采取这种额外的延迟措施，但具体情况可能会有所不同。

要同步加载文件而不是异步加载，请从第二个`script`标记中删除`async`属性，如下所示：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.5.0/alloy.min.js"></script>
```

## 选项3:使用NPM包

Adobe Experience Platform Web SDK也作为NPM包提供。 [](https://www.npmjs.com) NPM是适用于JavaScript的包管理器。通过安装NPM包，您可以控制Adobe Experience Platform Web SDK JavaScript的构建过程。 NPM包会公开EcmaScript版本5模块或EcmaScript版本2015(ES6)模块，这些模块将在浏览器中运行。

```bash
npm install @adobe/alloy
```

Adobe Experience Platform Web SDK的NPM包会公开`createInstance`函数。 此函数用于创建实例。 传递给函数的名称选项控制日志记录中使用的前缀。 以下是使用包的示例。

### 将包用作ECMAScript 2015(ES6)模块

```javascript
import { createInstance } from "@adobe/alloy";
const alloy = createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

>[!NOTE]
>
>NPM包依赖于CommonJS模块；因此，使用捆绑器时，请确保捆绑器支持CommonJS模块。 某些包程序（如[Rollup](https://rollupjs.org)）需要提供CommonJS支持的[plugin](https://www.npmjs.com/package/@rollup/plugin-commonjs)。

### 将包用作ECMAScript 5模块

```javascript
var alloyLibrary = require("@adobe/alloy");
var alloy = alloyLibrary.createInstance({ name: "alloy" });
alloy("config", { ... });
alloy("sendEvent", { ... });
```

### 支持Internet Explorer

Adobe Experience Platform SDK使用promise，promise是一种通信完成异步任务的方法。 SDK使用的[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)实施本地受除[!DNL Internet Explorer]之外的所有目标浏览器支持。 要在[!DNL Internet Explorer]上使用SDK，您必须具有`window.Promise` [polycilled](https://remysharp.com/2010/10/08/what-is-a-polyfill)。

一个用于polyfill promise的库是promise-polyfill。 有关如何使用NPM进行安装的更多信息，请参阅[promise-polyfill文档](https://www.npmjs.com/package/promise-polyfill)。

>[!NOTE]
>
>如果选择加载其他Promise实施，请确保它支持`Promise.prototype.finally`。

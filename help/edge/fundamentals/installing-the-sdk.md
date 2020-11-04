---
title: 安装Adobe Experience PlatformWeb SDK
seo-title: Adobe Experience PlatformWeb SDK安装SDK
description: 了解如何安装Experience PlatformWeb SDK
seo-description: 了解如何安装Experience PlatformWeb SDK
keywords: web sdk installation;installing web sdk;internet explorer;promise;
translation-type: tm+mt
source-git-commit: d23568f7ce63df5aa98dc237a6671eeadde0c9b2
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 2%

---


# 安装SDK {#installing-the-sdk}

使用Adobe Experience PlatformWeb SDK的首选方式是通过 [Adobe Experience Platform Launch](http://launch.adobe.com/)。 在扩展 `AEP Web SDK` 目录中搜索，安装，然后配置扩展。

CDN中也提供AEP Web SDK，供您使用。 您可以引用此文件或下载此文件并在自己的基础架构上托管它。 它提供微型和非微型版本。 非精简版本有助于进行调试。

URL结构：https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js或alloy.js，用于非微型版本。

例如：

* 缩小： [https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js)
* 未精简： [https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js)

## 添加代码 {#adding-the-code}

实施Adobe Experience Platform的第一步 [!DNL Web SDK] 是尽可能在HTML标签中复制并粘贴以下“基 `<head>` 本代码”:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

基本代码创建一个名为的全局函数 `alloy`。 使用此函数与SDK进行交互。 如果要将全局函数命名为其他名称，可以按如下方 `alloy` 式更改该名称：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

在此示例中，全局函数被重 `mycustomname`命名，而不是 `alloy`重命名。

>[!IMPORTANT]
>
>要避免潜在问题，请使用至少包含一个字符的名称，该字符不是数字，并且与上已找到的属性的名称不冲突 `window`。

除了创建全局函数外，此基本代码还加载包含在服务器上托管的外部文件\(`alloy.js`\)中的其他代码。 默认情况下，此代码以异步方式加载，以使您的网页尽可能高效。 这是建议的实施。

## 支持Internet Explorer {#support-internet-explore}

本SDK利用承诺，即一种通信异步任务完成的方法。 SDK [使用的](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise) Promise实现本机上受所有目标浏览器（除外）支持 [!DNL Internet Explorer]。 要在上使用SDK, [!DNL Internet Explorer]您需要填写多个 `window.Promise` 内 [容](https://remysharp.com/2010/10/08/what-is-a-polyfill)。

要确定您是否已填充 `window.Promise` 填充：

1. 在中打开您的网 [!DNL Internet Explorer]站。
1. 打开浏览器的调试控制台。
1. 在控 `window.Promise` 制台中键入，然后按Enter。

如果出现其他 `undefined` 情况，您可能已经填充 `window.Promise`。 确定是否已填充的 `window.Promise` 另一种方法是在完成上述安装说明后加载您的网站。 如果SDK在提到某些承诺时出错，您可能尚未填写 `window.Promise`。

如果您确定需要填充，请 `window.Promise`在先前提供的基本代码上方包含以下脚本标签：

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

这会加载一个脚本，确保 `window.Promise` 该脚本是有效的Promise实现。

>[!NOTE]
>
>如果选择加载其他承诺实施，请确保它支持 `Promise.prototype.finally`。

## 同步加载JavaScript文件 {#loading-javascript-synchronously}

如添加代码一 [节中所述](#adding-the-code)，您复制并粘贴到网站HTML中的基本代码将加载一个包含其他代码的外部文件。 此附加代码包含SDK的核心功能。 在加载此文件时尝试执行的任何命令都将排队，然后在加载文件后进行处理。 这是最高性能的安装方法。

但是，在某些情况下，您可能希望同步加载文件\（以后将记录有关这些情况的更多详细信息\）。 这样做会阻止浏览器解析和呈现HTML文档的其余部分，直到加载和执行外部文件。 通常不建议在向用户显示主要内容之前再延迟一次，但具体情况会有所不同。

要同步而非异步加载文件，请从第二个标 `async` 签中删除该属 `script` 性，如下所示：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js"></script>
```

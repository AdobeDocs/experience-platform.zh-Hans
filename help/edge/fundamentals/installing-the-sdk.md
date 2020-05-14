---
title: 安装Adobe Experience Platform Web SDK
seo-title: 安装SDK的Adobe Experience Platform Web SDK
description: 了解如何安装Experience Platform Web SDK
seo-description: 了解如何安装Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---


# 安装SDK

实施Adobe Experience Platform Web SDK的第一步是尽可能在HTML标签中复制并粘贴以下“基 `<head>` 本代码”:

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="alloy.js" async></script>
```

基本代码创建一个名为的全局函数 `alloy`。 使用此函数与SDK进行交互。 如果要将全局函数命名为其他名称，可以按如下方 `alloy` 式更改该名称：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="alloy.js" async></script>
```

在此示例中，全局函数被重 `mycustomname`命名，而不是 `alloy`重命名。

>[!IMPORTANT]
>要避免潜在问题，请使用至少包含一个字符的名称，该字符不是数字，并且与上已找到的属性的名称不冲突 `window`。

除了创建全局函数外，此基本代码还加载包含在服务器上托管的外部文件\(`alloy.js`\)中的其他代码。 默认情况下，此代码以异步方式加载，以使您的网页尽可能高效。 这是建议的实施。

## 支持Internet Explorer

本SDK利用承诺，即一种通信异步任务完成的方法。 SDK使 [用的](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) Promise实现本机上受除Internet Explorer以外的所有目标浏览器支持。 要在Internet Explorer上使用SDK，您需要填 `window.Promise` 充 [SDK](https://remysharp.com/2010/10/08/what-is-a-polyfill)。

要确定您是否已填充 `window.Promise` 填充：

1. 在Internet Explorer中打开您的网站。
1. 打开浏览器的调试控制台。
1. 在控 `window.Promise` 制台中键入，然后按Enter。

如果出现其他 `undefined` 情况，您可能已经填充 `window.Promise`。 确定是否已填充的 `window.Promise` 另一种方法是在完成上述安装说明后加载您的网站。 如果SDK在提到某些承诺时出错，您可能尚未填写 `window.Promise`。

如果您确定需要填充，请 `window.Promise`在先前提供的基本代码上方包含以下脚本标签：

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

这会加载一个脚本，确保 `window.Promise` 该脚本是有效的Promise实现。

## 同步加载JavaScript文件

如前所述，您复制并粘贴到网站HTML的基本代码会加载一个包含其他代码的外部文件。 此附加代码包含SDK的核心功能。 在加载此文件时尝试执行的任何命令都将排队，然后在加载文件后进行处理。 这是最高性能的安装方法。

但是，在某些情况下，您可能希望同步加载文件\（以后将记录有关这些情况的更多详细信息\）。 这样做会阻止浏览器解析和呈现HTML文档的其余部分，直到加载和执行外部文件。 通常不建议在向用户显示主要内容之前再延迟一次，但具体情况会有所不同。

要同步而非异步加载文件，请从第二个标 `async` 签中删除该属 `script` 性，如下所示：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="alloy.js"></script>
```

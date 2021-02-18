---
title: 安装Adobe Experience Platform Web SDK
description: 了解如何安装Experience Platform Web SDK。
keywords: web sdk安装；安装web sdk;internet explorer;promise;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 2%

---


# 安装SDK {#installing-the-sdk}

使用Adobe Experience Platform Web SDK的首选方式是通过[Adobe Experience Platform Launch](http://launch.adobe.com/)。 在扩展目录中搜索`AEP Web SDK`，安装，然后配置扩展。

Adobe Experience Platform Web SDK也可在CDN上提供，供您使用。 您可以引用此文件或下载此文件并在自己的基础结构上托管它。 它提供微型和非微型版本。 非微型版本有助于进行调试。

URL结构：https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js或alloy.js，用于非微型版本。

例如：

* 简化：[https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js)
* 未精简：[https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js](https://cdn1.adoberesources.net/alloy/2.3.0/alloy.js)

## 添加代码{#adding-the-code}

实施Adobe Experience Platform [!DNL Web SDK]的第一步是在HTML的`<head>`标签中尽可能高地复制和粘贴以下“基本代码”：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

基本代码创建名为`alloy`的全局函数。 使用此函数与SDK交互。 如果要将全局函数命名为其他名称，可以按如下方式更改`alloy`名称：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js" async></script>
```

在此示例中，全局函数被重命名为`mycustomname`，而不是`alloy`。

>[!IMPORTANT]
>
>要避免潜在问题，请使用至少包含一个字符的名称，该字符不是数字，并且与`window`上已找到的属性的名称不冲突。

此基本代码除了创建全局函数外，还加载包含在服务器上托管的外部文件\(`alloy.js`\)中的其他代码。 默认情况下，此代码以异步方式加载，以使您的网页尽可能高效。 这是建议的实施。

## 支持Internet Explorer {#support-internet-explore}

本SDK利用承诺，这是一种通信异步任务完成的方法。 SDK使用的[Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)实现本机上受除[!DNL Internet Explorer]之外的所有目标浏览器支持。 要在[!DNL Internet Explorer]上使用SDK，您需要`window.Promise` [polyfilled](https://remysharp.com/2010/10/08/what-is-a-polyfill)。

要确定是否已有`window.Promise`填充：

1. 在[!DNL Internet Explorer]中打开您的网站。
1. 打开浏览器的调试控制台。
1. 在控制台中键入`window.Promise` ，然后按Enter。

如果出现`undefined`以外的其他内容，则您可能已经填充了`window.Promise`。 确定`window.Promise`是否已填充的另一种方法是在完成上述安装说明后加载您的网站。 如果SDK引发错误，提及某项承诺，则您可能没有填充`window.Promise`。

如果您确定需要对`window.Promise`进行填充，请在先前提供的基本代码上方包含以下脚本标签：

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

这会加载一个脚本，确保`window.Promise`是有效的Promise实现。

>[!NOTE]
>
>如果选择加载其他Promise实现，请确保它支持`Promise.prototype.finally`。

## 同步加载JavaScript文件{#loading-javascript-synchronously}

如[添加代码](#adding-the-code)部分中所述，您复制并粘贴到网站HTML的基本代码将加载包含其他代码的外部文件。 此附加代码包含SDK的核心功能。 在加载此文件时尝试执行的任何命令都将排队，然后在加载文件后进行处理。 这是最高性能的安装方法。

但是，在某些情况下，您可能希望同步加载文件\（有关这些情况的更多详细信息将在以后记录\）。 这样做会阻止浏览器分析和呈现其余的HTML文档，直到加载和执行外部文件。 通常不建议在向用户显示主要内容之前再延迟一次，但具体情况会有所不同。

要同步加载文件而不是异步加载，请从第二个`script`标签中删除`async`属性，如下所示：

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.3.0/alloy.min.js"></script>
```

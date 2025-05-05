---
title: 实施第三方库
description: 了解在Adobe Experience Platform标记扩展中托管第三方库的各种方法。
exl-id: d8eaf814-cce8-499d-9f02-b2ed3c5ee4d0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 65%

---

# 实施第三方库

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为Adobe Experience Platform中的一套数据收集技术。 因此，产品文档中的术语有一些改动。 有关术语更改的综合参考，请参阅以下[文档](../term-updates.md)。

Adobe Experience Platform中标记扩展的主要用途之一，是让您能够轻松地在网站中实施现有的营销技术（库）。 通过使用扩展，您可以实施由第三方内容交付网络 (CDN) 提供的库，而无需手动编辑网站的 HTML。

有多种方法可以在扩展中托管第三方（供应商）库。 本文档概述了这些不同的实施方法，其中包括每种方法的优点和缺点。

## 先决条件

本文档要求您对标记中的扩展有一定的了解，包括扩展具有什么功能，以及它们是如何构建的。 有关详细信息，请参阅[扩展开发概述](./overview.md)。

## 基础代码加载流程

除了标记的上下文之外，了解营销技术通常在网站上加载的方式非常重要。 第三方库供应商会提供一段代码（称为基础代码），必须将这段代码嵌入到网站的 HTML 中，才能加载库的功能。

通常，当营销技术的基础代码加载到您的网站中时，会执行以下流程中的某个变体：

1. 设置一个可用来与供应商库交互的全局函数。
1. 加载供应商库。
1. 出于配置和跟踪的目的，对全局函数进行一系列有序的初始化调用。

初次设置全局函数时，您仍然可以在库完成加载之前调用该函数。您发出的任何调用都将添加到基础代码的队列机制中，并在库加载后按顺序执行。

在库完成加载后，将会有一个绕过队列的新函数替换该全局函数，并立即处理对该函数的任何后续调用。

### 基础代码示例

以下JavaScript是[Pinterest转换标记](https://developers.pinterest.com/docs/ad-tools/conversion-tag/?)未经简化的基础代码示例，为了演示如何针对标记的各种实施策略调整基础代码，稍后将在本文档中引用这些代码：

```js
!function(scriptUrl) {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = '3.0';
    var scriptElement = document.createElement('script');
    scriptElement.async = true;
    scriptElement.src = scriptUrl;
    var firstScriptElement = 
      document.getElementsByTagName('script')[0];
    firstScriptElement.parentNode.insertBefore(
      scriptElement, firstScriptElement
    );
  }
}('https://s.pinimg.com/ct/core.js');
pintrk('load', 'YOUR_TAG_ID');
pintrk('page');
```

总之，上述基础代码提供了一个[立即调用函数表达式 (IIFE)](https://developer.mozilla.org/en-US/docs/Glossary/IIFE)，该表达式可创建一个全局函数，从而与库 (`window.pintrk`) 进行交互。它还为 `scriptURL` 变量指定了 `https://s.pinimg.com/ct/core.js`（库所在位置）的值。如前所述，在加载库之前调用的任何函数，都将被推送到队列 (`window.pintrk.queue`) 中，以便在库可用时按顺序执行。

当论及如何在站点上加载库时，以下部分的基础代码与之最为相关：

```js
var scriptElement = document.createElement("script");
scriptElement.async = true;
scriptElement.src = scriptUrl;
var firstScriptElement = 
  document.getElementsByTagName("script")[0];
firstScriptElement.parentNode.insertBefore(
  scriptElement, firstScriptElement
);
```

基础代码创建一个脚本元素，将其设置为异步加载，并将 `src` URL 设置为 `https://s.pinimg.com/ct/core.js`。然后，通过将该脚本元素插入到已有的第一个脚本元素之前，将其添加到文档中。

## 标记实施选项

以下各部分演示了在扩展中加载供应商库的不同方式，以前面展示的 Pinterest 基础代码为例。每个示例都涉及为Web扩展[&#128279;](./web/action-types.md)创建一个操作类型，该操作类型将库加载到您的网站上。

>[!NOTE]
>
>虽然以下示例使用操作类型进行演示，但您可以将相同的原则应用于在网站上加载标记库的任何函数。


包含以下方法：

- [实施第三方库](#implementing-third-party-libraries)
   - [先决条件](#prerequisites)
   - [基础代码加载流程](#base-code-loading-process)
      - [基础代码示例](#base-code-example)
   - [标记实施选项](#tags-implementation-options)
      - [运行时从供应商主机加载{#vendor-host}](#load-at-runtime-from-the-vendor-host-vendor-host)
      - [运行时从标记库主机加载](#load-at-runtime-from-the-tag-library-host)
      - [直接嵌入库](#embed-the-library-directly)
   - [后续步骤](#next-steps)

### 运行时从供应商主机加载 {#vendor-host}

供应商库托管最常见的方法是使用供应商的 CDN。由于大多数供应商库的基础代码已配置为从供应商的 CDN 中加载库，为此，您可以将自己的扩展设置为从同一位置加载库。

此方法通常最易于维护，因为扩展会自动加载对CDN上的文件所做的任何更新。

使用此方法时，您只需将全部基础代码直接粘贴到操作类型中，如下所示：

```js
module.exports = function() {
  !function(scriptUrl) {
    if (!window.pintrk) {
      window.pintrk = function() {
        window.pintrk.queue.push(
          Array.prototype.slice.call(arguments)
        );
      };
      window.pintrk.queue = []; 
      window.pintrk.version = "3.0";
      var scriptElement = document.createElement("script");
      scriptElement.async = true;
      scriptElement.src = scriptUrl;
      var firstScriptElement = 
        document.getElementsByTagName("script")[0];
      firstScriptElement.parentNode.insertBefore(
        scriptElement, firstScriptElement
      );
    }
  }("https://s.pinimg.com/ct/core.js");
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

或者，您也可以采取其他步骤来重构此实施。由于变量 `scriptElement` 和 `firstScriptElement` 目前的作用范围仅限于导出的函数，因此可删除 IIFE，原因是这些变量不会产生全局风险。

此外，标记提供了多个[核心模块](./web/core.md)，这些模块是任何扩展都可以使用的实用程序。 具体来说，`@adobe/reactor-load-script` 模块可通过创建脚本元素并将其添加到文档中，从而在远程位置加载脚本。通过将此模块运用于脚本加载流程，您可以进一步重构操作代码：

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = 'https://s.pinimg.com/ct/core.js';
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

### 运行时从标记库主机加载

将供应商 CDN 用于库托管会带来若干风险：CDN 可能会失败，文件可能随时会因为严重错误而更新，或者文件可能因恶意目的而受到破坏。

要解决这些问题，您可以选择将供应商库作为单独的文件，并将其包含在您的扩展中。然后，可以配置扩展，以便该文件与主标记库一起托管。 运行期间，扩展将使用向网站交付主库的同一服务器来加载供应商库。

>[!IMPORTANT]
>
>在某些情况下，供应商库可能会加载来自第三方服务器的其他代码，Pinterest 供应商库的情况就是这样。对于这些情况，若将供应商库与您的扩展捆绑在一起，可能无法完全缓解所有与风险相关的问题。

为了实现上述功能，您必须先将供应商库下载到您的计算机。对于 Pinterest，可在 [https://s.pinimg.com/ct/core.js](https://s.pinimg.com/ct/core.js) 中找到供应商库。下载文件后，您必须将其放入扩展项目中。在以下示例中，该文件名为 `pinterest.js`，且位于项目目录的 `vendor` 文件夹中。

将库文件放入项目中之后，您必须更新[扩展清单](./manifest.md) (`extension.json`)，以指示供应商库应随主标记库一起交付。 这是通过在 `hostedLibFiles` 数组中向库文件添加路径来完成的：

```json
{
  "hostedLibFiles": ["vendor/pinterest.js"]
}
```

最后，必须配置操作代码，以便由托管主库的同一服务器加载供应商库。下面的示例使用[上一部分](#vendor-host)构建的操作代码作为起点。要使用 [turbine 对象](./turbine.md)，您必须传递供应商文件的文件名（不包含任何路径），如下所示：

```js
var loadScript = require('@adobe/reactor-load-script');
var scriptUrl = turbine.getHostedLibFileUrl('pinterest.js');
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    loadScript(scriptUrl);   
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

请务必注意，使用此方法时，每当库在其CDN上更新时，您必须手动更新下载的供应商文件，并将更改发布到扩展的新版本。

### 直接嵌入库

您可以通过直接将供应商库代码嵌入到操作代码本身，来避免完全加载供应商库，这可以有效地使其成为主标记库的一部分。 尽管此方法会增加主库的大小，但是无需另外发出 HTTP 请求以检索单独的文件。

通过将[上一部分](#vendor-host)中构建的操作代码用作起点，您可以用脚本自身的内容替换加载脚本的行：

```js
module.exports = function() {
  if (!window.pintrk) {
    window.pintrk = function() {
      window.pintrk.queue.push(
        Array.prototype.slice.call(arguments)
      );
    };
    window.pintrk.queue = []; 
    window.pintrk.version = "3.0";
    // Paste the full vendor library code here.
  }
  pintrk('load', 'YOUR_TAG_ID');
  pintrk('page');
};
```

## 后续步骤

本文档概述了在标记扩展中托管第三方库的不同方法。 尽管提供的示例侧重于库，但这些技术适用于您的扩展可利用的任何代码段。

请参阅本指南中链接的文档，以了解有关用于配置扩展的工具（包括操作类型、扩展清单、核心模块和 turbine 对象）的更多信息。

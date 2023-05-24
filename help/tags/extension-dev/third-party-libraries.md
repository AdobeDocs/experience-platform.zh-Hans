---
title: 實作協力廠商程式庫
description: 瞭解在Adobe Experience Platform標籤擴充功能中託管協力廠商程式庫的各種方法。
exl-id: d8eaf814-cce8-499d-9f02-b2ed3c5ee4d0
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 68%

---

# 实施第三方库

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../term-updates.md)。

Adobe Experience Platform中標籤擴充功能的主要用途之一，是讓您輕鬆地將現有的行銷技術（程式庫）實作到網站中。 通过使用扩展，您可以实施由第三方内容交付网络 (CDN) 提供的库，而无需手动编辑网站的 HTML。

在擴充功能中託管協力廠商（廠商）程式庫的方法有很多種。 本文档概述了这些不同的实施方法，其中包括每种方法的优点和缺点。

## 先决条件

本檔案需要您實際瞭解標籤內的擴充功能，包括擴充功能的功用和組成方式。 請參閱 [擴充功能開發概觀](./overview.md) 以取得詳細資訊。

## 基础代码加载流程

除了標籤的內容外，瞭解行銷技術一般如何載入網站也很重要。 第三方库供应商会提供一段代码（称为基础代码），必须将这段代码嵌入到网站的 HTML 中，才能加载库的功能。

通常，当营销技术的基础代码加载到您的网站中时，会执行以下流程中的某个变体：

1. 设置一个可用来与供应商库交互的全局函数。
1. 加载供应商库。
1. 出于配置和跟踪的目的，对全局函数进行一系列有序的初始化调用。

初次设置全局函数时，您仍然可以在库完成加载之前调用该函数。您所做的任何呼叫都會新增至基底程式碼的佇列機制，並在程式庫載入後依序執行。

在库完成加载后，将会有一个绕过队列的新函数替换该全局函数，并立即处理对该函数的任何后续调用。

### 基础代码示例

以下JavaScript是以下程式碼未縮制的基底程式碼範例： [pinterest轉換標籤](https://developers.pinterest.com/docs/ad-tools/conversion-tag/?)，本文稍後將參考此內容，示範如何針對標籤的不同實作策略調整基礎程式碼：

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

## 標籤實作選項

以下各部分演示了在扩展中加载供应商库的不同方式，以前面展示的 Pinterest 基础代码为例。這些範例都涉及建立 [Web擴充功能的動作型別](./web/action-types.md) 會在您的網站上載入程式庫。

>[!NOTE]
>
>雖然下列範例是為了示範而使用動作型別，但您可以將相同的原則套用至在網站上載入標籤程式庫的任何函式。


包含以下方法：

- [实施第三方库](#implementing-third-party-libraries)
   - [先决条件](#prerequisites)
   - [基础代码加载流程](#base-code-loading-process)
      - [基础代码示例](#base-code-example)
   - [標籤實作選項](#tags-implementation-options)
      - [运行时从供应商主机加载{#vendor-host}](#load-at-runtime-from-the-vendor-host-vendor-host)
      - [在執行階段從標籤程式庫主機載入](#load-at-runtime-from-the-tag-library-host)
      - [直接嵌入库](#embed-the-library-directly)
   - [后续步骤](#next-steps)

### 运行时从供应商主机加载 {#vendor-host}

供应商库托管最常见的方法是使用供应商的 CDN。由于大多数供应商库的基础代码已配置为从供应商的 CDN 中加载库，为此，您可以将自己的扩展设置为从同一位置加载库。

此方法通常最容易維護，因為擴充功能會自動載入CDN上檔案的任何更新。

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

此外，標籤提供數個 [核心模組](./web/core.md) 任何擴充功能都可使用的公用程式。 具体来说，`@adobe/reactor-load-script` 模块可通过创建脚本元素并将其添加到文档中，从而在远程位置加载脚本。通过将此模块运用于脚本加载流程，您可以进一步重构操作代码：

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

### 在執行階段從標籤程式庫主機載入

将供应商 CDN 用于库托管会带来若干风险：CDN 可能会失败，文件可能随时会因为严重错误而更新，或者文件可能因恶意目的而受到破坏。

要解决这些问题，您可以选择将供应商库作为单独的文件，并将其包含在您的扩展中。接著，您就可以設定擴充功能，讓檔案隨主標籤程式庫一併託管。 运行期间，扩展将使用向网站交付主库的同一服务器来加载供应商库。

>[!IMPORTANT]
>
>在某些情况下，供应商库可能会加载来自第三方服务器的其他代码，Pinterest 供应商库的情况就是这样。对于这些情况，若将供应商库与您的扩展捆绑在一起，可能无法完全缓解所有与风险相关的问题。

为了实现上述功能，您必须先将供应商库下载到您的计算机。对于 Pinterest，可在 [https://s.pinimg.com/ct/core.js](https://s.pinimg.com/ct/core.js) 中找到供应商库。下载文件后，您必须将其放入扩展项目中。在以下示例中，该文件名为 `pinterest.js`，且位于项目目录的 `vendor` 文件夹中。

將程式庫檔案放入專案中後，您必須更新 [擴充功能資訊清單](./manifest.md) (`extension.json`)，表示廠商程式庫應隨主要標籤程式庫一併傳送。 这是通过在 `hostedLibFiles` 数组中向库文件添加路径来完成的：

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

請務必注意，使用此方法時，每當程式庫在其CDN上更新時，您必須手動更新下載的廠商檔案，並發佈擴充功能的新版本變更。

### 直接嵌入库

您可以直接將程式庫程式碼內嵌至動作程式碼本身，略過必須完整載入廠商程式庫的程式，這能有效使其成為主要標籤程式庫的一部分。 尽管此方法会增加主库的大小，但是无需另外发出 HTTP 请求以检索单独的文件。

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

本文概述在標籤擴充功能中託管協力廠商程式庫的各種方法。 尽管提供的示例侧重于库，但这些技术适用于您的扩展可利用的任何代码段。

请参阅本指南中链接的文档，以了解有关用于配置扩展的工具（包括操作类型、扩展清单、核心模块和 turbine 对象）的更多信息。

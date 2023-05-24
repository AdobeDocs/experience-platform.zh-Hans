---
title: 非同步部署
description: 瞭解如何在網站上非同步部署Adobe Experience Platform標籤程式庫。
exl-id: ed117d3a-7370-42aa-9bc9-2a01b8e7794e
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 61%

---

# 异步部署 {#asynchronous-deployment}

>[!CONTEXTUALHELP]
>id="platform_tags_asynchronous_deployment"
>title="异步部署"
>abstract="如果启用此选项，在解析此脚本标记时，浏览器将开始加载 JavaScript 文件，但此时浏览器不是等待加载和执行库，而是将继续解析并渲染文档的其余部分。这可以提高网页性能，并且在涉及某些规则的执行方式时具有重要意义。有关详细信息，请参阅文档。"

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

我們產品所需的JavaScript程式庫的效能與非封鎖部署對Adobe Experience Cloud使用者而言日益重要。 工具如 [[!DNL Google PageSpeed]](https://developers.google.com/speed/pagespeed/insights/) 建議使用者變更在網站上部署Adobe程式庫的方式。 本文說明如何以非同步方式使用AdobeJavaScript程式庫。

## 同步与异步

### 同步部署

通常，库会在页面的 `<head>` 标记中同步加载。例如：

```markup
<script src="example.js"></script>
```

默认情况下，浏览器会解析文档并到达此行，然后开始从服务器获取 JavaScript 文件。接着，浏览器会等待文件返回，然后解析并执行 JavaScript 文件。最后，浏览器会继续解析 HTML 文档的其余部分。

如果解析器在渲染可见内容之前遇到 `<script>` 标记，则内容显示会出现延迟。在向用户显示内容时，如果所加载的 JavaScript 文件并非绝对必需，则不必要求访客等待内容显示。库越大，延迟时间越长。因此，[!DNL Google PageSpeed] 或 [!DNL Lighthouse] 等网站性能基准工具通常会标记同步加载的脚本。

如果您有許多要管理的標籤，標籤管理程式庫可能會快速增大。

### 异步部署

您可以通过向 `<script>` 标记添加 `async` 属性来异步加载任何库。例如：

```markup
<script src="example.js" async></script>
```

这可向浏览器指示，在解析此脚本标记时，浏览器应该开始加载 JavaScript 文件，但此时浏览器不是等待加载和执行库，而是应该继续解析并渲染文档的其余部分。

## 异步部署的注意事项

如上所述，在同步部署中，瀏覽器會在Adobe Experience Platform標籤程式庫載入及執行時，暫停剖析及轉譯頁面。 相反，在异步部署中，浏览器在加载库时会继续解析和渲染页面。標籤程式庫可能在何時完成載入與頁面剖析及轉譯之間相關性的變化，這些都是您必須納入考量的事項。

首先，由於標籤程式庫可能會在頁面底部剖析及執行完之前或之後完成載入，因此您不應再呼叫 `_satellite.pageBottom()` 從您的頁面代碼(`_satellite` 程式庫載入後才能使用)。 詳情請參閱 [非同步載入標籤內嵌程式碼](#loading-the-tags-embed-code-asynchronously).

其次，標籤程式庫可在 [`DOMContentLoaded`](https://developer.mozilla.org/zh-CN/docs/Web/Events/DOMContentLoaded) 瀏覽器事件（DOM就緒）已發生。

由於這兩點，值得說明的是 [程式庫已載入](../../extensions/client/core/overview.md#library-loaded-page-top)， [頁面底部](../../extensions/client/core/overview.md#page-bottom)， [DOM已就緒](../../extensions/client/core/overview.md#page-bottom)、和 [視窗已載入](../../extensions/client/core/overview.md#window-loaded) 非同步載入標籤程式庫時，核心擴充功能中的事件型別。

如果您的標籤屬性包含下列四個規則：

* 规则 A：使用 Library Loaded 事件类型
* 规则 B：使用 Page Bottom 事件类型
* 规则 C：使用 DOM Ready 事件类型
* 规则 D：使用 Window Loaded 事件类型

無論標籤程式庫何時完成載入，所有規則必定都會執行，而且會依下列順序執行：

规则 A → 规则 B → 规则 C → 规则 D

雖然順序一律會強制執行，有些規則可能會在標籤程式庫完成載入時立即執行，而有些可能會稍後執行。 標籤程式庫完成載入時，會發生下列情況：

1. 立即执行规则 A。
1. 如果 `DOMContentLoaded` 浏览器事件 (DOM Ready) 已经发生，则会立即执行规则 B 和规则 C。否则，规则 B 和规则 C 稍后在发生 [`DOMContentLoaded`](https://developer.mozilla.org/zh-CN/docs/Web/Events/DOMContentLoaded) 浏览器事件时执行。
1. 如果已发生 [`load`](https://developer.mozilla.org/zh-CN/docs/Web/Events/load) 浏览器事件（已加载窗口），则会立即执行规则 D。否则，将在稍后发生 [`load`](https://developer.mozilla.org/zh-CN/docs/Web/Events/load) 浏览器事件时执行规则 D。請注意，如果您已根據指示安裝標籤庫，則標籤庫 *一律* 完成載入 [`load`](https://developer.mozilla.org/zh-CN/docs/Web/Events/load) 發生瀏覽器事件。

将这些原则应用于您自己的网站时，请考虑以下事项：

* **使用 Library Loaded 事件类型的规则可能会在数据层完全加载之前执行。**&#x200B;这可能会导致执行规则的操作时缺少数据，因为页面上尚未提供数据。调整规则配置可减少这类问题。例如，您可以在数据层完成加载后立即使用由页面代码触发的 Custom Event 或 Direct Call 事件类型，而不是使用由 Library Loaded 事件类型触发的规则。
* **异步加载库时，Page Bottom 事件类型不会特别提供值。**&#x200B;请改为考虑使用 Library Loaded、DOM Ready、Window Loaded 或其他事件类型。

如果您发现这些事件发生的顺序混乱，则可能需要处理一些计时问题。在进行需要精确计时的部署时，可能需要使用事件侦听器和 Custom Event 或 Direct Call 事件类型以确保进行更可靠且一致的实施。

## 非同步載入標籤內嵌程式碼

當您設定時，標籤會在建立內嵌程式碼時提供開啟非同步載入的切換按鈕 [環境](../publishing/environments.md). 您还可以自行配置异步加载：

1. 向 `<script>` 标记中添加 async 属性以异步加载脚本。

   對於標籤內嵌程式碼，這表示會將這個變更為：

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js"></script>
   ```

   更改为以下内容：

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js" async></script>
   ```

1. 移除您之前可能在标记底部添加的任何代码：

   ```markup
   <script type="text/javascript">_satellite.pageBottom();</script>
   ```

   此程式碼會通知Platform瀏覽器剖析器已到達頁面底部。 標籤可能在此時間之前尚未載入及執行，因此呼叫 `_satellite.pageBottom()` 會導致錯誤，且Page Bottom事件型別可能不會如預期般運作。

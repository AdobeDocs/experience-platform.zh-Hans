---
title: Asynchronous Deployment
description: Learn how to asynchronously deploy Adobe Experience Platform tag libraries on your website.
exl-id: ed117d3a-7370-42aa-9bc9-2a01b8e7794e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 60%

---

# 异步部署 {#asynchronous-deployment}

>[!CONTEXTUALHELP]
>id="platform_tags_asynchronous_deployment"
>title="异步部署"
>abstract="如果启用此选项，在解析此脚本标记时，浏览器将开始加载 JavaScript 文件，但此时浏览器不是等待加载和执行库，而是将继续解析并渲染文档的其余部分。这可以提高网页性能，并且在涉及某些规则的执行方式时具有重要意义。有关详细信息，请参阅文档。"

>[!NOTE]
>
>经过品牌重塑，Adobe Experience Platform Launch 已变为 Adobe Experience Platform 中的一套数据收集技术。因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

Performance and non-blocking deployment of the JavaScript libraries required by our products is increasingly important to Adobe Experience Cloud users. Tools like [[!DNL Google PageSpeed]](https://developers.google.com/speed/pagespeed/insights/) recommend that users change they way they deploy the Adobe libraries on their site. This article explains how to use the Adobe JavaScript libraries in an asynchronous fashion.

## 同步与异步

### 同步部署

通常，库会在页面的 `<head>` 标记中同步加载。例如：

```markup
<script src="example.js"></script>
```

默认情况下，浏览器会解析文档并到达此行，然后开始从服务器获取 JavaScript 文件。接着，浏览器会等待文件返回，然后解析并执行 JavaScript 文件。最后，浏览器会继续解析 HTML 文档的其余部分。

如果解析器在渲染可见内容之前遇到 `<script>` 标记，则内容显示会出现延迟。在向用户显示内容时，如果所加载的 JavaScript 文件并非绝对必需，则不必要求访客等待内容显示。库越大，延迟时间越长。因此，[!DNL Google PageSpeed] 或 [!DNL Lighthouse] 等网站性能基准工具通常会标记同步加载的脚本。

Tag management libraries can quickly grow large if you have a lot of tags to manage.

### 异步部署

You can load any library asynchronously by adding an `async` attribute to the `<script>` tag. 例如：

```markup
<script src="example.js" async></script>
```

这可向浏览器指示，在解析此脚本标记时，浏览器应该开始加载 JavaScript 文件，但此时浏览器不是等待加载和执行库，而是应该继续解析并渲染文档的其余部分。

## 异步部署的注意事项

As described above, in synchronous deployments, the browser pauses parsing and rendering the page while the Adobe Experience Platform tag library is loaded and executed. 相反，在异步部署中，浏览器在加载库时会继续解析和渲染页面。The variability of when the tag library might finish loading in relation to page parsing and rendering must be taken into consideration.

First, because the tag library can finish loading before or after the bottom of the page has been parsed and executed, you should no longer call `_satellite.pageBottom()` from your page code (`_satellite` won&#39;t be available until after the library has loaded). This is explained in [Loading the tags embed code asynchronously](#loading-the-tags-embed-code-asynchronously).

Second, the tag library can finish loading before or after the [`DOMContentLoaded`](https://developer.mozilla.org/zh-CN/docs/Web/Events/DOMContentLoaded) browser event (DOM Ready) has occurred.

Because of these two points, it&#39;s worth demonstrating how the [Library Loaded](../../extensions/client/core/overview.md#library-loaded-page-top), [Page Bottom](../../extensions/client/core/overview.md#page-bottom), [DOM Ready](../../extensions/client/core/overview.md#page-bottom), and [Window Loaded](../../extensions/client/core/overview.md#window-loaded) event types from the Core extension function when loading a tag library asynchronously.

If your tag property contains the following four rules:

* 规则 A：使用 Library Loaded 事件类型
* 规则 B：使用 Page Bottom 事件类型
* 规则 C：使用 DOM Ready 事件类型
* 规则 D：使用 Window Loaded 事件类型

Regardless of when the tag library finishes loading, all the rules are guaranteed to be executed and they will be executed in the following order:

规则 A → 规则 B → 规则 C → 规则 D

Although the order is always enforced, some rules might be executed immediately when the tag library finishes loading, while others might be executed later. The following occurs when the tag library finishes loading:

1. 立即执行规则 A。
1. 如果 `DOMContentLoaded` 浏览器事件 (DOM Ready) 已经发生，则会立即执行规则 B 和规则 C。否则，规则 B 和规则 C 稍后在发生 [`DOMContentLoaded`](https://developer.mozilla.org/zh-CN/docs/Web/Events/DOMContentLoaded) 浏览器事件时执行。
1. 如果已发生 [`load`](https://developer.mozilla.org/zh-CN/docs/Web/Events/load) 浏览器事件（已加载窗口），则会立即执行规则 D。否则，将在稍后发生 [`load`](https://developer.mozilla.org/zh-CN/docs/Web/Events/load) 浏览器事件时执行规则 D。Note that if you&#39;ve installed the tag library according to the instructions, the tag library *always* finishes loading before the [`load`](https://developer.mozilla.org/zh-CN/docs/Web/Events/load) browser event occurs.

将这些原则应用于您自己的网站时，请考虑以下事项：

* **使用 Library Loaded 事件类型的规则可能会在数据层完全加载之前执行。**&#x200B;这可能会导致执行规则的操作时缺少数据，因为页面上尚未提供数据。调整规则配置可减少这类问题。例如，您可以在数据层完成加载后立即使用由页面代码触发的 Custom Event 或 Direct Call 事件类型，而不是使用由 Library Loaded 事件类型触发的规则。
* **异步加载库时，Page Bottom 事件类型不会特别提供值。**&#x200B;请改为考虑使用 Library Loaded、DOM Ready、Window Loaded 或其他事件类型。

如果您发现这些事件发生的顺序混乱，则可能需要处理一些计时问题。在进行需要精确计时的部署时，可能需要使用事件侦听器和 Custom Event 或 Direct Call 事件类型以确保进行更可靠且一致的实施。

## Loading the tags embed code asynchronously

Tags provide a toggle to turn on asynchronous loading when creating an embed code when you configure an [environment](../publishing/environments.md). 您还可以自行配置异步加载：

1. 向 `<script>` 标记中添加 async 属性以异步加载脚本。

   For the tags embed code, that means changing this:

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

   This code tells Experience Platform that the browser parser has reached the bottom of the page. It is likely that tags will not have loaded and executed before this time, therefore calling `_satellite.pageBottom()` results in an error and the Page Bottom event type may not behave as expected.

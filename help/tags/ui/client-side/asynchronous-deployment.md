---
title: 异步部署
description: 了解如何在您的网站上异步部署Adobe Experience Platform标记库。
exl-id: ed117d3a-7370-42aa-9bc9-2a01b8e7794e
source-git-commit: c314cba6b822e12aa0367e1377ceb4f6c9d07ac2
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 55%

---

# 异步部署 {#asynchronous-deployment}

>[!CONTEXTUALHELP]
>id="platform_tags_asynchronous_deployment"
>title="异步部署"
>abstract="如果启用此选项，则在解析此脚本标记后，浏览器将开始加载JavaScript文件，但是，它将继续解析并渲染文档的其余部分，而不是等待库的加载和执行。 这可以提高网页性能，但对于如何执行某些规则具有重要影响。 有关详细信息，请参阅文档。"

>[!NOTE]
>
>Adobe Experience Platform Launch已在Adobe Experience Platform中重新命名为一套数据收集技术。 因此，产品文档中的术语有一些改动。有关术语更改的综合参考，请参阅以下[文档](../../term-updates.md)。

我们的产品需要提高JavaScript库的性能和对其进行无阻塞部署，这对Adobe Experience Cloud用户来说越来越重要。 诸如 [[!DNL Google PageSpeed]](https://developers.google.com/speed/pagespeed/insights/) 建议用户更改在其网站上部署Adobe库的方式。 本文介绍如何以异步方式使用AdobeJavaScript库。

## 同步与异步

### 同步部署

通常，库会在页面的 `<head>` 标记中同步加载。例如：

```markup
<script src="example.js"></script>
```

默认情况下，浏览器会解析文档并到达此行，然后开始从服务器获取 JavaScript 文件。接着，浏览器会等待文件返回，然后解析并执行 JavaScript 文件。最后，浏览器会继续解析 HTML 文档的其余部分。

如果解析器在渲染可见内容之前遇到 `<script>` 标记，则内容显示会出现延迟。在向用户显示内容时，如果所加载的 JavaScript 文件并非绝对必需，则不必要求访客等待内容显示。库越大，延迟时间越长。因此，[!DNL Google PageSpeed] 或 [!DNL Lighthouse] 等网站性能基准工具通常会标记同步加载的脚本。

如果您要管理大量标记，则标签管理库会快速增大。

### 异步部署

您可以通过向 `<script>` 标记添加 `async` 属性来异步加载任何库。例如：

```markup
<script src="example.js" async></script>
```

这可向浏览器指示，在解析此脚本标记时，浏览器应该开始加载 JavaScript 文件，但此时浏览器不是等待加载和执行库，而是应该继续解析并渲染文档的其余部分。

## 异步部署的注意事项

如上所述，在同步部署中，浏览器在加载和执行Adobe Experience Platform标记库时会暂停解析和渲染页面。 相反，在异步部署中，浏览器在加载库时会继续解析和渲染页面。必须考虑标记库可能完成加载的时间相对于页面解析和渲染的可变性。

首先，由于标记库可以在解析并执行页面底部之前或之后完成加载，因此您不应再调用 `_satellite.pageBottom()` 从页面代码(`_satellite` 在库加载后才可用)。 这在 [异步加载标记嵌入代码](#loading-the-tags-embed-code-asynchronously).

其次，标记库可以在 [`DOMContentLoaded`](https://developer.mozilla.org/zh-CN/docs/Web/Events/DOMContentLoaded) 发生浏览器事件（DOM就绪）。

由于这两点，因此，有必要展示 [Library Loaded](../../extensions/web/core/overview.md#library-loaded-page-top), [Page Bottom](../../extensions/web/core/overview.md#page-bottom), [DOM Ready](../../extensions/web/core/overview.md#page-bottom)和 [Window Loaded](../../extensions/web/core/overview.md#window-loaded) 异步加载标记库时，核心扩展中的事件类型会起作用。

如果您的标记属性包含以下四个规则：

* 规则 A：使用 Library Loaded 事件类型
* 规则 B：使用 Page Bottom 事件类型
* 规则 C：使用 DOM Ready 事件类型
* 规则 D：使用 Window Loaded 事件类型

无论标记库何时完成加载，都会保证执行所有规则，并且这些规则将按以下顺序执行：

规则 A → 规则 B → 规则 C → 规则 D

尽管始终强制按此顺序执行，但某些规则可能会在标记库完成加载时立即执行，而其他规则可能会在稍后执行。 标记库完成加载时会发生以下情况：

1. 立即执行规则 A。
1. 如果 `DOMContentLoaded` 浏览器事件 (DOM Ready) 已经发生，则会立即执行规则 B 和规则 C。否则，规则 B 和规则 C 稍后在发生 [`DOMContentLoaded`](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded) 浏览器事件时执行。
1. 如果已发生 [`load`](https://developer.mozilla.org/zh-CN/docs/Web/Events/load) 浏览器事件（已加载窗口），则会立即执行规则 D。否则，将在稍后发生 [`load`](https://developer.mozilla.org/en-US/docs/Web/Events/load) 浏览器事件时执行规则 D。请注意，如果您已按照相关说明安装了标签库，则标记库 *always* 完成加载 [`load`](https://developer.mozilla.org/en-US/docs/Web/Events/load) 发生浏览器事件。

将这些原则应用于您自己的网站时，请考虑以下事项：

* **使用 Library Loaded 事件类型的规则可能会在数据层完全加载之前执行。**&#x200B;这可能会导致执行规则的操作时缺少数据，因为页面上尚未提供数据。调整规则配置可减少这类问题。例如，您可以在数据层完成加载后立即使用由页面代码触发的 Custom Event 或 Direct Call 事件类型，而不是使用由 Library Loaded 事件类型触发的规则。
* **异步加载库时，Page Bottom 事件类型不会特别提供值。**&#x200B;请改为考虑使用 Library Loaded、DOM Ready、Window Loaded 或其他事件类型。

如果您发现这些事件发生的顺序混乱，则可能需要处理一些计时问题。在进行需要精确计时的部署时，可能需要使用事件侦听器和 Custom Event 或 Direct Call 事件类型以确保进行更可靠且一致的实施。

## 异步加载标记嵌入代码

当您配置 [环境](../publishing/environments.md). 您还可以自行配置异步加载：

1. 向 `<script>` 标记中添加 async 属性以异步加载脚本。

   对于标记嵌入代码，这表示将以下内容：

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

   此代码用于告知Platform浏览器解析器已到达页面底部。 此前可能未加载和执行标记，因此调用 `_satellite.pageBottom()` 会导致错误，并且Page Bottom事件类型可能无法按预期运行。

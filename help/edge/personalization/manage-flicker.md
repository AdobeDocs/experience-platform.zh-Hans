---
title: 使用Adobe Experience Platform Web SDK管理个性化体验的闪烁
description: 了解如何使用Adobe Experience Platform Web SDK管理用户体验上的闪烁。
keywords: target；闪烁；预隐藏Style；异步；异步；
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: e5d279397cab30e997103496beda5265520dca77
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# 管理闪烁

在尝试渲染个性化内容时，SDK必须确保没有闪烁。 闪烁，也称为FOOC(原始内容的Flash)，是指在测试/个性化期间出现替代内容之前，先短暂显示原始内容。 SDK会尝试将CSS样式应用于页面的元素，以确保这些元素在成功呈现个性化内容之前处于隐藏状态。

闪烁管理功能包含几个阶段：

1. 预隐藏
1. 预处理
1. 渲染

## 预隐藏

在预隐藏阶段，SDK使用 `prehidingStyle` 配置选项，用于创建HTML样式标记并将其附加到DOM以确保隐藏页面的大部分内容。 如果您不确定页面的哪些部分将被个性化，建议设置 `prehidingStyle` 到 `body { opacity: 0 !important }`. 这可确保隐藏整个页面。 但是，这有一个缺点，即会导致由Lighthouse、网页测试等工具报告的页面渲染性能变差。 要获得最佳的页面渲染性能，建议设置 `prehidingStyle` 到容器元素列表，其中包含将个性化的页面部分。

假设您有一个类似于下面的HTML页，并且您只知道 `bar` 和 `bazz` 容器元素将永远不会进行个性化：

```html
<html>
  <head>
  </head>
  <body>
    <div id="foo">
      Foo foo foo
    </div>

    <div id="bar">
      Bar bar bar
    </div>

    <div id="bazz">
      Bazz bazz bazz
    </div>
  </body>
</html>
```

然后 `prehidingStyle` 应设置为如下内容 `#bar, #bazz { opacity: 0 !important }`.

## 预处理

一旦SDK从服务器收到个性化内容，预处理阶段就会开始。 在此阶段，将预处理响应，确保隐藏必须包含个性化内容的元素。 HTML隐藏这些元素后，已根据 `prehidingStyle` 配置选项将被删除，并显示HTML正文或隐藏的容器元素。

## 渲染

成功呈现所有个性化内容后，或者出现任何错误后，将显示所有以前隐藏的元素，以确保页面上没有被SDK隐藏的隐藏元素。

## 异步加载SDK时管理闪烁

建议始终异步加载SDK以获得最佳页面渲染性能。 但是，这对个性化内容的呈现有一些影响。 异步加载SDK时，需要使用预隐藏代码片段。 必须在“HTML”页面的SDK之前添加预隐藏代码片段。 以下是隐藏整个主体的示例代码片段：

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

为了确保HTML正文或容器元素不会长时间隐藏，预隐藏代码片段使用计时器，默认情况下，该计时器会删除之后的代码片段 `3000` 毫秒。 此 `3000` 毫秒是最长等待时间。 如果更快地收到并处理了来自服务器的响应，则会尽快删除预隐藏HTML样式标记。

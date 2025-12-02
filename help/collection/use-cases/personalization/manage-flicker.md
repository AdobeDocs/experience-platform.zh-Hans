---
title: 使用Adobe Experience Platform Web SDK管理个性化体验的闪烁
description: 了解如何使用Adobe Experience Platform Web SDK管理用户体验上的闪烁。
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# 管理闪烁

在尝试呈现个性化内容时，SDK必须确保不会出现闪烁。 闪烁，也称为FOOC（原始内容的闪烁），是指在测试/个性化期间出现替代内容之前，先短暂显示原始内容。 SDK会尝试将CSS样式应用于页面的元素，以确保这些元素在成功呈现个性化内容之前处于隐藏状态。

管理闪烁的方式取决于您是以同步还是异步方式部署Web SDK。 检查部署`<head>`或标记加载器的`alloy.js`标记。 `async`标记中是否存在`<script>`属性决定了Web SDK是否异步加载。

```html
<!-- This tag loads synchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js"></script>

<!-- This tag loads asynchronously -->
<script src="https://assets.adobedtm.com/[...]/launch-example.min.js" async></script>

<!-- This library loads synchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js"></script>

<!-- This library loads asynchronously -->
<script src="https://cdn1.adoberesources.net/alloy/2.14.0/alloy.min.js" async></script>
```

## 管理同步部署的闪烁

同步闪烁管理分为三个阶段：

1. 预隐藏
1. 预处理
1. 渲染

在&#x200B;**预隐藏阶段**&#x200B;期间，SDK使用[`prehidingStyle`](../../js/commands/configure/prehidingstyle.md)配置属性创建HTML样式标记，并将其附加到DOM以确保隐藏页面的所需部分。 如果您不确定页面的哪些部分将个性化，建议将`prehidingStyle`设置为`body { opacity: 0 !important }`。 这可确保隐藏整个页面。 但是，这有一个缺点，即会导致Lighthouse、Web页面测试等工具报告的页面渲染性能不佳。 要获得最佳的页面渲染性能，建议将`prehidingStyle`设置为包含将个性化的页面部分的容器元素列表。

假设您有一个与以下页面类似的HTML页面，并且您知道只有`bar`和`bazz`容器元素永远是个性化的：

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

则`prehidingStyle`应设置为`#bar, #bazz { opacity: 0 !important }`之类的内容。

当SDK收到来自服务器的个性化内容后，**预处理阶段**&#x200B;开始。 在此阶段中，将预处理响应，确保隐藏必须包含个性化内容的元素。 隐藏这些元素后，将删除根据`prehidingStyle`配置选项创建的HTML样式标记，并显示HTML正文或隐藏的容器元素。

成功呈现所有个性化内容后，或者如果发生任何错误，**呈现阶段**&#x200B;开始。 将显示所有以前隐藏的元素，以确保页面上没有被SDK隐藏的隐藏元素。

## 管理异步部署的闪烁

建议始终异步加载SDK以获取最佳页面渲染性能。 但是，这对个性化内容的呈现有一些影响。 异步加载SDK时，需要使用预隐藏代码片段。 必须在HTML页面的SDK之前添加预隐藏代码片段。 以下是隐藏整个主体的示例代码片段：

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

为了确保HTML正文或容器元素不会长时间隐藏，预隐藏代码片段使用计时器，默认情况下，该计时器会在`3000`毫秒后删除代码片段。 `3000`毫秒是最长等待时间。 如果更快地收到并处理了来自服务器的响应，则会尽快删除预隐藏HTML样式标记。

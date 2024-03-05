---
title: 使用Adobe Experience Platform Web SDK管理个性化体验的闪烁
description: 了解如何使用Adobe Experience Platform Web SDK管理用户体验上的闪烁。
keywords: target；闪烁；预隐藏Style；异步；异步；
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# 管理闪烁

在尝试呈现个性化内容时，SDK必须确保不会出现闪烁。 闪烁，也称为FOOC(原始内容的Flash)，是指在测试/个性化期间短暂显示原始内容之前出现替代内容时。 SDK会尝试将CSS样式应用于页面的元素，以确保这些元素在成功呈现个性化内容之前处于隐藏状态。

管理闪烁的方式取决于您是同步还是异步部署Web SDK。 查看 `<head>` 标记您部署的位置 `alloy.js` 或标记加载器。 存在 `async` 中的属性 `<script>` 标记可确定Web SDK是否以异步方式加载。

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

时段 **预隐藏阶段**，SDK使用 [`prehidingStyle`](../commands/configure/prehidingstyle.md) configuration属性，用于创建HTML样式标记并将其附加到DOM以确保隐藏页面的所需部分。 如果您不确定将个性化的页面部分，建议设置 `prehidingStyle` 到 `body { opacity: 0 !important }`. 这可确保隐藏整个页面。 但是，这有一个缺点，即会导致Lighthouse、Web页面测试等工具报告的页面渲染性能不佳。 要获得最佳的页面渲染性能，建议设置 `prehidingStyle` 到容器元素列表，其中包含将个性化的页面部分。

假设您有一个类似于下面的HTML页面，并且您只知道 `bar` 和 `bazz` 容器元素将始终进行个性化：

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

然后 `prehidingStyle` 应该设置为如下内容 `#bar, #bazz { opacity: 0 !important }`.

在SDK收到来自服务器的个性化内容后， **预处理阶段** 开始。 在此阶段中，将预处理响应，确保隐藏必须包含个性化内容的元素。 HTML隐藏这些元素后，将根据 `prehidingStyle` 删除了配置选项，并显示了HTML正文或隐藏的容器元素。

成功呈现所有个性化内容后，或者如果有任何错误，则 **渲染阶段** 开始。 将显示所有以前隐藏的元素，以确保页面上没有被SDK隐藏的隐藏元素。

## 管理异步部署的闪烁

建议始终异步加载SDK以获取最佳页面渲染性能。 但是，这对个性化内容的呈现有一些影响。 异步加载SDK时，需要使用预隐藏代码片段。 必须在HTML页面中的SDK之前添加预隐藏代码片段。 以下是隐藏整个主体的示例代码片段：

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

为了确保HTML正文或容器元素不会长时间隐藏，预隐藏代码片段将使用计时器，默认情况下，该计时器将在以下时间之后删除代码片段 `3000` 毫秒。 此 `3000` 毫秒是最长等待时间。 如果更快地收到并处理了来自服务器的响应，则会尽快删除预隐藏HTML样式标记。

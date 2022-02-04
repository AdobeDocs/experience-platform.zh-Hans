---
title: 使用Adobe Experience Platform Web SDK管理闪烁以提供个性化体验
description: 了解如何使用Adobe Experience Platform Web SDK管理用户体验中的闪烁。
keywords: target；闪烁；预隐藏Style；异步；
exl-id: f4b59109-df7c-471b-9bd6-7082e00c293b
source-git-commit: e5d279397cab30e997103496beda5265520dca77
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# 管理闪烁

在尝试渲染个性化内容时，SDK必须确保不会出现闪烁。 闪烁，也称为FOOC(原始内容的Flash)，即在测试/个性化期间，在替代内容显示之前短暂显示原始内容时。 SDK会尝试将CSS样式应用于页面的元素，以确保在个性化内容成功呈现之前隐藏这些元素。

闪烁管理功能有几个阶段：

1. 预隐藏
1. 预处理
1. 渲染

## 预隐藏

在预隐藏阶段，SDK会使用 `prehidingStyle` 配置选项来创建HTML样式标记并将其附加到DOM中，以确保隐藏页面的大部分。 如果您不确定将对页面的哪些部分进行个性化，建议设置 `prehidingStyle` to `body { opacity: 0 !important }`. 这可确保隐藏整个页面。 但是，这会导致由Lighthouse、Web页面测试等工具报告的页面渲染性能下降，从而带来负面影响。 要获得最佳页面渲染性能，建议设置 `prehidingStyle` 到包含将进行个性化的页面部分的容器元素列表。

假设您有一个类似于下面的HTML页面，并且您只知道 `bar` 和 `bazz` 容器元素将永远进行个性化：

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

然后， `prehidingStyle` 应该设置为类似的 `#bar, #bazz { opacity: 0 !important }`.

## 预处理

SDK从服务器收到个性化内容后，将开始预处理阶段。 在此阶段，将预处理响应，确保隐藏必须包含个性化内容的元素。 隐藏这些元素后，将根据 `prehidingStyle` 配置选项，此时会显示HTML主体或隐藏的容器元素。

## 渲染

成功渲染所有个性化内容后，或者如果出现任何错误，则会显示之前隐藏的所有元素，以确保页面上没有SDK隐藏的隐藏元素。

## 异步加载SDK时管理闪烁

建议始终异步加载SDK以获得最佳页面渲染性能。 但是，这对呈现个性化内容有一定的影响。 异步加载SDK时，需要使用预隐藏代码片段。 必须先添加预隐藏代码片段，然后再在HTML页面的SDK中添加。 以下是隐藏整个正文的示例代码片段：

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

为确保HTML正文或容器元素在较长的时间段内未隐藏，预隐藏代码片段使用的计时器默认会在 `3000` 毫秒。 的 `3000` 毫秒是最长等待时间。 如果已先收到并处理来自服务器的响应，则会尽快删除预隐藏HTML样式标记。

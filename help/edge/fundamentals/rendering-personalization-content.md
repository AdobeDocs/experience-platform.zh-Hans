---
title: 呈现个性化内容
seo-title: Adobe Experience Platform Web SDK呈现个性化内容
description: 了解如何使用Experience Platform Web SDK呈现个性化内容
seo-description: 了解如何使用Experience Platform Web SDK呈现个性化内容
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# （测试版）呈现个性化内容

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前为测试版，并非所有用户都可用。 文档和功能可能会发生更改。

当您将活动发送到服务器并设置为该活动的选项时，SDK会 `viewStart` 自动 `true` 呈现个性化内容。

```javascript
alloy("event", {
  "viewStart": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

个性化内容的呈现是异步的，因此当特定内容片段是页面的一部分时，不应存在任何假设。

## 管理闪烁

在尝试呈现个性化内容时，SDK必须确保不会闪烁。 Flicker也称为FOOC（原始内容的Flash），是指在测试或个性化过程中，在替代内容出现之前，原始内容被短暂显示。 SDK会尝试将CSS样式应用于页面的元素，以确保这些元素在成功呈现个性化内容之前处于隐藏状态。

闪烁管理功能有几个阶段：

1. 预隐藏
1. 预处理
1. 渲染

### 预隐藏

在预隐藏阶段，SDK使用配置选项创建HTML样式标签并将其附加到DOM中，以确保隐藏页面的大部分。 `prehidingStyle` 如果您不确定页面的哪些部分将进行个性化，则建议将其设置为 `prehidingStyle``body { opacity: 0 !important }`。 这可确保整个页面处于隐藏状态。 但是，这会导致由Lighthouse、Web页测试等工具报告的页面渲染性能下降。 要获得最佳页面渲染性能，建议将其设置 `prehidingStyle` 为包含将个性化页面部分的容器元素列表。

假设您有如下HTML页面，并且您知道只有和容器元 `bar` 素 `bazz` 将永远是个性化的：

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

那就 `prehidingStyle` 应该设成这样 `#bar, #bazz { opacity: 0 !important }`.

### 预处理

SDK从服务器收到个性化内容后，预处理阶段开始。 在此阶段，将预先处理响应，确保必须包含个性化内容的元素处于隐藏状态。 隐藏这些元素后，将删除根据配置选项创建的HTML样式标签，并显示 `prehidingStyle` HTML正文或隐藏的容器元素。

### 渲染

在成功呈现所有个性化内容后，或者如果出现任何错误，将显示所有以前隐藏的元素，以确保页面上没有SDK隐藏的隐藏元素。

## 异步加载SDK时管理闪烁

建议始终异步加载SDK以获得最佳页面呈现性能。 但是，这对呈现个性化内容有一定的影响。 当异步加载SDK时，需要使用预隐藏代码片断。 必须在HTML页中的SDK之前添加预隐藏代码片断。 以下是隐藏整个正文的示例代码片断：

```html
<script>
  !function(e,a,n,t){
    if (a) return;
    var i=e.head;if(i){
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
    setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

要确保HTML正文或容器元素在较长的时间段内不隐藏，预隐藏代码片段使用计时器，默认情况下，该计时器会在毫秒后删除代 `3000` 码片段。 毫秒 `3000` 是最长等待时间。 如果服务器响应已经收到并且处理得更快，则会尽快删除预隐藏的HTML样式标记。

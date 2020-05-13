---
source-git-commit: e00dc3e8dec0117617081ca4fc9ffa752b01b3b7
workflow-type: tm+mt
translation-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---
# 管理闪烁

在尝试呈现个性化内容时，SDK必须确保不会闪烁。 Flicker也称为FOOC（原始内容的Flash），是指在测试／个性化过程中，在替代内容出现之前短暂显示原始内容。 SDK会尝试将CSS样式应用于页面的元素，以确保这些元素在个性化内容成功呈现之前处于隐藏状态。

闪变管理功能有几个阶段：

1. 预隐藏
1. 预处理
1. 渲染

## 预隐藏

在预隐藏阶段，SDK使用 `prehidingStyle` 配置选项创建HTML样式标签并将其追加到DOM，以确保页面的大部分处于隐藏状态。 如果您不确定页面的哪些部分将进行个性化，建议将其设 `prehidingStyle` 置为 `body { opacity: 0 !important }`。 这可确保整个页面处于隐藏状态。 但是，这会导致由Lighthouse、Web页测试等工具报告的页面渲染性能下降。 要获得最佳页面渲染性能，建议将其 `prehidingStyle` 设置为列表容器元素，这些元素包含将要个性化的页面部分。

假定您有如下HTML页面，并且您知道只有和 `bar` 容器 `bazz` 元素将永远是个性化的：

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

那就 `prehidingStyle` 应该设定成这样 `#bar, #bazz { opacity: 0 !important }`。

## 预处理

SDK从服务器收到个性化内容后，预处理阶段即开始。 在此阶段，将预先处理响应，确保隐藏必须包含个性化内容的元素。 隐藏这些元素后，将删除根据配置选项创建的 `prehidingStyle` HTML样式标签，并显示HTML正文或隐藏的容器元素。

## 渲染

在所有个性化内容均成功呈现后，或者如果出现任何错误，则会显示所有以前隐藏的元素，以确保页面上没有SDK隐藏的隐藏元素。

## 异步加载SDK时管理闪烁

建议始终异步加载SDK以获得最佳页面渲染性能。 但是，这对个性化内容的呈现有一定的影响。 异步加载SDK时，需要使用预隐藏代码片段。 必须在HTML页中的SDK之前添加预隐藏代码片段。 以下是隐藏整个正文的示例片段：

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

为确保HTML正文或容器元素在较长的时间段内未隐藏，预隐藏代码片段使用计时器，默认情况下，该计时器会在毫秒后删除该代 `3000` 码片段。 毫 `3000` 秒是最长等待时间。 如果服务器响应已经收到并且处理得更快，则会尽快删除预隐藏的HTML样式标记。

---
title: 使用JavaScript库安装Web SDK
description: 使用独立的CDN文件引用Web SDK库。
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# 使用JavaScript库安装Web SDK

在不使用[使用标记扩展](/help/tags/extensions/client/web-sdk/overview.md)的情况下安装Web SDK的替代方法是引用托管在CDN上的JavaScript库。 您可以直接引用库，也可以下载该库并将其托管在您自己的基础架构中。 它提供缩小的和完整的格式。

可以使用以下URL结构访问Web SDK库：

* **缩小**： `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **完整**： `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

有关要包含在URL中的最新版本，请参阅[发行说明](../release-notes.md)。 例如，版本2.19.1的完整版本的URL是`https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`。

## 添加代码

在HTML的`<head>`标记中尽可能高地添加以下代码块：

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

此代码异步创建一个`alloy`对象，该对象允许您调用任何Web SDK命令。 如果要同步加载Web SDK，可以删除代码块最后一行中的`async`属性。 删除`async`属性会阻止浏览器解析和渲染HTML文档的其余部分，直到加载和执行库为止。 一般情况下，建议不要再向用户显示主要内容之前发生这种额外延迟，但是根据贵组织的需求，这样做可能会有意义。

---
title: 使用JavaScript库安装Web SDK
description: 使用独立的CDN文件引用Web SDK库。
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 9876390f7ba34c312f2ce4c00fe39e3ea1ef1ace
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# 使用JavaScript库安装Web SDK

不使用标记扩展[&#128279;](extension.md)安装Web SDK的替代方法是引用托管在CDN上的JavaScript库。 您可以直接引用库，也可以下载该库并将其托管在您自己的基础架构中。 它提供缩小的和完整的格式。

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

此代码异步创建一个`alloy`对象，该对象允许您调用任何Web SDK命令。 如果要同步加载Web SDK，可以删除代码块最后一行中的`async`属性。 删除`async`属性会阻止浏览器解析和渲染HTML文档的其余部分，直到加载和执行库为止。 通常建议不要在向用户显示主要内容之前再出现这种延迟，但根据贵组织的需求，这样做可能比较合理。

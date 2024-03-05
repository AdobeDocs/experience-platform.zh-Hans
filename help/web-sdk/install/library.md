---
title: 使用JavaScript库安装Web SDK
description: 使用独立的CDN文件引用Web SDK库。
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# 使用JavaScript库安装Web SDK

安装Web SDK的一个选项是引用CDN上托管的JavaScript库。 您可以直接引用库，也可以下载该库并将其托管在您自己的基础架构中。 它提供缩小的和完整的格式。

可以使用以下URL结构访问Web SDK库：

* **缩小**： `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.min.js`
* **完整**： `https://cdn1.adoberesources.net/alloy/[VERSION]/alloy.js`

请参阅 [发行说明](../release-notes.md) ，以在URL中包含最新版本。 例如，版本2.19.1的完整版本的URL为 `https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`.

## 添加代码

将以下代码块添加到尽可能高的位置 `<head>` HTML的标记：

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<script src="https://cdn1.adoberesources.net/alloy/2.19.1/alloy.min.js" async></script>
```

此代码异步创建 `alloy` 用于调用任何Web SDK命令的对象。 如果要同步加载Web SDK，可以删除 `async` 代码块最后一行中的属性。 删除 `async` 属性会阻止浏览器解析和渲染HTML文档的其余部分，直到加载并执行库为止。 通常建议不要在向用户显示主要内容之前再出现这种延迟，但根据贵组织的需求，这样做可能比较合理。

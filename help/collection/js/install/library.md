---
title: 安装Web SDK JavaScript库
description: 使用独立的CDN文件引用Web SDK库。
exl-id: bacfe938-4326-48f6-a321-bd16970e77eb
source-git-commit: 010192e91185c11d5454d4153913c06b90fe2122
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# 安装Web SDK JavaScript库

如果您选择不使用[Web SDK标记扩展](/help/tags/extensions/client/web-sdk/overview.md)，可以通过引用Adobe CDN上托管的独立JavaScript库来安装Web SDK。 您可以直接引用库，也可以下载该库并将其托管在您自己的基础架构中。 它提供缩小的和完整的格式。

可以使用以下URL结构访问Web SDK库：

* **缩小**： `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js`
* **完整**： `https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.js`

有关要包含在URL中的最新版本，请参阅[Web SDK发行说明](../release-notes.md)。 例如，版本2.19.1的完整版本的URL是`https://cdn1.adoberesources.net/alloy/2.19.1/alloy.js`。

## 添加基础代码和库加载器

要添加的代码包含两个部分：

* **基础代码**：允许在Web SDK异步加载时通过排队命令进行引导。 有关详细信息，请参阅[基础代码](base-code.md)。 Adobe建议在异步加载库时使用基础代码，以避免在页面加载期间调用Web SDK命令时出现争用情况。
* **库加载器**：加载完整的JavaScript库。

在可能调用Web SDK的任何脚本之前，在`<head>`标记中尽可能高地添加以下代码块：

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!-- Library loader -->
<script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
```

如果要同步加载Web SDK，可以在加载库时删除`async`属性。 在浏览器获取和执行库时，删除`async`属性会阻止HTML解析。 一般情况下，建议不要再向用户显示主要内容之前发生这种额外延迟，但是根据贵组织的需求，这样做可能会有意义。

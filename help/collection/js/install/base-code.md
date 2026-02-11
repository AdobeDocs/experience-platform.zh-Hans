---
title: 基础代码
description: 当数据收集库异步加载时，对命令(bootstrap)进行排队。
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# 基础代码

在Adobe Experience Platform Web SDK异步加载时，基础代码通过排队命令启用引导过程。 基础代码运行后，您可以立即调用任何命令，如[`configure`](../commands/configure/overview.md)或[`sendEvent`](../commands/sendevent/overview.md)，而无需担心竞争条件或库完成加载时的时间。 当Web SDK完成加载时，排队的命令会以先进先出的顺序（与它们排队的顺序相同）执行。

命令会返回Promise，即使排队时也是如此。 如果命令已排入队列，则Promise将在Web SDK完成加载时运行该命令之后解析或拒绝。 如果Web SDK从未完成加载（例如，库加载失败），则已排队的Promise将保持挂起状态。

## 添加基础代码

将基础代码放在`<head>`标记中尽可能高的位置，放在可能调用Web SDK的任何脚本之前。

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

添加基础代码后，使用您选择的方法([JavaScript库加载器](library.md)或[Tags嵌入代码](/help/tags/extensions/client/web-sdk/getting-started.md))加载Web SDK。 对于基于标记的实施，Web SDK标记扩展2.34.0及更高版本支持基础代码。

此基础代码在以下情况下是&#x200B;**不需要**：

* 如果要同步加载JavaScript库，请执行以下操作。 在获取和执行库时，同步加载会阻止解析。
* 如果使用标记扩展，则所有对Web SDK的调用都将在标记规则或操作中进行。 仅当您的实施在标记库之外引用Web SDK时，才需要包含基础代码。 大多数标记实施通常不会在标记库之外调用Web SDK，因此大多数标记实施不需要基础代码。

## 示例

请参阅此代码示例中的注释，了解如何排队和解析命令的时间。 此示例同时适用于JavaScript库和标记扩展：

```html
<head>
  <script>
    // Calls made before the base code runs are not captured (alloy is not yet defined).
    // Always make sure that the base code runs before any attempt to call commands.
    // alloy("getLibraryInfo").then(console.log).catch(console.error);
  </script>

  <!-- Base code -->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!-- Queued command -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Queued call resolved:", result);
    }).catch(console.error);
  </script>

  <!-- Load the Web SDK using the JavaScript loader -->
  <script src="https://cdn1.adoberesources.net/alloy/<VERSION>/alloy.min.js" async></script>
  <!-- or the tag extension -->
  <!-- <script src=".../launch-<ENV>.min.js" async></script> -->

  <!-- Another call (queued if the library is still loading; immediate if it is ready) -->
  <script>
    alloy("getLibraryInfo").then(result => {
      console.log("Immediate call resolved:", result);
    }).catch(console.error);
  </script>
</head>
```

## 重命名SDK实例

您可以通过修改基础代码的最后一行来重命名所调用的全局函数。 更改：

```js
(window,["alloy"]);
```

收件人：

```js
(window,["ingot"]);
```

此更改允许您使用`ingot`而不是`alloy`调用命令：

```js
ingot("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

## 多个SDK实例

您可以选择使用基础代码在页面上配置多个SDK实例。 有关详细信息，请参阅[使用多个Web SDK实例](../../use-cases/multiple-instances.md)。

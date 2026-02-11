---
title: 使用多个Web SDK实例
description: 了解如何与多个Experience Platform Web SDK资产交互。
keywords: 多个属性
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 192739967e6b050bb04893ee7bab5119dd7f870c
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# 使用多个Web SDK实例

在某些情况下，您可能希望与同一页面上的两个不同属性进行交互。 可能的情况包括：

* 已被收购并正致力于整合其网站的公司
* 多个公司之间的数据共享关系
* 正在测试新的Adobe解决方案并且不想中断现有实施的客户

SDK允许您通过向[基代码](../js/install/base-code.md)中的数组添加其他名称，为每个属性创建单独的实例。 以下示例提供了两个名称： `titanium`和`copper`。

```html
<!-- Base code -->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n.setTimeout(function(){n[o].q.push([i,l,u])})})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>

<!-- Load the Web SDK (JavaScript library loader or Tags embed code) -->
<!-- <script src=".../alloy.min.js" async></script> -->
<!-- <script src=".../launch-<ENV>.min.js" async></script> -->
```

因此，脚本将创建两个全局函数（上例中的`titanium`和`copper`），在库初始化时，这两个函数会变成两个SDK实例。 每个实例都维护自己的配置和状态；任何使用`titanium`的命令都与`copper`隔离。

>[!TIP]
>
>如果将基础代码与标记一起使用，则在配置标记扩展时，请确保您设置的所有实例名称与所有[SDK实例名称](/help/tags/extensions/client/web-sdk/configure/general.md)匹配。

按照`titanium`和`copper`作为Web SDK实例的命名模式示例，您可以独立执行命令：

```javascript
titanium("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

titanium("sendEvent", {
  data: {
    key: "value"
  }
});

copper("configure", {
  datastreamId: "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  orgId: "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

copper("sendEvent", {
  data: {
    key: "value"
  }
});
```

请确保先对每个实例执行[`configure`](../js/commands/configure/overview.md)命令，然后再在同一实例上执行其他命令。

>[!IMPORTANT]
>
>为避免与Cookie冲突，每个Web SDK实例必须具有自己的唯一`datastreamId`和自己的唯一`orgId`。

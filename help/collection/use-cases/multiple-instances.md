---
title: 使用多个Web SDK实例
description: 了解如何与多个Experience Platform Web SDK资产交互。
keywords: 多个属性
exl-id: e07afb0d-3490-414f-bc9c-f71bc04fe664
source-git-commit: 2c60ebdebd706ed7b5beb2438ae83665b6b6e47a
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# 使用多个Web SDK实例

在某些情况下，您可能希望与同一页面上的两个不同属性进行交互。 这些情况包括：

* 已被收购并正致力于整合其网站的公司
* 多个公司之间的数据共享关系
* 正在测试新的Adobe解决方案并且不想中断现有实施的客户

SDK允许您向基础代码中的数组添加其他名称，为每个属性创建单独的实例。 以下示例提供了两个名称： `titanium`和`copper`。

```html
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["titanium", "copper"]);
</script>
<script src="alloy.js" async></script>
```

因此，该脚本将创建两个SDK实例。 与第一个实例交互的全局函数名为`titanium`，与第二个实例交互的全局函数名为`copper`。

通过创建两个单独的实例，可以为每个实例配置不同的属性。 由于与`titanium`交互而发生的任何通信或数据持久性均与`copper`保持隔离。

在上例之后，您可以使用每个实例执行命令：

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

请确保先对每个实例执行`configure`命令，然后再在同一实例上执行其他命令。

>[!IMPORTANT]
>
>为避免与Cookie冲突，每个Web SDK实例必须具有自己的唯一`datastreamId`和自己的唯一`orgId`。

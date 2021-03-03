---
title: 与Adobe Experience Platform Web SDK中的多个属性交互
description: 了解如何与多个Experience Platform Web SDK属性交互。
keywords: 多个属性；configure;sendEvent;edgeConfigId;orgId;
translation-type: tm+mt
source-git-commit: b865b7fb940ca2d5f8b44f71eb58e62e3473f52d
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# 与多个属性交互

在某些情况下，您可能希望与同一页面上的两个不同属性进行交互。 这些案例包括：

* 已获得并正在努力将其网站集成到一起的公司
* 多个公司之间的数据共享关系
* 正在测试新Adobe解决方案且不想破坏其现有实施的客户

SDK允许您通过在基本代码中向数组添加另一个名称，为每个属性创建一个单独的实例。 下面的示例提供两个名称，`mycustomname1`和`mycustomname2`。

```markup
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["mycustomname1", "mycustomname2"]);
</script>
<script src="alloy.js" async></script>
```

因此，该脚本创建了两个SDK实例。 与第一实例交互的全局函数名为`mycustomname1`，与第二实例交互的全局函数名为`mycustomname2`。

通过创建两个单独的实例，可以为每个实例配置不同的属性。 由于与`mycustomname1`交互而发生的任何通信或数据持久性都与`mycustomname2`隔离。

在上面的示例中，您可以使用每个实例执行命令，如下所示：

```javascript
mycustomname1("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg"
});

mycustomname1("sendEvent", {
  "data": {
    "key": "value"
  }
});

mycustomname2("configure", {
  "edgeConfigId": "f46e981f-fd03-4bdd-a9d9-73ce4447f870",
  "orgId": "ADB3NUMBERSANDLETTERS2@AdobeOrg"
});

mycustomname2("sendEvent", {
  "data": {
    "key": "value"
  }
});
```

请务必为每个实例执行`configure`命令，然后对同一实例执行其他命令。

## 限制

为避免与Cookies冲突，页面中只有Adobe Experience Platform [!DNL Web SDK]的一个实例可以具有特定的`edgeConfigId`。 同样，只有Adobe Experience Platform [!DNL Web SDK]的一个实例可以具有特定的`orgId`。
